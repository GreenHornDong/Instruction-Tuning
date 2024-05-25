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
<img width="583" alt="image" src="https://github.com/GreenHornDong/Instruction-Tuning/assets/101792419/9b247ade-d63f-4fc6-b4c3-cbe22e5055c4">


<br />
coco数据集示例5（id 137690 418173 score:  0.86）：
<br />

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
