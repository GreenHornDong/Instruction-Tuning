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

#### IFT原理探究
1、FLAN(finetune language net)，谷歌在本文中首次提出Instruction tuning，文章将指令微调后的137B的模型和175B的GPT-3进行了比较，证明了指令微调的优越性。文章使用62个文本数据集，划分为12个类别，对于每个数据集，文章手工构建了10个独特的模板，这些模板使用自然语言instructions 来描述该数据集的任务。这10个模板中的大多数描述了原始任务，但为了增加多样性，对于每个数据集，还包括最多三个“turned the task around”的模板（例如，对于情感分类，要求生成电影评论的模板，可以增加指令多样性）。然后，将所有数据集混合后，对预训练语言模型做instruction tuning，其中每个数据集的template都是随机选取的。对比实验表明，实验1、任务类别越多，微调效果越好，也就是指令越多样，效果越好。实验2、模型size越大，效果越好，小模型进行微调可能会降低性能。实验3、主要研究instruction本身的设定对tuning的作用。模型效果变好的一种可能是任务量比较多，fine-tuning过程即使不加instruction也能达到很好的效果。本文设计了两种不带有instruction的fine-tuning模式作对比，一种是no template，只提供给模型输入和输出。另一种是dataset name，它在输入前面拼接上task和数据集名称。对比结果表明带有指令的数据微调效果比no template高18个点，比dataset name高8个点。

<br />数据：手工设计模板，从现有数据集根据模板进行转换，数据量很大。
<br />https://arxiv.org/pdf/2109.01652.pdf  Finetuned Language Models are Zero-Shot Learners

2、同年，谷歌针对CoT(chain of thought，链式思维)在Instruction-Tuning中能否提升模型的能力，以及模型大小和数据集大小对指令调优的影响进行了进一步探究，这篇文章用了146个任务类别，473个数据集，1836 种指令任务，最终确定指令微调任务的多样性可以提升模型的能力, CoT数据可以显著提升模型的推理能力(以及在未见任务上的泛化能力), 模型规模越大，经过指令微调的效果越好，还没看到上限，文中最大540B

<br />数据：手工构造，数据量很大，CoT数据为人工编写。
<br />https://doi.org/10.48550/arXiv.2210.11416   Scaling Instruction-Finetuned Language Models

3、指令微调如何提升模型性能呢，这篇文章给出了一些定量分析，从token的偏移角度出发，对比微调后的模型和微调前的模型的回答的token分布，发现token会产生%5-8%左右的偏移(使用的模型为 Llama-2-7b -> Llama-2-7b-chat,  Llama-2-7b -> Vicuna-7b-v1.5, Mistral-7b -> Mistral-7b-instruct), 而且产生偏移的多数都是风格token，比如however, if这种词汇，会让模型的回答更加流畅和清晰，而模型回答中的关键词汇和信息，是模型本身经过预训练以后就具有的，也就是base模型和chat模型(tuned)产生的回答中关键信息一致，很有趣，所以这篇文章使用ICL作为提示+系统提示来代替指令微调。  

<br />数据：手工构造，本文ICL数据的构造步骤较为繁琐。
<br />https://arxiv.org/abs/2312.01552   The Unlocking Spell on Base LLMs: Rethinking Alignment via In-Context Learning

4、从上述问题出发，国内软件所联合美团提出以下论文，并发表观点：(1) 对于指令微调而言，学习与模型参数知识不一致的世界知识无法带来增益，甚至会造成额外的损害。(2) 有效指令微调的本质在于完成行为模式转换的同时，保持指令微调前后模型参数知识的一致性，但是使用与模型内部参数知识完全一致的指令数据并不总能取得最优性能。    换句话说，指令微调的核心作用机制并不是让模型去“学习”额外的知识，而是将模型内部现有的知识进行一种自我的对齐。这个其实就很符合一直以来的猜想，模型学不到额外知识，毕竟你参数也没怎么更新，指令微调数据里面的内容也都是用的已有的数据，所以只是让模型学会回答，这篇文章也对应文章3的使用ICL去替代指令调优，因为本质上ICL连参数更新都没有，更是教会模型如何去回答信息，从而可以产生和IFT相似的效果。文章通过计算指令微调前后模型预测排序的Pearson相关系数，来衡量模型内部知识的一致性，在一定范围内，微调数据一致性越高，模型效果越好。

