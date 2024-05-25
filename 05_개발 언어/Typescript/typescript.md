## 타입 스크립트 기본 이해

### 다른 언어는 `변수` 를 만들 때, `어떤 타입` 인지 명시

### [필요한 이유] `지뢰밭` 을 피하기 위해

- `지뢰밭` 이란?
    
    - ex) 개발자는 숫자 1 이 들어온다고 생각하고, 로직을 짬. 그런데, 실제로 들어오는 값은 문자열 1 이었음.
    
    ```jsx
    if(count > 5) {
    	// 등록 불가능 
    	return 
    } else { 
    	// 등록 가능
    }
    
    그래서, 5 번이 넘어가면 -> return 되어서 돌아가야 하는데, 돌아가지 않았음. 
    
    시사점은 
    	- '당연하게', '무의식적으로' , '경험적으로' , count는 '숫자' 일거야! 라고 '짐작' 하고 작성 
    	- 이렇게, '타입을 잘못 판단' 하게 될 경우 👉 오류가 발생하게 된다! 라는 것. 
    ```
    
    (출처 : [](https://www.notion.so/9958b60a88564cf5ba2d1e9d047bd8f6?pvs=21)[https://www.notion.so/_13_Typescript-9958b60a88564cf5ba2d1e9d047bd8f6?pvs=4#7f20f6bf7fee44f68809c9e9ad27872f](https://www.notion.so/_13_Typescript-9958b60a88564cf5ba2d1e9d047bd8f6?pvs=4#7f20f6bf7fee44f68809c9e9ad27872f))
    
- 결국, 타입 에러는
    
    - 개발자가 인지하고 있는 타입이, 정말 그 타입인가? 를 확인해야 하는데, 이를 확인하지 못 해 발생하는 에러

## 사용법

### [how] tsconfig 추가 (#📛 강의 다시 듣고 보충)

[](https://www.notion.so/9958b60a88564cf5ba2d1e9d047bd8f6?pvs=21)[https://www.notion.so/_13_Typescript-9958b60a88564cf5ba2d1e9d047bd8f6?pvs=4#f1fbba6f1524470eab9f7ba92e5e6298](https://www.notion.so/_13_Typescript-9958b60a88564cf5ba2d1e9d047bd8f6?pvs=4#f1fbba6f1524470eab9f7ba92e5e6298)

### [how] `타입 이름` 짓기

- 보통, `Interface + 해당 변수` 의 의미로 `IProfile` 이렇게 짓는다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/4ca337b4-e24e-4a5a-8d4e-149b5de39f71/Untitled.png)
    
    [](https://www.notion.so/9958b60a88564cf5ba2d1e9d047bd8f6?pvs=21)[https://www.notion.so/_13_Typescript-9958b60a88564cf5ba2d1e9d047bd8f6?pvs=4#ea66436a887a4af486bddba9efb57306](https://www.notion.so/_13_Typescript-9958b60a88564cf5ba2d1e9d047bd8f6?pvs=4#ea66436a887a4af486bddba9efb57306)
    

### [how] (예외) `공식 문서` 를 찾아봐야 하는 경우

- Component 넣을 때 AppProps 를 넣어야? - next 공식 문서에 있음??????????
    
    ```jsx
    이 경우, 왜 AppProps 를 넣어야 하냐면 
    
    함수의 경우 - 타입 추론이 안 됨 
    -> so, 함수 정의 부분에서 타입 정의하고, 사용할 때, 거기에 맞춰서 써야
    
    이때, next.js 는 프레임워크 니까, Component 를 넣을 때는 미리 지정해버림
    
    음... 맞나? 
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/d946e6f0-fbd7-473e-964c-cf7acb9bc623/Untitled.png)
    

### [기본 원리] TS는 `기본적으로 타입을 추론` 함 → 추론된 타입과 다른 경우가 존재 → `충돌 발생` → 이제부터, `명시적으로 타입` 을 넣어주게 됨

- 타입 추론 : 명시적으로 타입을 넣지 않았음 → aaa 에 “안녕” 넣었음 → 이제 부터 aaa 를 string 이라고 추론 → 그래서 그 다음 aaa 에 숫자를 넣으니, 에러! 를 냄 (#⭐⭐⭐⭐⭐ 타입 추론)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/2ff297fa-3fa4-42e2-90db-a6a7e6591d0e/Untitled.png)
    
- 타입 명시 : 이제 ccc 에 `number | string` 을 부여해서 → `충돌` 해결
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/62358280-0bf3-4543-a027-7a9fb9431d3d/Untitled.png)
    

### [불린 타입-사용팁] ( # `HTML` 에서 받아오는 `라디오 버튼` 은 `문자열` 임 → so, 불린 타입으로 변경해줘야 해!)

- 불린 타입 (#실제로 오류가 많이 일어남) (#DB 에서 받아오거나, HTML 에서 라디오 버튼으로 STIRNG 을 보냈거나 #⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐)
    
    ```jsx
    문자열 true 는 
    
    비어있는 값이 아니고 
    
    비어있으면 ex) " " -> falsy 여서 -> false 인데 
    
    값이 들어가 있으면 -> falsy 아니고 -> true 임 
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/19e72d6f-f3f9-494b-88df-84d83d832981/Untitled.png)
    

### [배열 타입-사용팁] (# 1) 막 넣는다 → 2) 마우스 호버 하면 `추론된 타입` 이 나온다 → 3) 해당 타입을 명시해서 사용한다. #⭐⭐⭐⭐⭐)

- [배열 타입] 다양한 타입을 함께 넣을 경우 → 1) 먼저 막 넣어본다 2) `마우스 호버` 하면 `추론된 타입` 이 나온다 → 3) `추론된 타입` 을 `명시` 해서 쓴다 (#⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/4cab6658-4758-4d64-a817-3fddaac73420/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/66429bed-06d6-467b-9325-11a8340b6666/Untitled.png)
    

### [객체 타입-사용팁] (# 1) 막 넣는다 → 2) 마우스 호버 하면 `추론된 타입` 이 나온다 → 3) 해당 타입을 명시해서 사용한다. . #⭐⭐⭐⭐⭐ #중요 )

- [객체 타입] 객체 타입을 `명시` 하려면, → 마찬가지로, 막 적고 → `추론` 에 의해 나온 것을 → 적어주면 됨
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/150bd1f2-ea1a-4d16-b1bb-a09825296991/Untitled.png)
    

