정리하면 

[내가 느낀점] 
	- 지금까지는 '값' 을 기준으로 생각했다. 그 전에, '값' 이 결정되기 전인 앞단에서 '타입' 을 생각한다. 
	- '값' 이 들어가는 곳은 '변수' 다. 따라서, 변수를 기준으로 작성하게 된다. 
	- 따라서 '모든 변수' 는 type 이 설정될 텐데, 그게, infer 되거나, explicit 되는 경우가 있게 된다. 
 

[Type Inference & Explicit Type Annotations]

ts 는 type infer 기능이 있음
initial value 가 설정되면 -> 해당 값을 기준으로 추론 
initial value 가 없으면 -> any 로 보고 모든 타입을 받음 -> type checking 안 됨 

그럼 언제 explicit type assign 을 해? 
ts 가 infer 해주는 type 과 내가 기대하는  type 이 다를 때! 
또는 built in 타입 과 다른 타입이 필요할 때 


[union type]
	- 필요한 상황 ⭐⭐⭐ variable that shoud not be limited to one value type ⭐⭐⭐ 
	- 키워드 : variable, 값 할당하기 전 타입을 부여
![](https://i.imgur.com/e5jbKgv.png)



[Working with Object Types]

- '객체' 는 각 키가 어떤 type 을 갖는지, 'struct' 를 정해줘야 함. 
ex) name key, which should hold string, 
ex) age key, which should hold number, 
![](https://i.imgur.com/jxeR5lC.png)




[Working with Array Types]
```
1) array type 은 '이건 array 야!' 에서 끝나는게 아니라, more information 을 원함. (마치, 객체에서 key 하나 하나 당 type 을 지정한 것 처럼) 
2) 그래서, 이건 array of string 이야! 라는 수준 까지 원함 
3) array of string 을 표현하는 2가지 방법 
	a. let hobby : Array<string>
		i. hobby should be an array of string values 로 읽는다. 
	b. let hobby : string[] 
		i. hobby should be an string array 
```

![](https://i.imgur.com/XgmmJUU.png)






[Adding Types to Functions - Parameter & Return Value Types]


return statement 가 없는 경우 

1) undefined
![](https://i.imgur.com/RkkcAxj.png)




1) void : does not return anything ⭐⭐⭐⭐⭐⭐ 
![Uploading file...mcqbq]()



- return 값이 있는 경우 
	○ 기본적으로는 infer 를 한다. 
	○ 혹은 추정되는 값( 여기에서는 number )를 적는다. 
![](https://i.imgur.com/FietGM8.png)





[Defining Function Types ⭐⭐⭐⭐⭐] 

calculate 는 세번째 매개변수로 '함수' 를 받고 있다. 
이 함수가 어떤 형식이어야 하는가? 어떤 structure 여야 하는가? 

매개변수로 a 라는 number, b 라는 number 타입을 받고 
return 을 number 형태를 한다. 

이걸 명시 해둔다. 

이렇게 type 설정을 하고 

맞게 할당해서, 실행하면 된다. 

다만, 이 함수 설정이 길어질 수 있다. 
따라서, 밖에서 type 정의하고, 가져올 수 있다. 
(⭐outsource this type definition⭐')

![](https://i.imgur.com/kQ5YHjh.png)




[Interfaces vs Custom Types]

ingeneral you can always use type keyword
allow you to define other types 
![](https://i.imgur.com/Nw1gt0D.png)



interface 는 
	1) limited to obejcts
	2) 장점은 이렇게 implements 할 수 있음 
![](https://i.imgur.com/WfMGQHr.png)


	1) 그리고 쉽게 redefine 할 수 있음! 
mode key 를 쉽게 추가할 수 있음. 
![](https://i.imgur.com/4398hi6.png)







[Merging Types ⭐⭐⭐⭐⭐⭐⭐] 

	- type 키를 사용해서 Admin 과 AppUser 를 합치고 싶은 경우 
![](https://i.imgur.com/wz3fDSR.png)


	- interface 키로 합치고 싶은 경우 
		○ 이렇게 Admin, AppUser 를 extends 하면 AppAdmin 으로 확장된다 
		○ 즉, 합쳐진다. 
![](https://i.imgur.com/lDGIc6F.png)
![](https://i.imgur.com/1wXvuAS.png)

 





[Being Specific With Literal Types]


role 에 'admin, user, editor' 만 오게 하고 싶은 경우 
string 으로 하면, 모든 글자가 다 들어오는데, 그러면 안 되니까. 
![](https://i.imgur.com/p37xTIl.png)



다만, 하나로 잠궈놓을 수 있긴 한데 

let role : 'admin' | 'user' | 'editor' 
이렇게 일반 변수 선언에서 처럼 let 를 쓰네 
![](https://i.imgur.com/nuyQd0N.png)




[Adding Type Guards ⭐⭐⭐⭐⭐⭐] 

type Role = 'admin' | 'user' 
let role : Role; 
role : Role

이렇게 , 특정한 값만 들어와야 하는 경우, 
![](https://i.imgur.com/SrIQo9M.png)



- 이렇게 조건문과 && 을 사용해서 type guards 를 걸어 줄 수 있음 ⭐⭐⭐⭐⭐⭐⭐ 
- 그래서 내가 원하는 것만 들어오게 더 엄격하게 관리 ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/ydsyZqQ.png)




[Type Guards & Type Narrowing - A Closer Look] 

Type Guards & Type Narrowing - A Closer Look


When using "Type Guards" (i.e., if statements that check which concrete type is being used), TypeScript performs so-called "Type Narrowing".
This means that TypeScript is able to narrow a broader type down to a more specific type.
Consider this example:

1. function combine(a: number | string, b: number | string) {
2.   if (typeof a === 'number' && typeof b === 'number') {
3.     return a + b;
4.   }
5.  
6.   return `${a} ${b}`;
7. }
In this example, inside the if statement, TypeScript narrows the types of a & b from "either a number or a string" down to "definitely a number" - because that's what the condition of the if check says (and TypeScript "understands" that).
After the if statement, TypeScript understands that a and b are again either a number or a string"  because we only make it into the if statement if both are of type number. The type therefore is broader again.
You can add all kinds of "Type Guards" to run code conditionally and get TypeScript to narrow a type:
	• Use JavaScript's typeof operator as shown above to check if you're dealing with a string, number, boolean, object, function, symbol or bigint type
	• Use JavaScript's instanceof operator to check if an object value is based on some specific class
	• Use JavaScript's in operator to check if an object contains a specific property
Important: You can NOT check if a value meets the definition of a custom type (type alias) or interface type. These are TypeScript-specific features for which no JavaScript equivalent exists. Therefore, since those if checks need to run at runtime, you can't write any code that would be able to check for those types at runtime.
For example, the below code won't work because the User type does not exist once the code is compiled to JavaScript:

8. type User = {
9.   name: string;
10.   age: number;
11. };
12.  
13. type Admin = {
14.   name: string;
15.   age: number;
16.   permissions: string[];
17. };
18.  
19. function login(u: User | Admin) {
20.   if (typeof u === User) {
21.     // do something
22.   }
23. }
But you could check for the existence of the permissions property since only the Admin object will have one:

24. function login(u: User | Admin) {
25.   if ('permissions' in u) {
26.     // do something
27.   }
28. }
That code would work at runtime.

출처: <https://kmooc.udemy.com/course/react-typescript-the-practical-guide/learn/lecture/40464100#content> 





# [generic type] ⭐⭐⭐ 


- 요약 
```
place holder 가 있음. 
그 뒤 혹은 위에, '구체화' 시켜 나가는 과정이 있음 
```



### udemy 강의 요약
```
1. 아직, 어떤 타입이 들어올지는 모르는 상황
2. 그때, placeholder T, U 같은 걸 써놓음 
3. 그리고, 실제로 해당 타입을 사용할 때, 타입을 부여하고, 타입에 맞는 값을 쓴다. 
4. 추후에, 이 GENERIC TYPE 은 재활용 가능 
5. 이건, 함수를 정의할 때도, GENETIC TYPE 가능  
```



![](https://i.imgur.com/6aoNStU.png)
![](https://i.imgur.com/ULCjt0X.png)
![](https://i.imgur.com/bZlZ9bB.png)


### [예시]'제너릭 타입 매개변수' 이슈 ⭐⭐⭐⭐⭐ 
- 예시 코드 
``` ts 
"use client";

interface VoteProps {
  title: string;
  description: string;
  id: number;
  author? : string;
}

interface RenderVotesProps {
  voteListData: VoteProps[];
}

export const RenderVotes: React.FC<RenderVotesProps> = ({voteListData}) => {
  return (
    <>
    </>
  );
};

```


- 해석 
``` bash
RenderVotes: React.FC
	 /*RenderVotes 라는 함수가 있는데, 이 함수의 타입은 'react functional component(리액트 함수형 컴포넌트)' 라는 걸 '명시적으로 선언(explicitly assign)' 한 것. 
	
	React Functional component 로 명시 선언되면 
	1) props 를 받을 수 있고 
	2) type checking 을 받을 수 있고 
	3) jsx/tsx 를 사용할 수 있음. 
	
	그러면, 꼭, '명시적으로 선언' 해야 하는 건가?
	'추론 기능' 을 사용할 수도 있지만, 타입 오류의 가능성이 높아짐
	
	*/


React.FC<RenderVotesProps>
	/* 이 react 함수형 컴포넌트의 '인자의 type' 로 무엇을 받을 것 인가? 라고 했을 때, 'RenderVotesProps' 이걸 '해당 함수형 컴포넌트의 인자 타입' 으로 받겠다는 말
	*/


그러면, RenderVotesProps 은 어떻게 설정되어 있는가? 

	interface RenderVotesProps {
	  voteListData: VoteProps[];
	}

이걸 보면, voteListData 라는 변수가 들어오고, 해당 변수는 VoteProps 타입이어야 한다. 
즉, props 로 들어오는 voteListData 변수는 VoteProps[] 타입 이어야 한다. 

'VoteProps[] 타입' 은 
interface VoteProps {
  title: string;
  description: string;
  id: number;
  author? : string;
}

을 통해 보면 
1) '배열' 인데 
2) 구성 요소는 '객체' 이고 
3) 각 객체의 key 는 title, description, id, author 로 구성된다. 

즉, 

이렇게 구성된 타입을 가진 객체인 voteListData 이 
제네릭 타입인 RenderVotesProps 에 들어가게 되어, 
매개변수인 ({voteListData}) 으로 들어가게 된다. 

```


- 그러면 왜 제네릭 타입 매개변수 인가? 왜 제네릭 인가? 
``` bash
제네릭의 특징은 'placeholder' 라는 것 
즉, 선언할 때, placeholder 이고, 
실제로 실행하게 될 때, 추가로 구체화 시킨다. 

이 경우, 

RenderVotes: React.FC<RenderVotesProps>
여기에서, 'placeholder' 가 나오고 

'구체화' 되는 건, 
여기 아래 부분 인 듯 하다. 
interface VoteProps {
  title: string;
  description: string;
  id: number;
  author? : string;
}

interface RenderVotesProps {
  voteListData: VoteProps[];
}


```


