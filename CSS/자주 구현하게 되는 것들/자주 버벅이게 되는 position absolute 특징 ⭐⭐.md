

- position abolute 특징
``` bash
1. 기본적으로 안전하게 사용하기 위해, top, left 를 모두 0 으로 두고 쓴다. 
2. width 를 100% 로 꽉 채우고 사용한다. 
```

``` css 
.global-nav{
    /* position : absolute 일 때, width 를 100% 로 해야 넓어짐 */
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;

    height: 44px;

    /* 좌우 패딩*/
    padding: 0 1rem;}
```


- 관련 프로젝트 
	- [[230913_애플페이지클론_섹션2_스크롤을 이용한 인터렉션 구현#해결방식 nav 태그를 👉 position absolute 로 변경해서 👉 공간을 차지 하지 않게 하기 ⭐⭐⭐ 중요한 이슈 해결]]