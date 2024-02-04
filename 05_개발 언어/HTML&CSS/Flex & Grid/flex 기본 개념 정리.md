
# 유연한 박스 

- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션1 > Flex 핵심정리 #4 - 유연한 박스`

<br>

## flex-basis

- 개념 
```
flex-basis 는 flex 아이템의 초기 크기를 설정
width, height 와 비슷한 역할
```

![](https://i.imgur.com/T9WT2zP.png)
(출처 : https://studiomeal.com/archives/197)


- 만약, width : 100px 로 설정한다면
![](https://i.imgur.com/COfx833.png)


- 정리하면 
``` bash 
- flex-basis 는 flex item 의 초기 크기를 설정함. 
- 최소값으로 작용하고, 해당 값을 넘는애들까지 강제로 작아지게 하지 않는다.
```


- 예제 코드 
``` css
.item { 
	/* 100px 미만인 flex아이템은 100px 까지 늘어남
	100px 이상인 flex아이템은, 그냥, 원래대로
	*/
	flex-basis : 100px
}
```


<br>

## flex-grow 

^1163fa

- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션1 > Flex 핵심정리 #4 - 유연한 박스`

- 작동 원리 
``` css 
- 문제 상황 
	- '컨테이너의 크기' 와 'flex 아이템의 크기' 를 비교 했을 때, '여백을 어떻게 처리' 할 것 인가. 
	- 이 문제는, 브라우저의 너비 조절에 어떻게 대응할 것 인가! 에 자주 등장하는 문제 ⭐

- 원리 
	1. flex container 안에 '남은 공간' 이 있고, 'flex-grow에 양의 값' 이 설정되어 있다면
	2. '남은 공간을 해당 비율만큼' 갖게 된다. 
	3. 늘어나는 것은, 자기 부모의 크기 만큼만! 늘어남

- 포인트 
	- '비율' 은 '여백의 비율' 이다. (전체 콘텐츠와 여백이 함께 계산되는 공간이 아니고, '여백' 의 비율만을 따진다. ⭐⭐⭐)
	- '컨테이너 안에 남은 공간' 을 어떻게 분배할 것 인가의 문제 ⭐⭐⭐ 

/* 예시 */ 
	.container {
	    display: flex;
	}
	
	.item1 {
	    flex-grow: 1;
	}
	
	.item2 {
	    flex-grow: 2;
	}

/*
	👉 flex container 안에 '300px 이 남았다면', 1) item1 이 100px 2) item2 가 200px 씩 나눠갖게 된다. 	
*/
```

![](https://i.imgur.com/NYBiSi4.png)
(출처 : https://studiomeal.com/archives/197)


<br>


## flex-shrink 

^68a31b

- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션1 > Flex 핵심정리 #4 - 유연한 박스`

``` bash 
- 문제 상황 
	- '컨테이너의 크기' 와 'flex 아이템의 크기' 를 비교 했을 때, '컨테이너가 더 작아진 경우', '아이템을 어떻게 축소' 시킬 것 인가의 문제. 
	- 이 문제는, 브라우저의 너비 조절에 어떻게 대응할 것 인가! 에 자주 등장하는 문제 ⭐
		- ex) Do it 시리즈에서, 사진 넣는 것도 이거랑 관련됨 ⭐⭐ 

- 작동 방식 
	- 기본값 : flex-shrink : 1 ⭐⭐⭐⭐⭐ 
	- 작성된 비율만큼 해당 flex item 이 축소된다. 
	- flex-shrink 0 👉 '버팅기고 있게 된다.'

- 포인트 
	- 기본값이 1 이기 때문에 -> 뭘 안 해줘도, 우선, 줄어들게 되어 있음. 
	- flex-grow 랑 flex-shrink 는 세트⭐⭐⭐ 


- 예시 코드 
	.container {
	    display: flex;
	}
	
	.item1 {
	    flex-shrink: 1; /* 기본값과 동일, 필요한 경우 축소될 수 있음 */
	}
	
	.item2 {
	    flex-shrink: 2; /* item1보다 두 배 더 쉽게 축소됨 */
	}


```


<br>

## flex 

^4bb31b

- 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션1 > Flex 핵심정리 #4 - 유연한 박스`

``` bash 
- 기본 개념 
	- flex-basis, flex-grow, flex-shrink 를 한번에, 같이 쓸 수 있게 함. 
	- '단축 속성(shortcut-property)' 임 [[다양한 대응방안 정리]]

- 구성 요소 
	- flex: [flex-grow] [flex-shrink] [flex-basis];
	- flex-grow : 기본값 0 | 기본값 0의 의미 = 기본적으로 여백이 있다고 커지진 않음 ⭐⭐⭐
	- flex-shrink : 기본값 1 | 기본값 1의 의미 = 기본적으로 살짝 줄어들긴함 ⭐⭐ 
	- flex-basis : 0% ⭐⭐⭐⭐⭐ | 기본값 0% 의 의미 = 처음에 그려지는 것은 0 이다. 아무것도 없다. 

- flex 의 실행 흐름 ⭐⭐⭐⭐⭐ 
	1. 여백 계산 
		- flex-basis 의 기본값은 0% -> 따라서, 처음에 그려지는 것음 0 임 -> 그리고 '여백' 크기를 확정
		- 만약, flex-basis 값을 설정하면, 해당 비율 만큼 그리고 -> '여백' 크기를 확정 
	2. '위에서 계산된 여백' 을 flex-grow 의 비율대로 나눠그림 
	3. 만약, '여백이 없다면', 각 flex-shrink 비율대로 축소해서 그림 

- 시사점 
	- 생각해보면, '브라우저 너비 조절' 은 👉 'container의 크기 VS item 의 크기' 의 문제를 낳는데 
		- 👉 flex 의 구성요소 3가지를 보면, basis 를 기반으로 grow, shrink 만 결정해주면, 브라우저 조절에 대응이 된다는 것. 


- 예제 코드 
	.flex-item:nth-child(1) {
		flex : 1
		/* [해석] flex : 1 1 0% 이것과 동일 ⭐⭐⭐⭐⭐ 
			[실행순서] 
				1. flex-basis 0% 가 먼저 실행 -> 처음에 그려지는 것은 0 임 
				2. 남은 여백을 flex-grow 의 비율대로 계산함 -> 1:1:1 로 나눔
		*/
```


<br>

### 문제점 : 다양한 콘텐츠의 길이에 대응하기 힘듦 😥😥😥 
``` bash 
flex-item 안에, 
내용물이 엄청 길어지면, 
flex 시스템으로 강제하지 못 함. 

왜냐면, 
flex 계산상, '여백' 이 있어야, flex-grow 를 할 수 있는데, 
애초에 flex-item 의 콘텐츠가 '엄청 길면' -> 'container 와 flex-item 을 비교' 했을 때, '여백 자체가 없음' 으로 -> flex-grow 자체가 안 먹 힘 ⭐⭐⭐⭐⭐

```

<br>

### 해결방안 : `width 20%` 이렇게 비율을 사용 

- 'flex 매커니즘을 사용했던 니즈' 를 해결되었는지 검토 
``` bash 
- 'flex 매커니즘을 사용했던 니즈' 는 
	- 브라우저 크기를 키우면 -> '남은 여백' 을 1:2:1 의 비율로 나눠 가져서 크기가 커졌으면 했음. 
	- 브라우저 크기를 줄이면 -> flex-item 이 1:2:1 의 비율로 줄어들었으면 했음. 

- width % 설정으로 해결되나? 
	- 20% : 60% : 20% 로 설정하면 -> 브라우저 크기에 대응해서, 원하는 사이즈가 나올 수 있음 
```



- 무지막지하게 긴 콘텐츠 길이에 대응했는지 검토 
``` bash 
- width % 설정으로 가능했던 것 
	- flex-item 자체의 크기는 20% 로 설정할 수 있음. 

- width % 가 하지 못 하는 것 (한계) 
	- 무지막지하게 긴 콘텐츠는 container 를 뚫고 나옴 

- 무지막지하게 긴 콘텐츠가 container 를 뚫고 나오지 못 하게 하려면 
	- flex-item 에 overflow : hidden 를 줘서, flex-item 내부에서 p 를 삐져나가지 못 하게 한다. 

- 결론 
	1. flex-item 에 'width %' 를 설정한다. ⭐⭐⭐⭐⭐ 
	2. flex-item 를 삐져나오는 무지막지하게 긴 콘텐츠가 분명히 존재하므로 -> 이건, 'overflow : hidden' 등으로 처리 ⭐⭐⭐⭐⭐ 

```

^2cd36e

- 무지막지하게 긴 콘텐츠가 container 를 뚫고 나온 모습 
![](https://i.imgur.com/wBbj0n1.png)


<br>

### 그러면, flex 는 어디에 써? (flex-grow 는 '여백' 이 있는 경우에 사용할 수 있음. )

``` bash 
- flex 는 '다단 컬럼 구성상 여백' 생겨났을 때 -> 빈공간을 채워서 -> 통일감을 줄 수 있음. 
```


- 예시
``` bash 
- '이렇게 애매하게 남아있는 공간' 이 있음. 
```
![](https://i.imgur.com/ANK7cwM.png)



- 예제 코드 
``` css 
- 이렇게, flex-grow 하나만 써주거나
	.flex-item {
		flex-grow: 1;
	}

- 이렇게 작성해도 동작함
	.flex-item {
		 flex : 1 1 auto
	}
👉 auto 가 어떻게 동작하는거지?????

- 시사점 
	- flex-basis 는 기본값 auto 로 사용하는게, 안전함 ⭐⭐⭐⭐ 
	- 다만, 이 부분을 완전히 이해하진 못 함 
```

(출처 : - 수업 출처 : `CSS Flex와 Grid 제대로 익히기 > 섹션1 > Flex 핵심정리 #5-flex 속성 활용 - 11분`) ⭐⭐⭐⭐⭐⭐ 


^4acfb8







# 궁금한 점 

- 여기에서 auto 의 개념이 뭐지?  [[flex 기본 개념 정리#^4acfb8]]





