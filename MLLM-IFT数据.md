<img width="613" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/b3e4894f-3fc2-41fd-8edc-cae802f4afb2">1、blip_laion_cc_sbu_558k：所有指令均围绕描述一下这张图的内容构造, 指令过于简单，单轮对话，信息量极少。

<br />![图片](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/24e656d8-ac8c-4993-b070-692a953870a7)

2、llava_v1_5_mix665k：多轮对话指令，主要围绕图的内容展开多轮对话，包括图中物体的颜色，位置，以及更困难的图片理解，最后还包括纯文本的问题，多种语言数据。

<br /><img width="922" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/b12e6b3a-2c34-49e8-8d9b-899d1c1d50dc">

3、sharegpt4v_mix665k_cap23k_coco-ap9k_lcs3k_sam9k_div2k：如原文所说，将llava_v1_5_mix665k中的少量数据进行替换，将其中一些多轮对话换成由GPT-4V生成的高质量描述（此为单轮对话，指令格式为详细说明一下图片内容，数据来源为手动收集的多样化的图片），下图为其中替换的数据格式。

<br /><img width="596" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/7b9dcd99-aa7b-4f35-83cf-9a57da443040">

4、SVIT_mix_665K，由llava_v1_5_mix665k演化而来，将其中的LLaVA-Instruct-150K更换为SVIT core-150K，此数据集由纯文本GPT-4生成，但是不给出提示，全部为zero-shot，确保创造力，图片来源为VG。一共四种数据，包括对话，复杂推理，指代和详细描述。对话中很多都是短对话，要求模型使用一个词语或词组进行回答。

<br /><img width="880" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/a78203e2-5801-49c8-b3f2-bc7e8976f50b">

5、textOCR-GPT-4v，使用GPT-4V对图片进行标注，包括两个主要部分，一个是整体描述，一个是图中各个物体的识别。

<br /><img width="907" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/2a339bca-48f2-4059-a5ad-5d668193b4c2">

由此得见，llava_v1_5_mix665K确实是高质量数据，均由其演化而来。

llava_v1_5_mix665K数据去重(0.7)：
| Dataset | Llava_665K | 原始图片数据 | 相似数据 | 过滤后数据 |
| --- | --- | --- | --- | --- |
| coco | 364,100 | 88,524 | 86,359 | 2,165 |
| gqa | 72,140 | 72,140 | 70,214 | 1,926 |
| textvqa | 21,953 | 21,953 | 20,255 | 1,698 |
| VG_100K | 53,343 | 53,343 | 51,779 | 1,564 |
| VG_100K_2 | 33,074 | 33,074 | 31,724 | 1,350 |
| ocr_vqa | 80,000 | 80,000 | 79,328 | 672 |


llava_v1_5_mix665K数据去重(0.8)：
| Dataset | Llava_665K | 原始图片数据 | 相似数据 | 过滤后数据 |
| --- | --- | --- | --- | --- |
| coco | 364,100 | 88,524 | 72811 | 15713 |
| gqa | 72,140 | 72,140 | 58959 | 13181 |
| textvqa | 21,953 | 21,953 | 13693 | 8260 |  
| VG_100K | 53,343 | 53,343 | 42608 | 10735 |
| VG_100K_2 | 33,074 | 33,074 | 25462 | 7612 |
| ocr_vqa | 80,000 | 80,000 | 75104 | 4896 |

coco数据集示例1（id 000000011025 000000020188 score:  0.8043305277824402）： 
<br />
<img width="467" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/facbe905-39c7-4fba-8b73-b4bec5c1fce7">

coco数据集示例1（id 000000479396 000000480196 score:  0.8011465668678284）：
<br />
<img width="593" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/69d26377-c194-4bfb-a815-1f29e1c45e93">

coco数据集示例2（id 000000004289 000000524830 score:  0.8446336984634399）： 
<br />
<img width="409" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/b6973b79-1d63-4a69-a98a-fa3d5c4df596">

coco数据集示例3（id 000000208408 000000483952 score:  0.8500）： 
<br />
<img width="483" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/4dc37ffb-0f95-4218-9a21-94c2617f1c5b">

coco数据集示例4（id 000000154161 000000250926 score:  0.8521636128425598）： 
<br />
<img width="568" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/345bede5-2a55-466c-8989-e217538050ae">

gqa数据集示例1（id 2980 2955 score:  0.8072953820228577）： 
<br />
<img width="563" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/104d8574-816b-4986-b938-146630ccb50c">

gqa数据集示例2（id 2113 2038 score:  0.8028135895729065）： 
<br />
<img width="574" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/50219e45-48ad-4883-ad85-3ab61eff241c">

