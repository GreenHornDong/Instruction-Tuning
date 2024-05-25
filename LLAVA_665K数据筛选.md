## 图片数据去重
<br />
llava_v1_5_mix665K数据去重(0.7)：

| Dataset | Llava_665K | 原始图片数据 | 过滤数据 | 过滤后数据 | 过滤百分比 |
| --- | --- | --- | --- | --- | --- |
| coco | 364,100 | 88,524 | 86,359 | 2,165 | 97.6 |
| gqa | 72,140 | 72,140 | 70,214 | 1,926 | 97.3 |
| textvqa | 21,953 | 21,953 | 20,255 | 1,698 | 92.3 |
| VG_100K | 53,343 | 53,343 | 51,779 | 1,564 | 97.1 |
| VG_100K_2 | 33,074 | 33,074 | 31,724 | 1,350 | 95.9 |
| ocr_vqa | 80,000 | 80,000 | 79,328 | 672 | 99.2 |


<br />

llava_v1_5_mix665K数据去重(0.8)：

| Dataset | Llava_665K | 原始图片数据 | 过滤数据 | 过滤后数据 | 过滤百分比 |
| --- | --- | --- | --- | --- | --- |
| coco | 364,100 | 88,524 | 72811 | 15713 | 82.3 |
| gqa | 72,140 | 72,140 | 58959 | 13181 | 81.7 |
| textvqa | 21,953 | 21,953 | 13693 | 8260 | 62.4 | 
| VG_100K | 53,343 | 53,343 | 42608 | 10735 | 79.9 |
| VG_100K_2 | 33,074 | 33,074 | 25462 | 7612 | 77.0 |
| ocr_vqa | 80,000 | 80,000 | 75104 | 4896 | 93.9 |
 
<br />

llava_v1_5_mix665K数据去重(0.9)：
| Dataset | Llava_665K | 原始图片数据 | 过滤数据 | 过滤后数据 | 过滤百分比 |
| --- | --- | --- | --- | --- | --- |
| coco | 364,100 | 88,524 | 23002 | 65522 | 26.0 |
| gqa | 72,140 | 72,140 | 18881 | 53259 | 26.2 |
| textvqa | 21,953 | 21,953 | 2905 | 19048 | 13.2 |
| VG_100K | 53,343 | 53,343 | 12604 | 40739 | 23.6 |
| VG_100K_2 | 33,074 | 33,074 | 7179 | 25895 | 21.7 |
| ocr_vqa | 80,000 | 80,000 | 28000 | 52000 | 35.0 |
 


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

coco数据集示例5（id 000000377952 000000355609 score:  0.9095）：
<br />
<img width="724" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/ac206f1d-5190-4276-acda-f1397665289b">

coco数据集示例6（id 000000117322 000000407671 score:  0.9115）：
<br />
<img width="614" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/7a3682ff-9397-4918-a867-9fd8ab6704b1">

coco数据集示例7（id 000000476631 000000407671 score:  0.9153）：
<br />
<img width="617" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/e28ede82-789e-4f01-a0cd-489e6bf56e23">

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

textvqa数据集示例1（id 65f8b6e8a671ce9c 6f36f021e7dbf722 score:  0.8064557313919067）： 
<br />
<img width="382" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/3f48218d-3c5f-451e-8603-9a806c9c7f87">

textvqa数据集示例2（id 001f5618a7b33d88 4a61c62dc0b25a12 score:  0.8020707964897156）： 
<br />
<img width="397" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/8bfcc153-2017-4c01-af89-aa5f9b7b9fe4">

textvqa数据集示例3（id e7591dd27c5e002d 6dfda26ea4770ee3 score:  0.8508110642433167）： 
<br />
<img width="608" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/db6a99ac-82b5-4c8e-8567-eea6109e362a">

textvqa数据集示例4（id fad029f706716955 03070b053c750a30 score:  0.9065784811973572）：
<br />
<img width="406" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/bb9b7107-11e9-4098-aae1-12f90ebe71ce">

textvqa数据集示例5（id 3f0ce1ded7dd197c 2d7814cdb42c9562 score:  0.958331823348999）：
<br />
<img width="604" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/433ec36f-df3d-4e78-abed-342ee8874329">

VG数据集示例1（id VG_100K/2368639 VG_100K/2329484 score:  0.8029422760009766）： 
<br />
<img width="596" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/9ecb1566-84c2-4fc9-a69b-82bbd8a0f2f8">

VG数据集示例2（id VG_100K/2344834 VG_100K/2333811 score:  0.8088762760162354）： 
<br />
<img width="563" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/d3df2d6d-d80e-45c1-9dad-2d2be24e785a">

VG数据集示例3（id VG_100K/2321237 VG_100K/61571 score:  0.850286066532135）： 
<br />
<img width="577" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/6f975307-044e-4c7c-bb43-f197240a1061">

