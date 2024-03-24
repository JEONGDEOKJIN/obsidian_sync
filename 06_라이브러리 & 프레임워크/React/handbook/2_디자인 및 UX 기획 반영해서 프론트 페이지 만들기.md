
# 페이지 UX,UI 기획 
- 간단한 피그마 기획 메모 : https://bit.ly/4bBs7Pb

![[[240216] 포트폴리오 개정_아키텍처 및 구조도 (2).png]]

<br>

# `itemList` 페이지 만들기 


## 알게 된 점 
### 1. chatbox 를 만들 때 a) div 를 안정적으로 쌓아가고 2) 위에 header 의 height 를 잡고 3) 그걸 빼서 height 로 잡는다. 4) fixed 를 주는 div 의 위치도 ⭐⭐⭐ (📛 다시 만들어보면 좋을 것 같음)






## 자주 만나게 되는 에러 

### 1. 스크롤바를 포함해서 너비를 잡는 경우 
``` bash 
- `width : 100vw` 를 주게 되면, 일반 div 를 해도 -> 스크롤바를 포함! 해서 너비를 잡게 된다 
 
- 이를 해결하기 위해 
	- .element {
		  width: 100%;
		}

	- @media (min-width: 1024px) {
	  .element {
	    width: 100vw;
	  }
	}

사용한다. 

```


![](https://i.imgur.com/nOjaPJx.png)