### [map 에서 사용팁] (# 받아온 데이터에서 타입을 설정하면 → map 에서는 element 에 타입이 없어도 된다!

- type 설정 : data? 가 잘 받아와지면 → map 에서 element 는 타입 없어도 됨! (#⭐⭐ codegen 을 하면, type 설정이 간단할 것 같은데 다만, type 을 실제로 할 수 있어야 함 )
    
    ```bash
    타입은 query 를 받아오면 -> 바로 설정 -> 그러면 map 에서 안 해줘도 됨 
    staticRoutingMovedPage 이거 관련해서리!!! 
    ```
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/ff65b23e-0609-4558-bffc-6ffb587c8a72/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/e47caba1-88f3-4ea3-af8b-b99daa4e1137/Untitled.png)
    

### [함수 타입] (#⭐⭐⭐중요)

- [함수 타입 원리 - 1] (#⭐⭐⭐⭐⭐⭐⭐⭐ 가장 중요) 함수 타입은 `input 타입` 과 `return 타입` 이 있음 #만약, return 이 없으면 `void`
    
    함수 타입은 `입력 타입` 과 `리턴 타입` 이 있음
    
    왜냐면 함수는 ‘input - process - output’ 일 테니!!!
    
    - 리턴 타입 과 인풋 타입을 적은 예시
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/fde09183-715e-4920-b3b2-c79858169c87/Untitled.png)
    
    [](https://www.notion.so/9958b60a88564cf5ba2d1e9d047bd8f6?pvs=21)[https://www.notion.so/_13_Typescript-9958b60a88564cf5ba2d1e9d047bd8f6?pvs=4#5a3deb856fd84424bd79fb605c7ad672](https://www.notion.so/_13_Typescript-9958b60a88564cf5ba2d1e9d047bd8f6?pvs=4#5a3deb856fd84424bd79fb605c7ad672)
    
- [함수 타입 원리 - 2] `타입 추론이 안 됨` → 왜냐면, 함수를 사용할 때, 인자에 문자를 넣을지, 숫자를 넣을지 모른다. → 그래서, `함수가 중심` 이 됨. 너네가 나한테 맞춰! 가 된다
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/b4d1c71b-6eee-4201-87d6-05bffecaa052/Untitled.png)
    
- [함수 타입] 함수 타입의 기준은 `함수 정의` 와 `함수 실행` 중 어디에 기준을 맞출 것 인가! 의 문제에서 → `함수 정의` 에 맞춤 → “나는 이것만 받을거야. 이 함수 쓰는 놈들이 거기에 맞춰!!!” 가 됨 (만약, 쓰는 놈들이 마구잡이로 던지면, 난장판 됨. 그래서, `막 쓰는거 방지! 하기 위해서!` )
    
    함수는 받는 쪽!!!!!!! 이 중심임
    
    즉, 함수 정의 할 때 명시한 타입!!!!!!!!! 이 중심
    
    그것대로 함수 실행할 때
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/c323061f-52b0-47c4-98bb-8c11ee82d974/Untitled.png)
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/eb9fab16-8e04-4b3f-bdf2-ae8e864652a6/Untitled.png)
    
