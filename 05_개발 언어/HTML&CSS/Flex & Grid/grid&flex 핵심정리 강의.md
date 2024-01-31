

## 기본 template-grid-column, row 설정
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

- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션4 > Grid 핵심정리 #2 - 그리드의 기본형태`
- codepen 에 다양한 설정값들이 있음. 

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="xxBYmWj" data-user="anotheryear-hm" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/anotheryear-hm/pen/xxBYmWj">
  grid_#1_template grid , row 기본 설정</a> by JeongDeokjin (<a href="https://codepen.io/anotheryear-hm">@anotheryear-hm</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>


![](https://i.imgur.com/WvaETOy.png)


<br>

## [문제 상황] 콘텐츠가 없을 때에도 최소한 100px 씩 유지 and 콘텐츠가 길어지면, 길어진 만큼 늘어나게 하기!  

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

<p class="codepen" data-height="300" data-default-tab="html,result" data-slug-hash="ExMQrXr" data-user="anotheryear-hm" style="height: 300px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;">
  <span>See the Pen <a href="https://codepen.io/anotheryear-hm/pen/ExMQrXr">
  grid_#2_minmax_글자수가 적어도 100px 맞추기 &amp; 글자수가 커지면, 글자수에 맞게 늘어나게 하기</a> by JeongDeokjin (<a href="https://codepen.io/anotheryear-hm">@anotheryear-hm</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://cpwebassets.codepen.io/assets/embed/ei.js"></script>

![](https://i.imgur.com/SQUO47w.png)


<br>






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

