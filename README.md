# Instruction-Tuning

本仓库记录学习几年来在LLM领域的指令微调相关知识，指令微调(instruction finetuning)，又作指令调优(instruction tuning)，指令跟随(instruction following)。

大语言模型在下游任务上的性能，可以通过在指定任务上进行微调(fientune)提升，或者给定少量提示，也叫做few-shot prompt，指令微调是为了让模型能够理解人类指令，在不给出少量提示的情况下，增强模型的zero-shot能力的一种方式，比如，你可以在许多任务上进行指令微调，在其他任务上(unseen, 模型未见过)进行测试，你会发现模型的理解能力有所提升，可以给出更好的答案。

指令微调数据一般如下 {###Insruction:...., ###Input:...., ###Answer:....} 组成，举个例子，问模型1+1等于几， 微调数据就是{###Insruction:在接下来的input中，我给你两个数字，你能够告诉我两个数字的和吗, ###Input: 1，1, ###Answer: 2}。以上就是一条微调数据，当然，你可以更换数据模板，比如不用Input，或者给一些提示(few-shot)，或者在答案中给出CoT, 也就是整个答案的推理过程。

或许你曾经听过FLAN(finetune language net)，这篇论文是谷歌提出Instruction tuning的经典，文章将微调后的模型和175B的GPT-3进行了比较，证明了指令微调的优越性：
https://openreview.net/forum?id=gEZrGCozdqR

同年，谷歌针对CoT(chain of thought，链式思维)和few-shot在Instruction-Tuning中能否提升模型的能力，以及模型大小和数据集大小对指令调优的影响进行了进一步探究，这篇文章用了146种任务，473个数据集，最终确定指令微调任务的多样性可以提升模型的能力, CoT数据可以提升模型的推理能力, 模型规模越大，经过指令微调的效果越好，还没看到上限：
https://doi.org/10.48550/arXiv.2210.11416

近两年指令微调不仅在LLM领域，在多模态领域也是一大热点，经过探究和实验，许多学者认为，指令调优意在对齐模型的内部知识，让模型学会回答，这才是指令调优提升模型能力的重点，所以经过浓缩后的指令调优数据集可能仅有几千条，但是足以提升模型的能力。
 
