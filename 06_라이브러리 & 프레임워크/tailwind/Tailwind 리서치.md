# 리소스 

- 유튜브 링크 : https://youtu.be/qYgogv4R8zg?si=WkMTvv3pYazVwtxP

- [번역] Tailwind CSS에서 혼란을 방지하기 위한 5가지 모범 사례 ⭐⭐⭐⭐⭐⭐ 
	- https://velog.io/@lky5697/5-best-practices-for-preventing-chaos-in-tailwind-css

- tailwind 프로젝트 관리 페이지 
	- https://www.notion.so/STO-3f0ff1027f164bab89aceb6638bb005e?pvs=4


<br>

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

