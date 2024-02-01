

## 기본 template-grid-column, row 설정

- 코드펜 출처 : https://codepen.io/anotheryear-hm/pen/xxBYmWj
- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션4 > Grid 핵심정리 #2 - 그리드의 기본형태`

``` bash 
- 문제 상황 
	- 기본 column 과 row 의 개수를 몇 개로 가져갈지에 대해서 
	- '고정' 요소가 있고, '가변' 요소가 있음. 이걸 어떻게 나눠야 할지에 대해서. 
		- 브라우저 너비에 대응해서 '가변적' 인 요소가 있고 
		- 콘텐츠 크기 및 길이에 대응해서 '가변적' 인 요소가 있음. 

- 포인트 
1. 부모 container 의 너비(고정 or 가변) 을 '고정, 가변' 중 어떻게 나누어 가질 것 인가! 에 대한 결정 ⭐⭐⭐
2. '부모 container 의 너비' 가 없으면, 원하는 대로 나눠먹질 않음 ⭐⭐⭐⭐⭐ 
```


``` css
.grid-container {
	padding: 10px;
	background-color: lightgray;
	
	display: grid;

	/* columns */
		/* grid-template-columns: 100px 300px 200px;    */
			/*  컬럼의 너비를 100px, 300px, 200px 으로 정함*/

		/* grid-template-columns: 1fr 1fr 1fr; */
			/* 3개의 컬럼이, 균등한 비율로 가져감 */
			
		/* grid-template-columns: 1fr 2fr 1fr; */
			/* 3개의 컬럼이, 주어진 width를, 1:2:1 의 비율로 가져감 */
		
		/* grid-template-columns: 1fr 500px 1fr; */
			/* 3개의 컬럼중, 가운데는 500px 로 고정, 나머지는 남은 너비를 1:1 로 나눔 
				남은 너비를 나눠먹기 때문에 -> '너비 조정에 대응' 되는 느낌이 남! 
			*/

		/* grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr; */
			/* 주어진 width를, 6개의 컬럼이, 1:1:1:1:1:1 비율로, 나눠먹기 
				[문제] 2번째 row 에서 끝까지 안 채워짐. 📛📛📛 
			*/

		/* grid-template-columns: repeat(6, 1fr); */
			/* grid-template-columns: 1fr 1fr 1fr 1fr 1fr 1fr; 와 동일 */
		
		/* grid-template-columns: repeat(3, 1fr 2fr 1fr); */
			/* 3개의 컬럼이 1:2:1 로 나뉘어짐 | 3개의 컬럼은 계쏙 반복이 됨 📛📛📛 */
			/* 이건 생각보다 조금 다르게 나올 수 있음 📛📛📛 */
		
		grid-template-columns: repeat(3, 1fr);

	/* rows */
		/* grid-template-rows: 200px 200px; */
			/* grid-template-rows: 200px 200px auto; 랑 동일 📛📛📛 ⭐⭐⭐ | auto 의 쓰임 */
			/* 즉, auto 는 콘텐츠가 가진 크기 만큼만 커짐. 현재는 알파벳 크기 만큼만 커지게 됨 📛📛📛  */

		/* grid-template-rows: repeat(3, 1fr 2fr 1fr); */
		/* grid-template-rows: 1fr 2fr 1fr; */
			/* container 의 heigth 가 정해져 있으면 -> 해당 height 를 3개의 row 가 1:2:1 로 나눠가짐 */
		
		grid-template-rows: 1fr 2fr 1fr;

		height: 80vh;

	/* 포인트 
		1. 부모 container 의 너비(고정 or 가변) 을 '고정, 가변' 중 어떻게 나누어 가질 것 인가! 에 대한 결정 ⭐⭐⭐ 

	*/
	}

.grid-item { 
	padding: 10px;
	border: 3px solid rgb(50, 50, 40);
	color: white;
	background: #ff6937;
}
```

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="xxBYmWj" data-user="anotheryear-hm" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/anotheryear-hm/pen/xxBYmWj">
  grid_#1_template grid , row 기본 설정</a> by JeongDeokjin (<a href="https://codepen.io/anotheryear-hm">@anotheryear-hm</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>