<br />数据：手工构造，从医学、历史、工程和法学四个领域中筛选现有数据集的数据，构造三种训练集分别是Harmonious， Incompatible和Self-aligning，依据是模型在Few-shor ICL情况下能给出正确答案的就是Harmonious，给不出正确答案的是Incompatible，Self-aligning选用和Incompatible一致的指令和问题，但是回答则使用模型本身能够给出的回答。
<br />https://arxiv.org/abs/2402.18243   Learning or Self-aligning? Rethinking Instruction Fine-tuning

#### IFT数据
指令微调数据集有很多，如
<br />Alpaca(https://github.com/tatsu-lab/stanford_alpaca), 
<br />使用self-Instruct的方式生成数据，self-Instruct介绍见下文，数据生成模型使用OpenAI’s text-davinci-003，生成52K的IFT数据
<br />Dolly(https://www.databricks.com/blog/2023/04/12/dolly-first-open-commercially-viable-instruction-tuned-llm)
<br />dolly-15k是由5000多名Databricks员工在2023年3月和4月期间手工创建的。包括开放式问答，封闭式问答，信息提取，总结，头脑风暴，分类和创造性写作。
<br />HC3(https://github.com/Hello-SimpleAI/chatgpt-comparison-detection)
<br />人机对比语料库:数以万计的对比回答，分别来自人类专家和ChatGPT，涵盖了开放领域、金融、医疗、法律和心理学等领域。
<br />WizardLM(https://github.com/nlpxucan/WizardLM)
<br />使用Alpaca的训练数据集作为初始指令集，使用ChaGPT通过4个epoch将其重写为更复杂的指令，得到175K指令数据集 
<br />LIMA(https://arxiv.org/pdf/2305.11206.pdf)
<br />1K的训练数据，75%是从三个社区问答网站（Stack Exchange、wikiHow和Pushshift Reddit）中抽样的；20%手工编写，5%来自Super-Natural Instructions数据集的抽样。


#### IFT数据筛选
许多方法选择数据的依据为多样性和质量，利用GPT-3.5或者一些现有的大模型给指令数据集的质量进行打分，利用K-means聚类等方法将指令数据集划分为不同簇，从而选择更加多样的数据。

1、通过多样性和质量共同进行自动挑选(首次引入)，多样性的选择依据是设置位置函数(facility location function), 给定数据集V，选出子集A，使得A中的a与V中的v距离最大
<img width="628" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/371686b1-b4c4-4ec7-ae17-e0778929aff4">
<br />数据质量则使用ChatGPT进行打分或者使用scoring model进行打分，Quality-Diversity Instruction Tuning(QDIT)的分数是多样性和质量的线性组合 f (a|A,α) = (1−α)d(a|A)+αq(a), α是控制质量和多样性的超参数，d(a|A)代表多样性分数，q(a)代表质量分数。依靠上述过程选出指令微调数据，消融实验表明，相对于随机选择和基于质量的选择，该方法效果更好，但是带来的计算开销较大，总数据集为V的话，每次挑选一个a使得QDIT最大需要的时间复杂度为O(V的三次方)，挑选K个则是O(V的三次方*K)。为了确保挑选出的数据确实满足多样性指标，文章使用伯克利神经解析器解析数据集中的根动词和第一直接名词，与随机选择和基于质量的挑选方式比较，表明文章方法确实有效。

<br />数据：小数据集：Alpaca52K，Dolly 15K，大数据集：Ultrachat 1.3M, LMSYS-Chat 1M，组合数据集Alpaca 52K+Dolly 15K+OIG-small-chip2 210K。每个大数据集选10K个数据，小数据集选原数据集的5%左右
<br />https://arxiv.org/pdf/2305.11206.pdf  Data Diversity Matters for Robust Instruction Tuning

2、通过Chatgpt对Alpaca的52K数据进行打分(0-5)，选择分数高于4.5的数据，共计9K，在9K高质量数据上进行微调的结果要优于Alpaca, 在多种数据集和模型上的实验表明文章方法确实有效。

<br />数据：Chatgpt对数据打分，根据分值高于某一阈值筛选IFT数据
<br />https://arxiv.org/pdf/2307.08701.pdf  ALPAGASUS: TRAINING A BETTER ALPACA WITH FEWER DATA

3、MoDS从数据质量、多样性、必要性三个角度来对原始数据集进行数据过滤，以往方法多考虑质量和多样性，没有针对不同模型考虑数据必要性。质量和多样性顾名思义，数据必要性是选择对于大模型较复杂、较难或不擅长的数据，以填补大模型能力的空白。数据质量：采用OpenAssistant的reward-model-debertav3-large-v2模型对数据进行打分，选择出高质量数据集Data；然后使用K-Center-Greedy算法(采用BERT模型生成句向量来计算不同数据之间的距离)对Data1进行数据筛选, 得到种子数据集(Seed Instruction Data)SID。数据必要性：对于一条指令，如果LLM本身回答较好，则说明LLM具有处理该指令的能力，而那些不能处理的指令对于模型微调来说更重要，因此使用SID先微调LLM得到Initial LLM,用Initial LLM对高质量数据集Data1进行response，利用奖励模型对结果进行评分，当分值小于阈值β时，说明Initial LLM不具有处理这些类型指令的能力，获取必要性数据集Data2，对Data2进行多样性筛选，获取增强指令数据集(Augmented Instruction Data)AID。最终使用SID和AID微调并获得最终模型。

<br />https://arxiv.org/pdf/2311.15653.pdf   MoDS: Model-oriented Data Selection for Instruction Tuning
<br />https://github.com/CASIA-LM/MoDS

4、该论文提出一种迭代的筛选指令微调数据数据集的方法，Self-Evolved：给定初始模型M和初始数据集V，随机挑选K个数据点作为P0，剩下的数据作为Q0，使用P0微调M，得到M1，使用M1模型计算数据集的embedding，使用K均值聚类从Q0中挑选K个距离P0最远的数据，并将其加入P0得到P1，使用P1微调模型得到M2，此时Q1是V-P1，然后按照上述方法迭代T次，得到最终的模型MT。对比实验表明该方法在许多情况下优于使用完整IFT数据集的方法，并可以降低计算消耗。

<br />https://arxiv.org/pdf/2311.08182.pdf   Self-Evolved Diverse Data Sampling for Efficient Instruction Tuning 
<br />https://github.com/OFA-Sys/DiverseEvol

5、这篇文章假设SFT应该选择最能反映人类风格的示例。例如，教导LLM巴黎是法国的首都的示范是无益的，因为LLM在预训练阶段已经获得了这样的知识。相反，包含诸如“谢谢”和“首先”等词语的人类风格响应以及包含编号列表的结构化响应对于SFT是有帮助的(与上面的论文3和4相呼应)。文章指出选择响应更长的指令数据往往比多样性和质量高的指令数据表现更加稳定，相同的数据量选择响应更长的指令数据使得微调后的模型效果更好，为了评估模型的效果，选用GPT-4给两个response进行打分并给出解释，为了防止顺序的影响，会把两个response顺序进行交换，当GPT-4对交换前后的评定一致时，认为本次评定有效，消除顺序偏差，其次，在之前的研究中发现GPT-4对于长文本响应的偏好并不大，所以不考虑这一偏差。但是为了明确实验效果，后续采取人工评定的方式对响应进行打分，发现多数情况下GPT-4的选择并不是基于越长越好，50个对话里只有4个是因为响应文本长才使得GPT-4认为其更好。为了研究具有长回复的指令分布，文章使用伯克利神经解析器对来自Alpaca数据集中具有长回复的前1k个实例的指令的前20个最常见的根动词及其前4个直接名词对象进行解析，发现“写作”、“生成”、“创建”和“撰写”等指令根动词组成了所有指令的70％。

<br />数据：从已有数据集Alpaca 52K  WizardLM 70K  Dolly 15K挑选长文本数据
<br />https://doi.org/10.48550/arXiv.2402.06094  Rethinking Data Selection for Supervised Fine-Tuning

#### IFT数据生成
1、self-Instruct，使用LLM自动生成指令数据，步骤如下：首先，手工设计了175个表示不同任务的指令，并且给每条数据都编写了（指令, 输入, 输出）/（指令, 输出），将这175条数据作为种子池。其次，使用模型生成新的指令(使用few-shot ICL方式)，对该模型生成的指令判断是否分类任务(prompt模板不同，这里也使用few-shot ICL方式)。然后，使用模型生成实例，对上述模型生成的数据进行过滤和后处理，将经过过滤和后处理的数据添加到种子池中，一直重复上述步骤。文章使用GPT-3进行生成数据，并以此数据微调GPT-3，结果表明相比于原始GPT-3，其能力大幅提升，甚至可以和Instrcut-GPT001媲美。

<br />数据：从175个指令数据出发，使用GPT-3生成了52K的指令，82K的实例。
<br />https://arxiv.org/pdf/2212.10560.pdf  Self-Instruct: Aligning Language Model with Self Generated Instructions
<br />https://github.com/yizhongw/self-instruct

2、使用Evol-Instruct方法生成指令数据集，使用所有生成的指令数据来对LLaMA-7B进行微调得到WizardLM。Evol-Instruct：从简单的初始指令“1+1=？”开始，随机选择In-depth Evolving或In-breadth Evolving将简单指令升级为更复杂的指令或创建一个新的指令（增加多样性）。In-depth Evolving包括五种操作：添加约束、加深、具体化、增加推理步骤和复杂化输入。In-breadth Evolving是突变，即根据给定的指令生成一个全新的指令。这六种操作通过提示ChaGPT来实现。由于演化后的指令是从LLMs生成的，采用一个指令消除器过滤失败的指令。重复这个演化过程几轮，以获取包含各种复杂性的足够指令数据。对比实验表明Evol-Instruct生成的指令优于人类创建的指令。通过分析高复杂度部分的人类评估结果，证明了WizardLM模型的输出优于OpenAI ChatGPT的输出。在GPT-4的自动评估中，WizardLM在29个任务中的17个超过了ChatGPT的90%。

<br />数据：从Alpaca训练数据出发，使用Evol-Instruct生成175K的指令微调数据集。
<br />https://arxiv.org/pdf/2304.12244.pdf  WizardLM: Empowering Large Language Models to  Follow Complex Instructions
<br />https://github.com/nlpxucan/WizardLM

3、这篇论文通过精心设计的1000个示例，来证明多样性和质量高的指令微调数据集足以胜过大量质量不高的数据集。对比实验表明经过1K微调的LLaMA-65B(LIMA)模型效果优于Alpaca 65B(52K数据微调)和DaVinci003。消融实验微调LLaMa-7B模型，使用GPT-3.5 Turbo打分，生成5个response取平均。得出结论如下：1、LLM的知识几乎全来自预训练阶段 2、多样性和数据质量对模型效果的影响都非常大，数据量几乎无影响。文章最后的消融实验将经过1k数据微调的模型在30个多轮对话样本上再次微调，就大幅提升了模型的多轮对话能力，再次证明质量和多样性是关键，而非数据量。

<br />数据：750个手工构造于三个社区论坛中，而剩余的250个为人工创作。
<br />https://arxiv.org/pdf/2305.11206.pdf     LIMA: Less Is More for Alignment


### 多模态大语言模型领域

近两年指令微调不仅在LLM领域，在多模态领域也是一大热点，经过探究和实验，许多学者认为，指令调优意在对齐模型的内部知识，让模型学会回答，这才是指令调优提升模型能力的重点，所以经过浓缩后的指令调优数据集可能仅有几千条，但是足以提升模型的能力。


#### 大模型(size >= 7B)
1、MULTIINSTRUCT从现有的21个视觉语言数据集中构造了10类任务，具体包括62个任务，并手工为每类任务设计5个指令模板，文章还探究使用纯语言指令数据(NATURAL INSTRUCTIONS)结合MULTIINSTRUCT的微调效果。62个任务中有34个任务是从现有数据集获取的，剩下的28个任务通过从现有任务进行改写生成，例如区域描述任务可以改写为根据描述选择对应区域和根据区域选择对应描述。针对每个任务，生成5000-5M个实例，每个实例随机使用5个任务模板中的一个。实验结果表明，经过微调的OFA模型的多模态zero-shot能力大幅提升，首先在纯文本指令数据集NATURAL INSTRUCTIONS上微调，再在MULTIINSTRUCT数据上微调，可以获得表现最优的模型。消融实验表明：1、与FLAN类似，通过逐步增加视觉指令微调数据的种类和数量，模型的效果会越来越好，2、仅使用文本指令微调会降低模型的视觉理解能力，原因是模型对视觉标记的关注减少。
<img width="552" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/6ce93287-a37d-41ec-8a4a-e9eca847251b">

<br />https://arxiv.org/pdf/2212.10773.pdf   MULTIINSTRUCT: Improving Multi-Modal Zero-Shot Learning via Instruction Tuning
<br />https://github.com/VT-NLP/MultiInstruct

2、LLaVA模型在158K的IFT数据集上进行微调，数据来源为现有的视觉描述数据集，将其中的图片描述+图像(将图像转换为由文本表示的Context，文章采用了两种Context，一种是图片描述，另一种是box以及对应物体的种类。)等信息以文本格式输入GPT-4或者Chatgpt，让他们生成对应的问题和回答，指令手工制作，但是格式和内容十分简单，基本是围绕详细描述一下图片中的内容这种话制定的。

<br />https://arxiv.org/pdf/2304.08485.pdf     Visual Instruction Tuning
<br />https://github.com/haotian-liu/LLaVA/blob/main/docs/Data.md

3、M3IT数据集有40个数据集，包括240万个实例和400个手工编写的任务说明(每个数据集对应10个)，涵盖多样化的任务，包括字幕生成、视觉问答（VQA）、视觉条件生成、推理和分类。对使用图像特定区域的任务，将box注释直接在图像上用红色框标出，并使用Chatgpt改写VQA数据集中的的较短回答，测量指令数据之间的距离，确保指令多样性。最后通过人工筛查选出完整有效的数据。数据集格式为：图像(base64编码)，指令(从10个中随机选一个)，输入，输出，元数据(图像id,wikipedia_id等)。经上述数据集微调的模型展现出强大的zero-shot能力。

<img width="453" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/9f08eb23-e9e8-4b9a-a492-fcf7e048d421">

<br />https://doi.org/10.48550/arXiv.2306.04387    M3IT: A Large-Scale Dataset towards Multi-Modal Multilingual Instruction Tuning
<br />https://huggingface.co/datasets/MMInstruction/M3IT

4、VIGC生成的数据集，MLLM自动生成的首个多模态微调数据集，包括36,781个VIGC-LLaVA COCO和约180万个VIGC-LLaVA Objects365。VIGC借助了LLM中self-instruct的思想，通过多模态模型自身来生成指令。具体做法：首先在已有的Instrcution finetune数据集(llava150k和 OKVQA，A-OKVQA)上进行的训练得到一个能够根据给定图像生成对话的模型VIGC(包括生成和矫正)，然后再使用COCO和obj365作为图像数据集生成对应的指令微调数据。实验表明在生成的高质量数据上进行微调可以提升模型的泛化性能。

<br />https://arxiv.org/pdf/2308.12714.pdf     VIGC: Visual Instruction Generation and Correction
<br />https://opendatalab.github.io/VIGC/

5、LAMM是一个全面的多模态指导调整数据集，用于2D图像和3D点云的理解。该数据集包含了18.6万个语言-图像指令响应对，以及1万个语言-点云指令响应对。作者从公开可用的数据集中收集图像和点云，并使用GPT-API和自指令方法根据这些数据集的原始标签生成指令和响应。LAMM数据集还包括了用于常识知识问答的数据对，通过将来自Bamboo数据集和相应的维基百科描述的分层知识图标签系统结合起来。

<br />https://arxiv.org/pdf/2306.06687.pdf    LAMM:Language-Assisted Multi-Modal Instruction-Tuning Dataset, Framework, and
 Benchmark
 <br />https://github.com/OpenGVLab/LAMM

6、LLaVA-1.5所使用的微调数据，公开可用，详细信息如下。ALLAVA中也使用了该数据进行微调。
 <img width="393" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/cc3281b7-7f9d-460a-8f3b-7be933e302db">
<br />https://arxiv.org/abs/2310.03744      Improved Baselines with Visual Instruction Tuning
<br />https://llava-vl.github.io/
 
7、shareGPT-4V, 首先将10万张图像输入GPT-4V，生成高质量的图像文本数据，使用这些数据训练一个share-Captioner,然后将收集的120万张图像输入share-Captioner生成高质量图文数据集，从而得到120万高质量的图像文本数据，使用该数据训练的模型效果要优于原有模型，如LLaVA-7B，LLaVA-1.5-7B, LLaVA-1.5-13B, Qwen-VL-Chat-7B。最后使用该数据训练一个shareGPT-4V-7B，并在同类型模型中性能最佳。
<br />https://arxiv.org/abs/2311.12793     ShareGPT4V: Improving Large Multi-Modal Models with Better Captions
<br />https://sharegpt4v.github.io/

8、Vision-Flan，最大的人工注释的视觉IFT数据集，包含来自101个开源计算机视觉数据集的200多个多样化的视觉-语言任务。每个任务都配备有专家编写的说明和精心设计的输入和输出模板。该数据集涵盖了诸如图像字幕生成、视觉问答和视觉理解等各种任务。

<br />https://arxiv.org/abs/2402.11690     Vision-flan: Scaling human-labeled  tasks in visual instruction tuning
<br />https://vision-flan.github.io/


#### 小模型(size ~3B)
1、现有数据如Vision-FLAN的指令过于简单，但是一般来说，越复杂的指令越能够提升模型的指令跟随能力，本文考虑从现有图像出发，使用GPT-4V重新构造数据集，图片数据源来自Vision-FLAN和LAION，将图像输入GPT-4V，首先提示其生成完整的图像描述，然后根据图像描述和对应图片生成一个问题和对应的答案。在提示中要求GPT-4V生成的指令复杂，问题多样，以及回答详细。使用3B左右的参数和高质量的数据，训练的模型在各种任务上表现很好，甚至可以和7B，13B的一些模型相媲美。
<br />https://doi.org/10.48550/arXiv.2402.11684    ALLAVA: HARNESSING GPT4V-SYNTHESIZED DATA FOR A LITE VISION-LANGUAGE MODEL
<br />https://github.com/FreedomIntelligence/ALLaVA

2、3B左右的模型Imp，使用和LLaVA1.5一致的训练数据，558K的LCS预训练数据(blip_laion_cc_sbu_558k)和665K的指令微调数据(llava_v1_5_mix665k)，模型架构为 Phi-2(2.7B) + SigLIP(0.4B)。模型效果如下：
<img width="628" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/f4777eef-e157-45ac-a55a-6331ffa5493c">

@misc{imp2024,
  author = {Shao, Zhenwei and Ouyang, Xuecheng and Gai, Zhenbiao and Yu, Zhou and Yu, Jun},
  title = {Imp: An emprical study of multimodal small language models},
  year = {2024},
  url = {https://huggingface.co/MILVLG/imp-v1-3b}
}
<br />https://github.com/MILVLG/imp/tree/main
