
# 리소스 

- 유튜브 링크 : https://youtu.be/qYgogv4R8zg?si=WkMTvv3pYazVwtxP

- [번역] Tailwind CSS에서 혼란을 방지하기 위한 5가지 모범 사례 ⭐⭐⭐⭐⭐⭐ 
	- https://velog.io/@lky5697/5-best-practices-for-preventing-chaos-in-tailwind-css

- tailwind 프로젝트 관리 페이지 
	- https://www.notion.so/STO-3f0ff1027f164bab89aceb6638bb005e?pvs=4




# [tailwind 공식 문서  공부] 

## 1. tailwind 의 Core Concepts

### 1) Utility-First Fundamentals
- 출처 : https://tailwindcss.com/docs/utility-first

``` bash
tailwind 는 "'원시적인 utilities' 를 합쳐서 -> 'complex components' 를 만든다." 라는 특징이 있다. 
이것은, 'With Tailwind, you style elements by applying pre-existing classes directly in your HTML.' 이런 의미 와도 닿아 있다. 

여기에 있는 키워드들을 조합해서 생각해보면 

- 'pre-existing classes' 이란, '특정 class' 에 '특정 스타일' 을 적용해 놨다! 라는 의미. 
- 'utility' 란, 사전에 미리 정의된 '특정 class에 대응하는 특정 css 한 세트' 를 의미. 
- 'directly in your HTML' 란, 사전에 정의된 class 를 변경하면 -> 그에 따라 CSS 가 변경되고 -> HTML 에 바로 적용이 된다. 

이러한 특징을 종합하면, 'custom component design' 을 할 수 있게 된다. (This approach allows us to implement a completely custom component design without writing a single line of custom CSS.) 

즉, '컴포넌트 디자인' 이라는 키워드가 나온다. 
그 작은 부분, 부분을 디자인 한다는 측면에서, 새롭다. 


그러면, 이렇게 'utility 조합' 을 통해 '컴포넌트 디자인' 을 하면 좋은점은? 
1. '클래스 이름 작명' 에서 자유로워 진다. 
2. 'CSS 파일 크기' 가 제한된다. 
3. 'CSS is global' VS 'Classes in your HTML are local'
	/* styles.css */
	.btn {
	  background-color: blue;
	  color: white;
	}
	
	/* 변경하려면 전역 CSS 파일을 수정해야 함 */
	.btn {
	  background-color: red; /* 모든 .btn 클래스를 사용하는 요소가 영향을 받음 */
	}

	즉, btn 을 변경하면 -> 하나의 btn 만 변경되는게 아니라, 모든 btn 이 변경됨. 내가 원하는 것만 변경되지 않을 수가 있다는 것. 
```