VG数据集示例4（id VG_100K/2374048 VG_100K/2376414 score:  0.8553512096405029）：
<br />
<img width="428" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/143bfd9d-14db-4f2f-9566-abc532f98da3">

VG数据集示例5（id VG_100K/2320416 VG_100K/2369526 score:  0.8591662645339966）：
<br />
<img width="614" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/86fc5c62-070e-492a-b1e7-e33059b09a85">

VG数据集示例6（id VG_100K_2/2380238 VG_100K_2/2383683 score:  0.855143666267395）：
<br />
<img width="579" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/f0b56755-157f-430e-ab3e-82ef9a8f2d64">

VG数据集示例7（id VG_100K_2/2386906 VG_100K_2/2385350 score:  0.9020364880561829）：
<br />
<img width="605" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/c22cad17-2930-429e-b7a3-58f3f617fba1">

VG数据集示例8（id VG_100K_2/2388547 VG_100K_2/2383709 score:  0.9091617465019226）：
<br />
<img width="398" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/58f589b9-830f-4b44-95b6-1742975051e2">
<br />
**每列含义：**

- **Llava_665K：** 在Llava_665K微调数据集中共有多少条数据。
- **原始图片数据：** 表示Llava_665K数据集中的图片去重后的总数。
- **过滤数据：** 通过Vit模型的class embedding（维度为\[1, 1024\]）计算余弦相似度，找出的可视为重复且阈值设为0.7的数据量。
- **过滤后数据：** 经筛选去除相似度较高数据后，剩余的图片数量。

<br /> 


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
| coco | 364100 |  100946   | 263154   | 27.7  | 
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
<img width="547" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/6b623319-4c61-4962-9203-f08fd6446d9d">


<br />
coco数据集示例5（id 137690 418173 score:  0.86）：
<br />

<img width="547" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/1ca87024-9fe6-416c-8818-7958ae870d5f">


<br />
coco数据集示例6（id 257669 318594 score:  0.90）：
<br />
<img width="547" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/f1e51f4a-efb4-4b5f-9a07-df670517e826">



 gqa数据集示例1（id 4862 4812 score:  0.85）： 
<br />
<img width="478" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/4b28f6c6-14f1-4089-a783-b433fa689a4b">

<img width="467" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/d2fa2d37-8bcc-4869-b885-e85104ab4db6">

![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/146d10a7-df33-4ba8-b553-52fc15b0b78e)

<br />
 gqa数据集示例2（id 1668 9 score:  0.80）： 
<br />
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/9a6fc4cc-fc8d-42cf-9190-6bf78bc61ea3)


<br />
 gqa数据集示例3（id 1515 9 score:  0.81）： 
<br />
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/97cef116-6933-4f35-be85-6ececd69f85c)

<br />
VG数据集示例1（id VG_100K_2/2409256 VG_100K_2/2379584 score:  0.87）： 
<br />
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/419b431f-2eb1-4883-8d84-39de940d7d1a)


<br />
VG数据集示例2（id VG_100K_2/2384651 VG_100K_2/2411289 score:  0.86）： 
<br />
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/3a426de3-cc6b-4987-a6dd-92519206aaf7)

<br />
VG数据集示例3（id VG_100K/2360667 VG_100K/2340039 score:  0.81）： 
<br />
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/331cb345-cb0c-4d24-a090-5f1109f2042a)

<br />
VG数据集示例4（id VG_100K/2361161 VG_100K/2353803 score:  0.85）： 
<br />
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/faf60476-7cca-4e94-a959-4d35f42d45ce)


<br />
VG数据集示例5（ id VG_100K/2361999 VG_100K/1159979 score:  0.85）： 
<br />
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/f66ff5ec-1abb-4875-95aa-473fc3be60fb)

<br />
VG数据集示例6（id VG_100K/2341788 VG_100K/2319322 score:  0.85）： 
<br />
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/218110bc-2432-4661-979d-3349c24cc4a1)

<br />
ocr_vqa数据集示例1（id 91939690 1511924772 score:  0.85）： 
<br />
<img width="468" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/af8556b7-9100-48b6-b105-5685f74bf798">

![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/a1fc1a68-663f-4241-a885-04c01948b304)

<br />
ocr_vqa数据集示例2（id 1517282969 1517464560 score:  0.87）： 
<br />
<img width="464" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/44d7ceb2-c674-41e0-ac00-c2451ab15bf4">

![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/478f6306-c0dc-45ea-8790-fdde5f0e6c63)

<br />
ocr_vqa数据集示例3（id 1935707833 098417804X score:  0.86）： 
<br />
<img width="468" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/7970d76b-7cfe-429c-9853-1762d46d3296">
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/8f5e333b-657b-408a-8629-df36716bab45)


<br />
ocr_vqa数据集示例4（id 310745640 310339553 score:  0.92）： 
<br />
<img width="475" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/28d6cd75-c669-4be7-a3af-5aa5cad796b5">
![image](https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/98e22225-c2ba-4d59-aa1f-947e3a3bff08)