![](https://i.imgur.com/WvaETOy.png)


<br>

## [문제 상황] 콘텐츠가 없을 때에도 최소한 100px 씩 유지 and 콘텐츠가 길어지면, 길어진 만큼 늘어나게 하기!  (minmax 사용)

- 코드펜 : https://codepen.io/anotheryear-hm/pen/ExMQrXr
- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션4 > Grid 핵심정리 #3 - 자동으로 채우기`

``` bash 
- 문제 상황 
	- '브라우저 너비 변경' 에 대응할 수도 있고
	- '콘텐츠와 콘테이너의 관계' 에 대응해야 할 수 있음. 

- 콘텐츠에 대응하는 방법 ⭐⭐⭐ 
	1. 글자(content)가, container 보다 작아지는 경우
		- content 는 글자, container 는 content 의 부모 요소가 되는 div 라고 가정 
		- 설령, 글자 수가 너무 작아도, container 가 따라서, 너무 작아지지 않게! 하고 싶으면 -> minmax 사용 가능 
		- 글자수가 작아지면, 작아지는 대로, container 가 따라서 작아지게 하려면 -> auto 로 잡아주면 돼
		- [예시] grid-template-rows: repeat(3, minmax(auto, auto))   ⭐⭐⭐
	
	2. 글자(content)가, container 보다 커 지는 경우 
		- container에 맞추게 하기 
			- 점점점 처리 
		- content 에 맞춰서 container 가 변하기 
			- auto : grid-template-rows: repeat(3, minmax(100px, auto)) ⭐⭐⭐

```

``` css 
.grid-container {
	padding: 10px;
	background-color: lightgray;
	
	display: grid;
		
	grid-template-columns: repeat(3, 1fr);
	
	/* ⭐⭐ 중요 */
	grid-template-rows: repeat(3, minmax(100px, auto))
	/* [콘텐츠 대응] 
	1. 글자(content)가, container 보다 작아지는 경우
		- content 는 글자, container 는 content 의 부모 요소가 되는 div 라고 가정 
		- 설령, 글자 수가 너무 작아도, container 가 따라서, 너무 작아지지 않게! 하고 싶으면 -> minmax 사용 가능 
		- 글자수가 작아지면, 작아지는 대로, container 가 따라서 작아지게 하려면 -> auto 로 잡아주면 돼
			grid-template-rows: repeat(3, minmax(auto, auto))   
	
	2. 글자(content)가, container 보다 커 지는 경우 
		- container에 맞추게 하기 
			- 점점점 처리 
		- content 에 맞춰서 container 가 변하기 
			- auto : grid-template-rows: repeat(3, minmax(100px, auto))
	*/

	}

.grid-item { 
	padding: 10px;
	border: 3px solid rgb(50, 50, 40);
	color: white;
	background: #ff6937;
}
```


![](https://i.imgur.com/SQUO47w.png)


<br>


## [문제 상황] 브라우저 너비에 따라 column 개수는 변화하되, 각 column 이 최소한 200px 되어야 하는 경우 (auto-fill 사용) | ⭐ 반응형으로 응용이 가능함 ⭐ 

- 코드펜 링크 : https://codepen.io/anotheryear-hm/pen/YzgapMq
- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션4 > Grid 핵심정리 #3 - 자동으로 채우기`

``` css
.grid-container {
	padding: 10px;
	background-color: lightgray;
	
	display: grid;    
		/* grid-template-columns: repeat(auto-fill, minmax(20%, auto)); */
		/* [해석]
			auto-fill : 개수는 자동으로 채워줘 (아마도, 전체를 20% 로 쪼개서 해달라고 했으니, 5개가 생길 것)
			minmax(20%, auto) : 1) 컬럼의 최소너비는 전체 너비의 20% 로 해줘 2) 최대는 자동으로  
			
			[해결하는 문제]
			브라우저의 너비에 따라서 -> 컬럼의 개수는 유지 하면서, 컬럼의 너비를 대응하게 하고 싶을 때 사용 가능                
		*/

	grid-template-columns: repeat(auto-fill, minmax(200px, auto));
		/* [해결하고 싶은 문제] 
			브라우저 너비가 이동하면, 알아서, 동일한 크기의 column 이, 개수가 줄어들었으면

			[브라우저 너비 변화 대응]
				1. 좁아지는 경우
					- 각 column 은, 최소한 200px 의 너비를 확보한다. 
					- 남은 공간을 max 계산에 쓴다. -> [⭐contents 대응] 각 content 의 크기별로, width 를 주려고 하는데, 200px 로 남은 나머지를 쓰는 느낌이라, 매우 커지지는 않는 것 같음 
					- 변화되는 것은, column 의 개수가 줄어든다. 
				2. 넓어지는 경우 
					- 주어진 너비에서, 최소한의 200px 을 최대만 많이 확보 
					- 그 남은 공간을 contents 의 auto 계산으로 쓴다. (이때, contents 대응⭐ 이 된다.)
					- 변화되는 것은, column 의 개수가 늘어난다. 
		*/

	grid-template-rows: repeat(3, minmax(100px, auto))
	/* [콘텐츠 대응] 
		1. 글자(content)가, container 보다 작아지는 경우
			- content 는 글자, container 는 content 의 부모 요소가 되는 div 라고 가정 
			- 설령, 글자 수가 너무 작아도, container 가 따라서, 너무 작아지지 않게! 하고 싶으면 -> minmax 사용 가능 
			- 글자수가 작아지면, 작아지는 대로, container 가 따라서 작아지게 하려면 -> auto 로 잡아주면 돼
				grid-template-rows: repeat(3, minmax(auto, auto))   
		
		2. 글자(content)가, container 보다 커 지는 경우 
			- container에 맞추게 하기 
				- 점점점 처리 
			- content 에 맞춰서 container 가 변하기 
				- auto : grid-template-rows: repeat(3, minmax(100px, auto))
	*/

	}

.grid-item { 
	padding: 10px;
	border: 3px solid rgb(50, 50, 40);
	color: white;
	background: #ff6937;
}
```

- 좁은 브라우저의 경우 
![](https://i.imgur.com/8Nzwdnw.png)


- 넓은 width 의 경우 
![](https://i.imgur.com/Ge3gAZn.png)


<br>

### 다른 경우 : 브라우저 너비 변경에 따라, column 개수는 동일하되, 각 column 이 차지하는 영역이 달라지게 하고 싶은 경우   
- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션4 > Grid 핵심정리 #3 - 자동으로 채우기`

``` css
.grid-container {
	padding: 10px;
	background-color: lightgray;
	
	display: grid;    

	/* ⭐⭐⭐ 각 column을 20% 으로 설정하면, 각 column 좀 더 균등하게 설정됨 ⭐⭐⭐ */
	grid-template-columns: repeat(auto-fill, minmax(20%, auto));

	grid-template-rows: repeat(3, minmax(100px, auto))
	}
```

- 브라우저 너비가 좁은 경우 
![](https://i.imgur.com/vq8OJ3D.png)


- 브라우저 너비가 긴 경우 
![](https://i.imgur.com/2SSeLwp.png)


<br>


### [문제 상황] 
- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션4 > Grid 핵심정리 #3 - 자동으로 채우기`

- 문제 상황 
``` 
grid-template-columns: repeat(auto-fill, minmax(100px, auto)); 로 설정하여, 
각 column 이 100px 씩 되게 설정함. 

문제는, 각 column 에 할당하고, 빈 공간이 생기게 됨 
```

![](https://i.imgur.com/4gYeQqJ.png)


- 해결 
``` css 
/* 'auto-fit' 을 사용함. -> 그러면, 주어진 컬럼의 너비로 남은 공간을 채움  */

.grid-container {
	padding: 10px;
	background-color: lightgray;
	
	display: grid;    

	/* ⭐⭐⭐ 각 column을 20% 으로 설정하면, 각 column 좀 더 균등하게 설정됨 ⭐⭐⭐ */
	grid-template-columns: repeat(auto-fill, minmax(20%, auto));

	grid-template-rows: repeat(3, minmax(100px, auto))
	}

```


- 빈 공간이 채워지는 원리 
``` bash 
누가, 어떻게 채워? 

1. 콘텐츠가 있으면 -> max 값으로 설정한 contents 가 먹게 되었음. 
2. 콘텐츠가 없으면 -> 각 column 이 균등하게 채움
```

1) 콘텐츠가 있어서 -> 남은 공간을 콘텐츠가 균등하게 먹은 경우
![](https://i.imgur.com/6LDvX4v.png)


2) 콘텐츠가 없어서 -> 기존이 컬럼들이 균등하게 먹은 경우 
![](https://i.imgur.com/IqwRfT6.png)

(출처 : 1분 코딩, flex&grid)









---

## 알아두면 좋은 것 


### 브라우저 너비를 줄여서 -> 사진 콘텐츠가 컨테이너 보다 큰 경우 -> 사진 콘텐츠를 컨테이너에 딱 맞게 하려면

``` bash 
- 문제 상황 
	- 브라우저 너비 변화에 따라서 -> 컨테이너가 축소되고 -> 그에 따라, 컨테이너 vs 컨텐츠 간 갈등이 생김 
	- 어떻게 하면, 딱 그 부분에서 컨텐츠가 컨테이너를 넘지 않으면서, 딱 붙게 만들 수 있을까. 

- 해결 
	- maxWidth 를 사용 

- 시사점 
	- 일반 css 이지만, 해결 방식이 중요해서 적음 
```

[[5. githubSync_gitBook/05_개발 언어/HTML&CSS/HTML5 + CSS3 웹 표준의 정석/요약#^9032fb| maxWidth 사용 ]]