- 이 파일을 뜯어보면, 자동적으로 적용 됨
![](https://i.imgur.com/CGEZcCj.png)




- inline styles 와 비교한 특장점 
``` bash
1. Designing with constraints
	- inline style 에 적용되는 값은 'magic number' (무한대로 들어감)
	- utilities 를 사용하면, 'predefined value' 를 사용

2. 'media query' 를 사용해서, 'responsive design(반응형 디자인)' 이 가능 

3. 'state variants'
	- ex) hover, focus 등이 가능

```




- hover 예제 연습해보기 
``` html 
<div class="py-8 px-8 max-w-sm mx-auto bg-white rounded-xl shadow-lg space-y-2 sm:py-4 sm:flex sm:items-center sm:space-y-0 sm:space-x-6">
  <img class="block mx-auto h-24 rounded-full sm:mx-0 sm:shrink-0" src="/img/erin-lindford.jpg" alt="Woman's Face" />
  <div class="text-center space-y-2 sm:text-left">
    <div class="space-y-0.5">
      <p class="text-lg text-black font-semibold">
        Erin Lindford
      </p>
      <p class="text-slate-500 font-medium">
        Product Engineer
      </p>
    </div>
    <button class="px-4 py-1 text-sm text-purple-600 font-semibold rounded-full border border-purple-200 hover:text-white hover:bg-purple-600 hover:border-transparent focus:outline-none focus:ring-2 focus:ring-purple-600 focus:ring-offset-2">Message</button>
  </div>
</div>
```


### 2) 








---

- 공식 영상 강의 👇👇👇 


# # 01: Setting Up Tailwind CSS v2.0 – Tailwind CSS v2.0: From Zero to Production


### tailwind 의 핵심  포인트 

1. tailwind 'utility class' is work 
``` bash
- 'compose together', 
- 'small single purpose' "classes" to achieve a desired look

```


### 궁금한 것 
2. post css 의 역할은? 


post css 를 쓴다는 것 
즉, auto prefixer that adds vendor prefixes to your css 






---




# grid 학습 

### 리소스 
- 인프런 grid 강의 
- 1분 코딩 블로그 : https://studiomeal.com/archives/533



## grid 내용 정리 
- 그러면, 그리드를 이렇게 쪼개줘도 될 거 같음 
	- 그리고, 가운데 부분에서, 본문 내용 적어주고 
``` bash
[키워드 정리]
		[1 row]
		- 1 row , 윗 부분 = '고정'
		
		[2row]
		- 첫 번째 = 'side bar 에 맞게 고정' | side bar 만 가리면 될 듯 
		- 두 번째 = '변화 가능' | 가운데 content 가 늘어나면 여기도 줄어들거 같음
		- 세 번째 = content 영역 | 여기는 table 이랑, 제목이 쭉 나열되는 곳 | '내용에 맞게 변화 가능⭐⭐⭐' 으로 해보자 
		- 네 번째 = '변화 가능'
		
		[쓸 수 있는 것]
		- '변화 가능' 하다면 fr 
		- repeat 함수
		- minmax (최소 100px 은 잡고, 늘어나는 건 auto!)
		- auto fit , auto fill 
			- 테이블 안에 있는 영역들을 잡을 때, auto fill 같은 것도 쓸 수 있을거 같은데 | 이건 minor 함 ⭐⭐ | 
			- 개수가 모자랄 때 채우냐, 남겨두냐 차이
			- 미디어 쿼리 대용
		
		- gap 으로 넓혀주기 
		
		- 각 셀별로 크기 지정 
			- grid-column-start
			- grid-column-end 
				- 셀 병합 느낌 
		
		- grid-template-areas⭐⭐⭐ 
			- 이름으로 그리드 나누기 
			- "header header header"
			- "a main b"
			- ". . . "
			- "footer footer footer"


[tailwind 에 있는 속성들]
1. 바둑판 만들기 (그리드 만들기)
	1) [tailwind] 
		a) Grid Template Columns
		- 'grid-cols-3' 을 쓰면 -> 	grid-template-columns: repeat(3, minmax(0, 1fr)); 이 css 로 명령어로 들어가서 -> 컬럼 3개, 컬럼당 width 는 최소한 0, 0 을 넘으면 균등 배분(1fr) 이 된다. 
	
		b) Grid Template Rows 와 Grid Template Columns 의 차이)
			- 'div 를 만들어 나가는 순서' 를 'Row' 로 할거냐, 'Columns' 로 할거냐 
			- Columns 를 쓰면 1,2,3, div는, 1번 컬럼, 2번 컬럼, 3번 컬럼 부터 채워진다 -> so, 눈으로 보게 될 때는, 가로 방향으로 채워진다, 라고 생각하게 된다.  
			- row 를 쓰면, div 는 1번 row, 2번 row, 3번 row 의 순으로 채워진다. -> so, 눈으로 볼 때는, 세로방향으로 채워진다고 느끼게 된다. 

		c) grid auto flow 
			- grid 에 배치되는 순서 
			- ex) column 을 사용하면, 아래 방향으로 배치 함 


	2) 일반 css 지식 
		- a) repeat 함수 사용 
			- grid-template-columns: repeat(3, 1fr) = 1) 간격은 1 비율(fraction) 으로 만드는데, 2) 이걸 3번 반복해라 = repeat(3) 
			- grid-template-columns : repeat(3, 1fr 2fr 1fr) = 1) '1 : 2 : 1' 비율로 컬럼을 3개 만들고 2) 이걸 3번 반복해라 -> 그러면, 총 9개 그리드 아이템이 생김

		- b) auto 키워드 사용 
			- grid-template-columns : 200px 200px auto = 1) 컬럼은 3개 2) 세번째 컬럼은, 그리드 칸이 아니라, 콘텐츠 영역 만큼만! 생김 ex) 글자를 썼다면, 세번째 영역은 height = 16px 가 될 것 

		- c) auto fill 사용 
			- [하고 싶은 것] 
				- 주어진 영역의 20% 씩 쪼개서 그리드가 생기게 하고 싶음 -> 20% 씩 쪼개면, 5개 들어감 
				- 동시에, '안에 있는 글씨가 커지면, 그에 맞게 그리드도 커지게' 하고 싶음 
				- 코드 : grid-template-columns : repeat(auto-fill , minmax(20% , auto));

		- d) auto fit 사용 (https://studiomeal.com/archives/533)
			- auto fill 을 할 때, 공간이 남아있으면, 그 부분을 다른 그리드 item 으로 채운다. 


	- 포인트 
		- grid 는 flex 와 마찬가지로, 부모 요소에 적용해서, 자식 요소가 쓸 수 있는 것 임 
		- 이때, '부모 요소가 grid 아이템을 펼칠 수 있는 width, height' 가 있어야! 펼쳐짐 ⭐⭐⭐ 
		- 단위는 'height : 80vh' 같이, 반응형 단위를 사용하자 ⭐⭐⭐ 


2. 각 요소 의 '영역 크기' 지정하기 
	1) 고정 간격 지정하기
	- grid-template-columns : 100px, 200px, 300px, 하면, -> 첫 번째 컬럼 = 100px, 두 번째 컬럼 = 200px, 세 번째 컬럼 = 300px 이 된다.

	2) 비율 간격(fraction) 지정하기
	- grid-template-columns : 1fr 2fr 1fr -> 하면 컬럼은 3개 생기고, 3개 영역은 '1 : 2 : 1' 로 '비율이 분할' 되어 생긴다. 
	- '양끝 고정', '가운데 반응형' 으로 되려면 -> grid-template-columns : 1fr 500px 1fr
	- fr = 늘어날 수 있는 공간이 있으면, 다 들어난다. ⭐⭐⭐ 

	3) minmax(100px, auto) ⭐⭐⭐⭐⭐ 
		- [하고 싶은 것] 
			- '글자가 적은 경우' -> 최소 100px 
			- '글자가 많은 경우' -> 100px 을 넘음 -> 그러면, 알아서 콘텐츠 만큼 늘어나게 = auto

	4) [tailwind 명령어] Grid Column Start / End
		- 전제 :  Grid Template Columns 로 바둑판 배열이 되어 있는 상태 
		- '세 번째 div' 에서 'col-span-2' 를 쓰면, '세번째 div 가 2개를 확장해서 먹는다.'


3. '각 요소 간의 간격' 지정하기
	row-gap : row 간 간격
	column-gap : column 간 간격
	gap : row & column 둘 다 



```


- auto fill 로 채워지는 영역 
![](https://i.imgur.com/4X6VnP5.png)


## 그리드 실전 예제 ⭐⭐⭐⭐⭐ 

### 그리드 만들기 예제 1 :  정적 그리드 아이템 생성 ⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐  
``` bash
- 9개 '그리드 아이템' 이 있음 

- column 은 grid-template-columns : repeat(3 , 1fr) 로 지정 
	- 그러면, 
		- 1) column 의 비율은 동등 비율이 되고, 
		- 2) 3번 반복 하니까, 3개 그리드 아이템이 생김

- row 는 grid-template-rows : repeat(3, minmax(100px , auto)) 로 지정 
	- 그러면, 
		- 1) 하나의 row 영역은, 텍스트가 많건 적건, 최소 100px 이고,
		- 2) 텍스트가 많아져서, 100px 을 넘으면, 텍스트의 크기대로 auto 가 됨. 

그 결과 아래와 같은 모양이 됨 👇👇👇 


- 문제점은, row 가 추가될 경우, 4번째 row, 5번째 row 부터는 적용이 안 된다. 
```

![](https://i.imgur.com/XgdN1y0.png)




### 그리드 예제 2 : 동적 그리드 생성 ⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐ 
``` bash 
[필요한 상황]
1. js 에서 새롭게 item 이 들어왔을 때, grid 의 row 를 수동으로 추가하지 않고도, '새롭게 들어온 item 에 맞게 row 가 동적으로 생성' 될 수 있게 하기 

[코드]
.grid-container {
	display : grid;
	grid-template-columns  : repeat(3, 1fr);
	grid-auto-rows : minmax(100px, auto)
	gap : 1rem // 게시물의 x,y 모든 gap 을 의미
}

[해석]
	- grid-auto-rows : minmax(100px , auto);
		- rows 는 이제 자동적으로 생길 것 임
		- 생기는 row 당 크기는 1) 최소한 100px 이고, 2) 만약, 내용물이 100px 을 넘게 되면, 내용물이 갖고 있는 크기대로 생길 것 임 (auto 가 하는 기능)



```





### [적용] layout 자체에 적용해보기 : 1차 시도는 실패. 끝 row 값이 원하는대로 컨트롤이 안 됨 -> 1차 실패 원인 : taiwind config 에서, 키값을 'gridTemplateRows' 로 따로 지정했었어야 했음 
1. 필요한 grid 설계 
``` bash
- row 3 개
	- 1st = header
	- 2nd = body 
	- 3rd = footer (근데 거의 없어도 될 듯)

- column 4개 
	- 1st = 왼쪽 메뉴 바 
	- 2nd = main content 에서 왼쪽  공란 
	- 3rd = main content
	- 4rd = main content 에서 오른쪽 공란

```


![](https://i.imgur.com/jhuZ3T5.png)



2. tailwind 에서 column 과 row 영역을 지정 하고 싶은 경우 
``` bash
[하고 싶은 것]
	.grid-container {
		display : grid;
		grid-template-columns : 100px, 200px, 300px,
	}

	css 에서 한 것 처럼, '각 columns 별 크기' 를 tailwind 에서 지정하고 싶음. 


[tailwind 예시]
1. 'tailwind.config.js' 에서 그리드 템플릿 컬럼을 정의
	// tailwind.config.js
	module.exports = {
	  extend: {
	    gridTemplateColumns: {
	      'custom': '100px 200px 300px',
	    }
	  }
	};

2. 정의된 클래스 컴포넌트를 사용
	<div className="grid grid-cols-custom">
	  {/* 그리드 콘텐츠 */}
	</div>


[프로젝트에 적용한 커스텀 버전]
  theme: {
    extend: {
      gridTemplateColumns : {
	      'admin_layout_column': '23rem 1fr auto 1fr',
	      'admin_layout_row': '8.06rem 100vh auto',
      },
      
- `'admin_layout_column': '23rem 1fr auto 1fr'`
	- 첫 번째 열을 23rem으로, = 이건 첫 번째 목차의 영역 대로 
	- 두 번째와 네 번째 열을 유효한 공간의 비율(`1fr`)로, 
	- 그리고 세 번째 열을 내용의 크기(`auto`)에 맞춰 설정
	
- `'admin_layout_row': '8.06rem 100vh auto'`
	- 첫 번째 열을 8.06rem,  = 이건 header 의 영역 대로 
	- 두 번째 열을 뷰포트 높이(`100vh`), = 이렇게 하면 안 넘치겠지❓❓ 
	- 그리고 세 번째 열을 내용의 크기(`auto`)에 맞춰 설정 = footer 영역은 없으니까 비워둠


```


3. 1차 시도 실패 원인  
```
여기 보면, row 랑 column 을 따로 지정해줬어야 했음
```
![](https://i.imgur.com/sOyHigv.png)





### [적용] table 태그 대신, grid 기반의 테이블로 만들어보기 


- 적용한 코드 
``` bash
  theme: {
    extend: {
      gridTemplateColumns : {
	      'layout': '23rem 10rem auto 10rem',
        'table': 'repeat(auto-fill, minmax(100px, auto))',
	        // minmax(100px, auto) 에서 100px  = 최소 100px 
	        // minmax(100px, auto) 에서 auto = 100px 넘으면 -> 콘텐츠 크기에 따라서, 콘테이너 크기 맞춰줘, 라는 의미
        
      },
      gridTemplateRows: {
        'layout': '8.06rem 800rem  1rem ',
        'table': 'repeat(auto-fill, minmax(100px, auto))',
      },

```




#### 문제 : 인프런 flex 예제에서 카드 리스트 사용 ⭐⭐⭐⭐⭐ 
- 문제는 살짝씩 틀어지는 이 구간 
![](https://i.imgur.com/oJ5hkyz.png)
















---






# 이슈 모음 

### 1. 자동완성이 안 되었었음 
``` bash
- 이건, code smell 을 extension 이랑 충돌이 일어나서 그랬음. -> 근데, 지우고 나서도 안 되는데? 
- cntrl + space 눌러서 써야 하나
```



### 2. 사진이 안 됨 
https://dalsong-00.tistory.com/35

- 될 가능성이 있음 👇👇👇👇👇 
https://velog.io/@posinity/%ED%85%8C%EC%9D%BC%EC%9C%88%EB%93%9Ccss%EC%99%80-%ED%95%A8%EA%BB%98-%EB%A6%AC%EC%95%A1%ED%8A%B8%EC%97%90%EC%84%9C-%EC%9B%90%ED%95%98%EB%8A%94-%EB%B0%B0%EA%B2%BD-%EC%9D%B4%EB%AF%B8%EC%A7%80%EB%A5%BC-%EC%A0%81%EC%9A%A9%ED%95%98%EB%8A%94-%EB%B2%95