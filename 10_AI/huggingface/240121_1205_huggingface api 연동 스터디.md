
- 출처 : https://youtu.be/z41vJlPMqnE

- js 독스 
	- https://huggingface.co/docs/transformers.js/index


---






### 토큰 만들기 

![](https://i.imgur.com/N4eCmGc.png)


<br>

# 프로젝트 셋팅 

## 1. 프론트 
- npx create-react-app front
[[5. githubSync_gitBook/12_KGA_웹개발 블록체인 교육과정/KGA_10월(blockchain, next, ts, tailwind)/231013_토이프로젝트_피카츄 응용해서 상품 페이지 ⭐⭐⭐⭐⭐#^4b04b6]]





## 2. 백엔드 
[[5. githubSync_gitBook/12_KGA_웹개발 블록체인 교육과정/KGA_10월(blockchain, next, ts, tailwind)/231013_토이프로젝트_피카츄 응용해서 상품 페이지 ⭐⭐⭐⭐⭐#^1a57ab]]

- 설치 리스트 
``` bash 
- express, dotenv 
- huggingface/inference

```




# huggingface 연결 

- docs 주소 : https://huggingface.co/docs/huggingface.js/index#from-npm

<br>

## 1. 필요 라이브러리 설치 및 환경변수 설정
- 터미널 설치 
``` bash 
# huggingface/inference
npm install @huggingface/inference
	# 첫 번째 튜토리얼에서는 이걸 설치 
	# 다 설치해야 하는지는 모르겠음. 

	# 이번 튜토리얼에서는 안 했지만, 공식 문서에는 나와있음. 
		# npm install @huggingface/hub
		# npm install @huggingface/agent

# dotenv
	npm install dotenv 
```


- .env
``` bash 
# 발급받은 토큰 붙여넣기
HF_ACCESS_TOKEN=hf_GJXBfGrgAiGpYGrRScVZDbKW 
```

- app.js 
``` js
// 라이브러리 
import { HfInference } from '@huggingface/inference'; // npm install @huggingface/inference
import dotenv from "dotenv"

dotenv.config()

// api key 
const HF_ACCESS_TOKEN = process.env.HF_ACCESS_TOKEN

// initialize hugging face inferance class 
const inferance = new HfInference(HF_ACCESS_TOKEN)


// 서버 설정
const express = require('express')
const app = express()
const PORT = 7070;

app.listen( PORT, () => {
    console.log("서버 열림")
} )
```


<br>

## 2. 모델 설정

1) 모델 찾기 
```
- https://huggingface.co/models?pipeline_tag=image-to-text&sort=trending

- point 
	- 다운로드 횟수 = 검증이 많이 되었다는 의미 
```

![](https://i.imgur.com/Iybz40a.png)


<br>

2) 코드에서 설정해주기  
``` js 
// 모델 이름 복사 -> 매개변수에 넣어주기 
const model = "nlpconnect/vit-gpt2-image-captioning"
```
![](https://i.imgur.com/8NfHRnO.png)



## 3. 코드 작성 
```bash 
- 해야 하는 것 
	- imageToText 메소드가 필요로 하는 데이터 형식에 맞춰서 '요청' 을 보내야 함. 

- 세부 Task
	- fetch : 해당 url 의 이미지를 가져오는 메소드 
	- blob : 대용량 2진 데이터 처리 할 때 사용 
```

- 세부 코드 
``` js 
// 라이브러리 
import { HfInference } from '@huggingface/inference'; // npm install @huggingface/inference
import dotenv from "dotenv"
import fetch from 'node-fetch';   // npm install node-fetch
globalThis.fetch = fetch;
import express from 'express'

const app = express()
dotenv.config()

// api key 
const HF_ACCESS_TOKEN = process.env.HF_ACCESS_TOKEN

// initialize hugging face inferance class 
const inferance = new HfInference(HF_ACCESS_TOKEN)

// define model 
const model = "nlpconnect/vit-gpt2-image-captioning" 
const imageUrl = "https://imgnews.pstatic.net/image/055/2024/01/21/0001124429_005_20240121113601356.png?type=w647"

// fetch this image as a Blob 
const response = await fetch(imageUrl); 
    // [궁금증] 왜 fetch 로 하지? 
    // [궁금증] 저기 예제에 나와있는 거랑, 이거랑, 다른 건가? 왜 다르지?  

const imageBlob = await response.blob()
    // [궁금증] blob 이란게 뭐지? blob 으로 변경해야, 가능한건가? 이런 파일 변경 같은 부분 음... 

// Use the imageToText function to get the iamge caption
const result = await inferance.imageToText({
    data : imageBlob, 
        // [궁금증] 여기에서 imageBlob 값을 가져올 수 있는 이유는, 스코프 체인을 통해, 상위 스코프에 접근할 수 있기 때문?
    model : model
})

// log the result
console.log(result)
```


<br>
## 생각해볼 점 
``` bash 
1. blob, fetch 같은 방식을 쓰는 건 어디에 나와있을까? 

- 해당 페이지에서 js api 연동 예시를 봐도 안 나오는데? (https://huggingface.co/nlpconnect/vit-gpt2-image-captioning?inference_api=true) 

- huggingface.js 에서 use the inference api 예시 활용 (https://huggingface.co/docs/huggingface.js/inference/README)


```


<br>
# image to 3d 테스트 



```
stable diffusion 이 조금 더 나은 모델이긴 함. 
```














