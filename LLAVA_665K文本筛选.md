## 文本数据去重（提取有效信息，使用gte_Qwen1_5-7B-instruct计算文本相似度）

<br /> 

llava_v1_5_mix665K数据去重(0.8)：
| Dataset | 原始数据 | 过滤数据 | 过滤后数据 | 过滤百分比 |
| --- | --- | --- | --- | --- |
| coco | 364100 |  162701   | 201399   | 44.6  | 
| gqa | 72,140 |  27993 | 44147  | 38.8  | 
| ocr_vqa | 80000  |  34926 | 45074   | 43.66  | 
| text_vqa | 21953  |  5660 | 16293   | 25.78  | 
| VG_100K | 53343  |  35918 | 17425  | 67.33  | 
| VG_100K_2 | 33074  |  20266 | 12808   | 61.27  | 

<br />

llava_v1_5_mix665K数据去重(0.85)：
| Dataset | 原始数据 | 过滤数据 | 过滤后数据 | 过滤百分比 |
| --- | --- | --- | --- | --- |
| coco | 364100 |  100946 | 263154   | 27.7  | 
| gqa | 72,140 |  7042 | 65098   | 9.76  | 
| ocr_vqa | 80000  |  15402 | 64598    | 19.25  | 
| text_vqa | 21953  |  1721 | 20232    | 7.84  | 
| VG_100K | 53343  |  12942 | 40401  | 24.26  | 
| VG_100K_2 | 33074  |  6256 | 26818  | 18.92  | 


<br />

llava_v1_5_mix665K数据去重(0.90)：
| Dataset | 原始数据 | 过滤数据 | 过滤后数据 | 过滤百分比 |
| --- | --- | --- | --- | --- |
| coco | 364100 |  60987    | 303113    | 16.7  | 
| gqa | 72,140 |  1661  | 70479    | 2.3  | 
| ocr_vqa | 80000  |  5586 | 74414     | 6.98  | 
| text_vqa | 21953  |  246 | 21707    | 1.12  | 
| VG_100K | 53343  |  1047 | 52296   | 1.96  | 
| VG_100K_2 | 33074  |  327 | 32747   | 0.99  | 


<br />
coco数据集示例1（id 177505 566237 score:  0.80）：
<br />
<img width="556" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/9f6c54c7-981f-4958-81df-c70f516a4590">

<br />
coco数据集示例2（id 189983 398713 score:  0.81）：
<br />
<img width="509" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/67b10d4e-89a4-4fe9-940c-f2f3adde81d3">

<br />
coco数据集示例3（id 306178 282998 score:  0.82）：
<br />
<img width="513" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/d3ec870e-b080-40cf-aade-848e583a5e3f">


<br />
coco数据集示例4（id 297969 525405 score:  0.85）：
<br />
<img width="583" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/9b247ade-d63f-4fc6-b4c3-cbe22e5055c4">


<br />
coco数据集示例5（id 137690 418173 score:  0.86）：
<br />
<img width="559" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/53df487c-e9af-4c7c-b89c-0eaeda3e9e55">

<br />
coco数据集示例6（id 257669 318594 score:  0.90）：
<br />
<img width="547" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/f1e51f4a-efb4-4b5f-9a07-df670517e826">

<br />
coco数据集示例7（id 532419 361119 score:  0.91）：
<br />
<img width="559" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/633003a8-3020-42d1-9229-578fa3b6e4dc">


 gqa数据集示例1（id 4862 4812 score:  0.85）： 
<br />
<img width="478" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/4b28f6c6-14f1-4089-a783-b433fa689a4b">
<br />
<img width="467" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/d2fa2d37-8bcc-4869-b885-e85104ab4db6">
<br />
<img width="615" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/faf8c838-4611-4a04-8f45-05b7d0f1db54">

<br />
 gqa数据集示例2（id 1668 9 score:  0.80）： 
<br />
<img width="623" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/9b25c5af-7dc7-4a19-bbd6-120c63f6d202">



<br />
 gqa数据集示例3（id 1515 9 score:  0.81）： 
<br />
<img width="617" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/680b72e2-bb91-47fc-b4c9-1d8049b380d5">


<br />
VG数据集示例1（id VG_100K_2/2409256 VG_100K_2/2379584 score:  0.87）： 
<br />
<img width="594" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/782a3339-17d6-4152-b457-561812b1ac77">



<br />
VG数据集示例2（id VG_100K_2/2384651 VG_100K_2/2411289 score:  0.86）： 
<br />
<img width="641" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/5e5b7f4f-d284-487f-b2a4-220e2f12debd">


<br />
VG数据集示例3（id VG_100K/2360667 VG_100K/2340039 score:  0.81）： 
<br />
<img width="605" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/85b6fdda-4532-4b27-80ff-ded55bb2a047">


<br />
VG数据集示例4（id VG_100K/2361161 VG_100K/2353803 score:  0.85）： 
<br />
<img width="619" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/e3e04da5-9e36-45a4-b536-829f7481ceb4">



<br />
VG数据集示例5（ id VG_100K/2361999 VG_100K/1159979 score:  0.85）： 
<br />
<img width="600" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/2c170573-a9e4-479e-9378-0b472c9af54f">


<br />
VG数据集示例6（id VG_100K/2341788 VG_100K/2319322 score:  0.85）： 
<br />
<img width="628" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/4630d738-2643-43a8-be70-e0e7c4dceb0f">


<br />
ocr_vqa数据集示例1（id 91939690 1511924772 score:  0.85）： 
<br />
<img width="468" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/af8556b7-9100-48b6-b105-5685f74bf798">
<br />
<img width="495" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/5d083d1b-8a91-470b-a195-2c252b88d5b3">


<br />
ocr_vqa数据集示例2（id 1517282969 1517464560 score:  0.87）： 
<br />
<img width="464" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/44d7ceb2-c674-41e0-ac00-c2451ab15bf4">
<br />
<img width="501" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/86600453-9f17-4933-81a4-16806203c2a4">


<br />
ocr_vqa数据集示例3（id 1935707833 098417804X score:  0.86）： 
<br />
<img width="468" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/7970d76b-7cfe-429c-9853-1762d46d3296">
<br />
<img width="566" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/9ba0de5a-e08b-4665-a076-77e7be9d27a7">



<br />
ocr_vqa数据集示例4（id 310745640 310339553 score:  0.92）： 
<br />
<img width="475" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/28d6cd75-c669-4be7-a3af-5aa5cad796b5">

<img width="498" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/888ecd0b-d77e-41e8-bb12-de2572a46760">

