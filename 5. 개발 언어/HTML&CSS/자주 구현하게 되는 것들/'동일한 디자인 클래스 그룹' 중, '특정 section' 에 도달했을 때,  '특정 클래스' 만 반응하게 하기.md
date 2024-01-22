


# 설명
``` bash
['동일한 디자인 클래스' 란?]
	- 애플 클론 코딩에서의 'sticky elem'
		- 특성 1 :  '스크롤이 아래로 내려간다고 해서, 같이 따라 내려가는게 아닌 특성!⭐⭐' 을 갖고 있음. 
		- 특성 2 : 각 클래스 마다 '하위 디자인 요소는 다름' ex) 첫 번째는 '목넘김이 다름' 이라는 글자. 두 번째는 '획기적인 손잡이' 라는 글자. 

['특정 section' 에 도달 했다는 건?]
	- '아래로 스크롤 했을 때' 👉 특정, elem 이 보이게 하고 싶어함. 
	- 이때, '트리거는 스크롤' 이고 👉 따라서, 'section 태그' 별로 다르게 반응하게 됨. 

['특정 section 에서 특정 class 만' 의 의미는?]
	- 'sticky elem' 은 동일한 디자인 베이스를 하고 있지만, 하위 요소가 다르다. 
	- 따라서, 'css 복합 선택자' 를 활용해서, '스크롤 트리거' 에 따라 '특정 section' 이 발동되고 -> 해당 class 만의 특별한 디자인 요소가 나오게 된다.. (이건 #show-scene-0 #scroll-section-0 .sticky-elem, 이 선택자에 의해서!)

[주의 할 것]
	- '⭐⭐특정 section 에 들어갔을 때!⭐⭐' 라는 것을 구현하기 위해, 조건문이 아니라, 'css 복합 선택자' 를 사용했다는 것 ⭐⭐⭐ 
	- 그리고, 이 구현 방식은 상황에 따라서, 달라질 수 있다는 것
```



<br>

# 스크롤이 `특정 section` 에 있을 때, `특정 sticky-elem` 보이게 하기 ⭐⭐⭐| 기본 로직 


## 기본 로직 & 구현 ⭐⭐⭐
- 로직 
``` bash
1. 모든 sticky-elem 클래스는 display : none
2. 특정 영역으로 들어갔을 때 -> 해당 영역의 sticky-elem 을 display : block;
```

- 구현 코드 
``` css
/* 딱 붙어 있는 요소들 👇👇 */
.sticky-elem {
    display: none;
    position: fixed;
    top: 0;    
    /* 센터 정렬을 위해, 가로를 다 채워주기 ⭐⭐ | 이런 의도는 중요한 것 같음 ⭐⭐*/
    width: 100%;
    /* 이것도 센터 정렬을 위해서, 같이 넣어준 부분인데, 왜 left 0 인거지?  */
    left: 0;
}

/* scene 과 section 별 매칭 */
#show-scene-0 #scroll-section-0 .sticky-elem,
#show-scene-1 #scroll-section-1 .sticky-elem,
#show-scene-2 #scroll-section-2 .sticky-elem,
#show-scene-3 #scroll-section-3 .sticky-elem {
    display: block;
}
    /* [동작 방식] 
        스크롤 해서 -> 2번째 section 을 지나가게 되면 
        body 태그에 <body id = "show-scene-2"> 이렇게 id 를 붙이게 된다.  
        -> 그러면, #scroll-section-2 에 해당하는 .sticky-elem 만 보인다. 
    */
```


<br>

## 관련 프로젝트 
[[230913_애플페이지클론_섹션2_스크롤을 이용한 인터렉션 구현#스크롤이 `특정 section` 에 있을 때, `특정 sticky-elem` 보이게 하기 ⭐⭐⭐ 기본 로직]]
