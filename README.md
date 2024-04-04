# Instruction-Tuning

## 主要内容
本仓库记录学习几年来在LLM领域(以及多模态大模型领域)的指令微调相关知识，指令微调(instruction finetuning)，又作指令调优(instruction tuning)，指令跟随(instruction following)。

## 名词缩写
LLM：Large language model 大语言模型
<br />MLLM：Multimodal large language model 多模态大语言模型
<br />ICL：In context learning 上下文学习
<br />FT：Finetune 微调
<br />IFT：Instruction finetune 指令微调

## 什么是指令微调
大语言模型和多模态大语言模型在下游任务上的性能，可以通过在指定任务上进行微调(fientune)提升，或者给定少量提示来增强模型回答的流畅度和准确度，也叫做few-shot prompt，不同于few-shot prompt， 这种方式下模型的参数完全不更新，因此又叫做In context learning(上下文学习)，指令微调是为了让模型能够理解人类指令，在不给出提示的情况下，增强模型的zero-shot能力的一种方式，比如，你可以在许多任务上进行指令微调，在其他任务上(unseen, 模型未见过)进行测试，你会发现模型的理解能力有所提升，可以给出更好的答案。

<br />换句话说，few-shot-prompt旨在使用的时候，给出几个样例，让模型知道应该怎么去回答，而IFT则是在预训练阶段以后，在构建的指令数据集上对模型进行微调，使用的时候模型会给出更好的回答。

<br />假如你问模型1+2=?。

<br />few-shot-prompt的问题格式一般是: 
<br />Question: 1+3=? Aswer: 4  <br />Question: 2+3=? Aswer: 5  <br />Question: 1+2=?
<br />然后模型给出回答，这里有两个样例，所以是2-shot

<br />对于经过IFT的模型，直接问，Question: 1+2=?就可以。