gqa数据集示例3（id 3003 2955 score:  0.8526859283447266）： 
<br />
<img width="569" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/c3a1624b-87be-4cd3-bc5e-620e9d875819">

gqa数据集示例4（id 2142 2038 score:  0.8534134030342102）：
<br />
<img width="572" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/4e121a23-5295-4d40-b246-c946758ce454">

gqa数据集示例5（id 2361634 2361485 score:  0.8513107895851135）：
<br />
<img width="621" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/8e9cd394-9ae1-42c2-bff0-97948b7ee4c3">

gqa数据集示例6（id 2362277 2361234 score:  0.9193390607833862）：
<br />
<img width="616" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/0c2ab3bc-74be-42ee-912b-4eee68bf0c8e">

gqa数据集示例7（id 2362309 2361271 score:  0.9175586700439453）：
<br />
<img width="613" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/5ce74591-e8da-4273-a195-d79e77fbc782">

gqa数据集示例8（id 2361505 2361249 score:  0.9082695245742798）：
<br />
 <img width="468" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/20fcc59c-8c02-404c-8298-d02d76533f7b">

ocr_vqa数据集示例1（id 471746851 1517562635 score:  0.8029585480690002）： 
<br />
<img width="418" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/30085984-319c-4fa2-9f60-1c6acd0ea18a">

ocr_vqa数据集示例2（id 971828679 1512030104 score:  0.8074419498443604）： 
<br />
<img width="389" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/3bbbc2c3-e06e-415c-9d0c-4b4e32c25596">

ocr_vqa数据集示例3（id 1622664493 1937007014 score:  0.908668041229248）：
<br />
<img width="395" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/abcd13d7-650f-4dd5-b6be-a80a743597b5">

ocr_vqa数据集示例4（id 470194960 1904920845 score:  0.9079761505126953）： 
<br />
<img width="415" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/05304ae9-dad7-460b-88cc-67cfc2adc70f">

ocr_vqa数据集示例5（id 1439528578 807261580 score:  0.9579094648361206）： 
<br />
<img width="401" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/d8df1b8c-4082-40bb-9300-992c37e2d81c">

VG数据集示例1（id 000000377952 000000355609）： 

VG数据集示例2（id 000000117322 000000407671）： 

VG数据集示例3（id 000000476631 000000407671）： 

llava_v1_5_mix665K数据去重(0.9)：
| Dataset | Llava_665K | 原始图片数据 | 相似数据 | 过滤后数据 |
| --- | --- | --- | --- | --- |
| coco | 364,100 | 88,524 | 23002 | 65522 |
| gqa | 72,140 | 72,140 | 18881 | 53259 |
| textvqa | 21,953 | 21,953 | 2905 | 19048 |
| VG_100K | 53,343 | 53,343 | 12604 | 40739 |
| VG_100K_2 | 33,074 | 33,074 | 7179 | 25895 |
| ocr_vqa | 80,000 | 80,000 | 28000 | 52000 |

coco数据集示例1（id 000000377952 000000355609 score:  0.9095）：
<br />
<img width="724" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/ac206f1d-5190-4276-acda-f1397665289b">

coco数据集示例2（id 000000117322 000000407671 score:  0.9115）：
<br />
<img width="614" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/7a3682ff-9397-4918-a867-9fd8ab6704b1">

coco数据集示例3（id 000000476631 000000407671 score:  0.9153）：
<br />
<img width="617" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/e28ede82-789e-4f01-a0cd-489e6bf56e23">

gqa数据集示例1（id 000000377952 000000355609）： 

gqa数据集示例2（id 000000117322 000000407671）： 

gqa数据集示例3（id 000000476631 000000407671）： 


ocr_vqa数据集示例1（id 000000377952 000000355609）： 

ocr_vqa数据集示例2（id 000000117322 000000407671）： 

ocr_vqa数据集示例3（id 000000476631 000000407671）： 

VG数据集示例1（id 000000377952 000000355609）： 

VG数据集示例2（id 000000117322 000000407671）： 

VG数据集示例3（id 000000476631 000000407671）： 
**每列含义：**

- **Llava_665K：** 在Llava_665K微调数据集中共有多少条数据。
- **原始图片数据：** 表示Llava_665K数据集中的图片去重后的总数。
- **相似数据：** 通过Vit模型的class embedding（维度为\[1, 1024\]）计算余弦相似度，找出的可视为重复且阈值设为0.7的数据量。
- **过滤后数据：** 经筛选去除相似度较高数据后，剩余的图片数量。


注：上传的excel表格均是原始数据集每隔500条进行一次采样获得。