- [함수 타입의 강점] 함수를 표현식으로 썼을 때 → 함수 실행 결과를 변수에 담으면 → 해당 변수에서, `함수 return type` 을 알 수 있어!!!!!!!!!!!! (#⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐ 와 몰랐네) → 이것도 결국 `string + number 를 하려고 하는거 아니야?` 라는 `지뢰 판단의 근거` 가 됨
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/e5d4c4d9-b456-4020-aa6b-59c15a102df4/Untitled.png)
    

## [실제 타입 에러 해결하기]

### [빈출 에러] 주소창과 HTML 에서 온 값은 ‘string’ 임!

### [빈출 에러] 값 or 속성을 추가함으로써 → 기존 타입과 달라 발생하는 에러 → `?` 또는 `|` 으로, 해당 변수 또는 객체가 담을 수 있는 타입을 확장!

- 값을 추가하려는 경우. 이때 개발자는, 해당 변수의 타입을 당연히 string 으로 인지한다. 하지만, 애초에 number 로 되어 있다면 에러가 나게 된다 → 이때, `|` 을 통해 `해당 변수가 담을 수 있는 타입을 확장` 한다.
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/3a0e66b9-ef8f-4b67-9988-4c2d77fb1627/Untitled.png)
    
- 객체의 property 를 추가하는 경우. 개발자는, 해당 타입이 당연히 존재한다고 생각함. - 그런데 에러가 남 - 그러면, `?` 을 통해서 `객체가 담을 수 있는 변수를 확장` 하면 됨
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/300579e7-f7bb-4928-beda-d2e059e2a869/Untitled.png)
    

### 나도 모르게 타입 추론이 되어 버린 상황

- `형식에 writer 속성이 없습니다.` 라는 문제 해결 (#⭐⭐⭐ 나도 모르게 타입이 추론되어 버린 상황 # 타입 명시가 필요한 상황 → 명시를 함 → 이때, `지금은 없고, 그때는 있다` 의 상황이 생겨서 오류가 발생함 → 값이면 `|` property 면 `?` 추가해서 대응 )
    
    - [1] 문제 상황
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/39e2587b-0d71-4ec0-888f-c1a93b2bb387/Untitled.png)
        
    - [2] 원인 : myvariables 에 이미 값을 넣었고 → `나도 모르게 타입이 추론` 되어버린 상황
        
        ```jsx
        myvariables 에 number 변수에 Number를 추가 
        myvariables 는 타입추론으로 number 가 됨 
        	이 부분은 마우스호버 하면, 알 수 있음 
        ```
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/6d5baaa1-c5a1-4ffb-8844-9ff56789c299/Untitled.png)
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/254a08a8-7d34-444c-8a66-a67a218a11fc/68ab8e47-0e4f-4b49-8b7a-1f3128e7581f.png)
        
    - [3] 해결-1 : 타입 명시 → 문제는 처음 변수 넣을 때, 없다! 라고 나옴
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/81c180e1-4e37-4be8-b9e4-acb3dce2068d/Untitled.png)
        
    - [4]해결-2 : 타입 명시할 때, `지금은 없고, 그대는 있다` 의 상황을 대비!!! → `?` `|` 를 활용
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/df4f73c5-2e9b-49e4-9157-e41c5705fd6f/f9516c85-dfd5-45af-a3f7-a2a86c11b1fb.png)
        

### event 가 이벤트 핸들러의 매개변수로 들어가는 경우, 함수 정의 부분에서 type 을 정해줘야 하는데, event 에 대해서는 Reat 가 정한 타입을 사용하기

- [event 타입] (#React 가 event 객체를 인자로 넣는다 → 따라서, React 가 만들어 놓은 타입을, 사용해서, 넣는다. )
    
    - [1] 문제 상황 : 뭔가를 적으면 → 이벤트가 발생함 → 그래서, event 객체 안으로 들어감 → 이걸 REACT 가 알아서 해줌 → 그래서, 비록 함수의 매개변수 이지만, React 가 적어놓은 타입을 사용하면 됨
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/ac72a964-6f52-4c73-bc54-cf1ade2eb34f/Untitled.png)
        
    - [2] react 가 정해놓은대로 쓰기 (#📛📛📛📛📛 이걸 그럼 어디서 어케 알지?) (#⭐⭐⭐⭐⭐⭐ 어떤 타입인지는, html 종류 에 따라서 다르다!!!!!!⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐⭐)
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/64d4a5e3-5c87-4742-939f-0e1a708eb653/b3a0cd8d-f02a-4492-88d9-9a23dbc616ae.png)
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/e79fd6b2-23f3-4ee7-8111-dc8290e74b46/Untitled.png)
        

### props 에러 해결

### 타입 관리 (#import #export)

- `함수 타입에 return` 이 없으면 `void`
    
    ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/0cae17fc-ff5c-424e-96d6-f2bfc4d7beb4/883e2d29-9b2a-49bb-a295-15566b2b703b/Untitled.png)
    

## 여기 부터 학습

### 타입 쉽게 사용하기 (#📛 여기부터 학습!!!)

- 여기 부터 학습

‣