### 数据构成
指令微调数据一般如下：
<br />{###Insruction:...., ###Input:...., ###Answer:....} 
<br />举个例子，问模型1+1等于几， 微调数据就是<br />{###Insruction:在接下来的input中，我给你两个数字，你能够告诉我两个数字的和吗, ###Input: 1，1, ###Answer: 2}。<br />以上就是一条微调数据，当然，你可以更换数据模板，比如不用Input，或者给一些提示(few-shot)，或者在答案中给出CoT, 也就是整个答案的推理过程。

## 经典论文
### LLM领域
1、或许你曾经听过FLAN(finetune language net)，谷歌在本文中首次提出Instruction tuning，文章将指令微调后的137B的模型和175B的GPT-3进行了比较，证明了指令微调的优越性
<br />https://arxiv.org/pdf/2109.01652.pdf  Finetuned Language Models are Zero-Shot Learners

2、同年，谷歌针对CoT(chain of thought，链式思维)和few-shot在Instruction-Tuning中能否提升模型的能力，以及模型大小和数据集大小对指令调优的影响进行了进一步探究，这篇文章用了146种任务，473个数据集，最终确定指令微调任务的多样性可以提升模型的能力, CoT数据可以提升模型的推理能力, 模型规模越大，经过指令微调的效果越好，还没看到上限，文中最大540B
<br />https://doi.org/10.48550/arXiv.2210.11416   Scaling Instruction-Finetuned Language Models

3、有没有想过为什么指令微调效果会变好呢，这篇文章给出了一些定量分析，从token的偏移角度出发，对比微调后的模型和微调前的模型的回答的token分布，发现token会产生%5-8%左右的偏移(使用的模型为 Llama-2-7b -> Llama-2-7b-chat,  Llama-2-7b -> Vicuna-7b-v1.5, Mistral-7b -> Mistral-7b-instruct), 而且产生偏移的多数都是风格token，比如however, if这种词汇，会让模型的回答更加流畅和清晰，而模型回答中的关键词汇和信息，是模型本身经过预训练以后就具有的，也就是base模型和chat模型(tuned)产生的回答中关键信息一致，很有趣，所以这篇文章使用ICL作为提示+系统提示来代替指令微调。  <br />https://arxiv.org/abs/2312.01552   The Unlocking Spell on Base LLMs: Rethinking Alignment via In-Context Learning

4、从上述问题出发，国内软件所联合美团提出以下论文，并发表观点：(1) 对于指令微调而言，学习与模型参数知识不一致的世界知识无法带来增益，甚至会造成额外的损害。(2) 有效指令微调的本质在于完成行为模式转换的同时，保持指令微调前后模型参数知识的一致性，但是使用与模型内部参数知识完全一致的指令数据并不总能取得最优性能。    换句话说，指令微调的核心作用机制并不是让模型去“学习”额外的知识，而是将模型内部现有的知识进行一种自我的对齐。这个其实就很符合一直以来的猜想，模型学不到额外知识，毕竟你参数也没怎么更新，指令微调数据里面的内容也都是用的已有的数据，所以只是让模型学会回答，这篇文章也对应文章3的使用ICL去替代指令调优，因为本质上ICL连参数更新都没有，更是教会模型如何去回答信息，从而可以产生和IFT相似的效果。文章通过计算指令微调前后模型预测排序的Pearson相关系数，来衡量模型内部知识的一致性。
<br />https://arxiv.org/abs/2402.18243   Learning or Self-aligning? Rethinking Instruction Fine-tuning

#### 数据集的挑选
指令微调数据集有很多，如
<br />Alpaca(https://github.com/tatsu-lab/stanford_alpaca), 
<br />WizardLM(WizardLM: Empowering large pretrained language models to follow complex instructions, https://openreview.net/forum?id=CfXh93NDgH),
<br />Dolly(https://www.databricks.com/blog/2023/04/12/dolly-first-open-commercially-viable-instruction-tuned-llm)

#### 数据集的挑选策略
许多方法选择数据的依据为多样性和质量，利用GPT-3.5或者一些现有的大模型给指令数据集的质量进行打分，利用K-means聚类等方法将指令数据集划分为不同簇，从而选择更加多样的数据。

5、这篇文章假设SFT应该选择最能反映人类风格的示例。例如，教导LLM巴黎是法国的首都的示范是无益的，因为LLM在预训练阶段已经获得了这样的知识。相反，包含诸如“谢谢”和“首先”等词语的人类风格响应以及包含编号列表的结构化响应对于SFT是有帮助的(与上面的论文3和4相呼应)。文章指出选择响应更长的指令数据往往比多样性和质量高的指令数据表现更加稳定，相同的数据量选择响应更长的指令数据使得微调后的模型效果更好，为了评估模型的效果，选用GPT-4给两个response进行打分并给出解释，为了防止顺序的影响，会把两个response顺序进行交换，当GPT-4对交换前后的评定一致时，认为本次评定有效，消除顺序偏差，其次，在之前的研究中发现GPT-4对于长文本响应的偏好并不大，所以不考虑这一偏差。但是为了明确实验效果，后续采取人工评定的方式对响应进行打分，发现多数情况下GPT-4的选择并不是基于越长越好，50个对话里只有4个是因为响应文本长才使得GPT-4认为其更好。为了研究具有长回复的指令分布，文章使用伯克利神经解析器对来自Alpaca数据集中具有长回复的前1k个实例的指令的前20个最常见的根动词及其前4个直接名词对象进行解析，发现“写作”、“生成”、“创建”和“撰写”等指令根动词组成了所有指令的70％。
<br />https://doi.org/10.48550/arXiv.2402.06094  Rethinking Data Selection for Supervised Fine-Tuning

6、这篇论文通过精心设计的1000个示例，来证明多样性和质量高的指令微调数据集足以胜过大量质量不高的数据集。消融实验微调LLaMa-7B模型，使用GPT-3.5 Turbo打分，生成5个response取平均。得出结论如下：1、LLM的知识几乎全来自预训练阶段 2、微调使模型学习到输出回答的方式 3、通过小规模的优质数据便可以进行高效对齐。
<br />https://arxiv.org/pdf/2305.11206.pdf   LIMA: Less Is More for Alignment

7、通过多样性和质量共同进行自动挑选(首次引入)，多样性的选择依据是设置位置函数(facility location function), 给定数据集V，选出子集A，使得A中的a与V中的v距离最大
<img width="628" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/371686b1-b4c4-4ec7-ae17-e0778929aff4">
数据质量则使用CHatGPT进行打分或者使用scoring model进行打分，Quality-Diversity Instruction Tuning(QDIT)的分数是多样性和质量的线性组合 f (a|A,α) = (1−α)d(a|A)+αq(a), α是控制质量和多样性的超参数，d(a|A)代表多样性分数，q(a)代表质量分数。依靠上述过程选出指令微调数据，消融实验表明，相对于随机选择和基于质量的选择，该方法效果更好，但是带来的计算开销较大，总数据集为V的话，每次挑选一个a使得QDIT最大需要的时间复杂度为O(V的三次方)，挑选K个则是O(V的三次方*K)。为了确保挑选出的数据确实满足多样性指标，文章使用伯克利神经解析器解析数据集中的根动词和第一直接名词，与随机选择和基于质量的挑选方式比较，表明文章方法确实有效。
<br />https://arxiv.org/pdf/2305.11206.pdf  Data Diversity Matters for Robust Instruction Tuning



### 多模态大语言模型领域

近两年指令微调不仅在LLM领域，在多模态领域也是一大热点，经过探究和实验，许多学者认为，指令调优意在对齐模型的内部知识，让模型学会回答，这才是指令调优提升模型能力的重点，所以经过浓缩后的指令调优数据集可能仅有几千条，但是足以提升模型的能力。
 
