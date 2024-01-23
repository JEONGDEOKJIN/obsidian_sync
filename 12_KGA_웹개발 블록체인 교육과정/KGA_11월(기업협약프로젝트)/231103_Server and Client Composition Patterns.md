
## 리소스 
- 출처 : https://nextjs.org/docs/app/building-your-application/rendering/composition-patterns



## 문제 상황 ⭐⭐⭐ 

1. 클라이언트 컴포넌트에서 서버 컴포넌트를 사용해야 하는 경우 
- 옵시디언 출처 : [[231103_client component by 공식문서 ⭐⭐⭐#^2d03d4]]
- 공식 문서 출처 : https://nextjs.org/docs/app/building-your-application/rendering/client-components#how-are-client-components-rendered
``` bash
- you may want to 'reduce the client bundle size', 'fetch data on the server', or '⭐⭐ use an API that is only available on the server' ⭐⭐ 
```


## [When to use Server and Client Components?]
- 출처 :  (https://nextjs.org/docs/app/building-your-application/rendering/composition-patterns#when-to-use-server-and-client-components)

![](https://i.imgur.com/HtaPpSn.png)

- 왜 이렇게 구분 된 건가? 왜 구분해서 쓸 수 밖에 없나? ⭐⭐⭐⭐⭐⭐ 
``` bash
server component 는 서버의 자원을 활용해서, 'html 및 RSC Payload 를 미리 준비' 해둔다. 

즉, 특정 컴포넌트를 server component 로 할당해 두면 (이게 기본값 이지만) , 서버는 'html 및 RSC Payload 를 미리 준비' 해둔다. 

왜 그래야만 하는가? 
	그렇게 되면, 미리 준비된걸 던져주면 되니까, 브라우저가 해석해야 하는 js bundle 이 적어서, 속도 측면에서 빠르고, seo 측면에서 좋다. (일반론)

이걸 하려면, 즉, SSR 을 하려면, 왜 구분해서 사용해야만 하는가? 
	'특정 컴포넌트의 동작' 이 '브라우저 기반 api 사용' 혹은 '브라우저 기반 환경에서 동작하는가' 를 본다. 
	미리 할 수 있다면 너무 좋은데, '그 컴포넌트가 쓰는 기능의 본질이 브라우저를 만나야만 동작' 할 수 있는 거라면, 
	클라이언트가 렌더링 할 수 있게 조치를 취해줘야 하는 거지. 

어쩌면, 너무 당연함. ⭐⭐⭐⭐⭐⭐⭐⭐ 
	즉, '특정 컴포넌트에서 사용하고자 하는 기능이 뭔가' 를 보고, 
	'해당 기능이 온전하게 동작하려면, 브라우저 api 또는 브라우저 환경이 필요한지를 보고', 
	브라우저 환경이 필요 하다면, 'next.js framework 이 정해놓은 규칙에 따라서, 브라우저에게 잘 전달될 수 있게!' 해줘야 하고, 
	'use Client' 를 header 에 작성하여 -> 'RSC Payload 에 담겨서 전달' 되게 한다. 
	

```


- 그 밖에 구분 기준 예시 
``` bash
'use an API that is only available on the server' -> server component
```




