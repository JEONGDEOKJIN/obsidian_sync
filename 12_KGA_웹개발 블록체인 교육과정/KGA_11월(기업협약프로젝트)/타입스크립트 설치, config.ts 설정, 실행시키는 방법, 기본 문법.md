
---
createDate : 2023-09-07

publish : 벨로그 
blogTitle : reduce 메소드 
publishURL : 
postDate : 

tags : #javascript, #1차작성, 

---

---
createDate : 2023-09-07

isPublished : 
publish : 
blogTitle : 
publishURL : 
postDate : 

tags : #typescript , #타입스트립트 

---


# typescript 설치 

``` bash 
# package.json 초기화
npm init -y

# 개발 버전으로 설치 
npm install -D typescript
	# [주의사항]
		# 1) 설치하고자 하는 디렉토리를 확인  
		
	# -D 로 설치하는 이유는? 
		# 1) typescript 는 javascript 로 '컴파일' 되어서, js 로써 실행됨 
		# 2) js 가 실행되는 환경은 node.js 또는 브라우저임. 
		# 3) js 실행환경에 typescript 는 필요하지 않으므로, 개발시에만 필요한 버전으로 설치

# 설치가 되었는지 확인
npx tsc --version
	# [npx 요약]
		# 1) npx 의의 : npm package executor 의 약자 
		# 2) npx 의 필요성 : '테스트 용도, 종속성 문제 없이, 간단히 npm package 를 실행' 하고 싶을 때 사용 | 만약, 정식과정을 거치면, npm install -> 종속성 문제 해결 -> npm run 의 과정을 거쳐야 하는데, 그럴 필요가 없음. 
		# 3) npx 실행 과정  : 1) local 또는 전역에서, 이미 설치되어 있다면, 해당 파일을 실행 2) 미설치 되어 있다면, npm cache 에서 영역에 설치 후 실행
		
	# tsc : type script compiler
```




<br>


# typescript 로 작성한 파일 실행시켜보기


### 1. 전체 요약 
``` bash
# 1. .ts 확장자 파일 작성
	- 코드 작성

# 2. 컴파일 옵션을 설정할 수 있는 tsconfig.json 파일 만들기
npx tsc --init

# 3. 컴파일 옵션 설정  
{
  "compilerOptions" : {
  "module" : "CommonJS",    // CommonJS 모듈 시스템의 키워드 : require 과 module.export
  "outDir" : "./dist",    // ./dist 로 파일 내보내기
  "target" : "ES6",   // 변환된 버전은 ECMAScript 2015
  "esModuleInterop" : true,   // CommonJS 와 ECMAScript 2015 간 싱크 맞추기  
  "strict" : true,    // 엄격한 타입 검사
  "baseUrl" : "./src",    // '파일 찾을 경로를 custom'
  "paths" : {   // 경로에 붙이는 '별칭(alias)'
      "@user/*" : ["user/*"]   
  }
}
, "include" : ["src/**/*"]  // 컴파일 포함 대상 : scr 경로 아래에 '모든 경로' 에 있는 모든 파일
, "exclude" : ["**/*.test.ts"]    // 컴파일 제외 대상 : '모든 경로' 에 있는 'test.ts 확장자' 가 붙는 파일 
}

# 4.실제로 컴파일 하기 
	# tsc-alias 라이브러리 받아서 설치 
	npm install -D tsc-alias
	
	# package.json 에서 build 에 해당하는 명령어 변경 해주기 
	{ "build" : "tsc && tsc-alias" }
	
	# 터미널에서 컴파일 하기 
	npm run build 

#5. 컴파일된 js 를 node 로 실행 
node dist/<컴파일된 파일> 

```



### 2. `.ts` 확장자로 파일 작성 
- 대략 이런 모습 👇👇
![](https://i.imgur.com/u5YbBD5.png)



<br>

### 3. 컴파일 옵션 설정 (tsconfig.json)

- 요약 
``` ts
// 컴파일 옵션을 설정할 수 있는 tsconfig.json 파일 만들기
npx tsc --init
	// [해석] tsconfig.json 파일이 생겨남


// [기본 예시] 컴파일 옵션 설정 예시 
{
  "compilerOptions" : {
  "module" : "CommonJS",    // CommonJS 모듈 시스템의 키워드 : require 과 module.export
  "outDir" : "./dist",    // ./dist 로 파일 내보내기
  "target" : "ES6",   // 변환된 버전은 ECMAScript 2015
  "esModuleInterop" : true,   // CommonJS 와 ECMAScript 2015 간 싱크 맞추기  
  "strict" : true,    // 엄격한 타입 검사
  "baseUrl" : "./src",    // '파일 찾을 경로를 custom'
  "paths" : {   // 경로에 붙이는 '별칭(alias)'
      "@user/*" : ["user/*"]   
  }
}
, "include" : ["src/**/*"]  // 컴파일 포함 대상 : scr 경로 아래에 '모든 경로' 에 있는 모든 파일
, "exclude" : ["**/*.test.ts"]    // 컴파일 제외 대상 : '모든 경로' 에 있는 'test.ts 확장자' 가 붙는 파일 
}
```

- 디렉토리 위치 및 코드 
![](https://i.imgur.com/lpV7mBN.png)


<br>


- 하위 요소 설명 
``` bash
# 컴파일 옵션 세부 요소 

["compilerOptions"] 
	- ts 파일 컴파일 할 때, '어떤 형태로 컴파일을 할 것 인가' 을 정의하는 부분
	- 이제부터 나오는 것들은 'compilerOptions' 의 세부 속성
	
["module" : "CommonJS"]
	- '컴파일 된 js' 에 'CommonJS' 라는 모듈 시스템을 적용할 것 임. 
	
	Cf. '모듈' 과 'Common JS' 란? 
	- 모듈 : 코드의 집합 (즉, 함수 덩어리, 변수 덩어리, 클래스 덩어리 등을 의미)
	- 모듈 시스템 : 모듈을 '어떻게 가져오고', '내보내는가' 를 규정한 시스템 
	- 'Common JS' : 1) require() 를 통해 모듈을 가져옴 2) module.exports 를 통해 모듈을 내보내는 모듈 시스템 (많고 많은 모듈 시스템 방식 중 하나) 

["outDir" : "./dist"]
	- outDir : 컴파일된 파일을 내보낼 경로 지정 (내보낼 폴더 명 지정)
	- "./dist" : 현재, 'tsconfig.json' 파일이 있는 경로와, '동일 레벨에 있는 dist 폴더' 에 내보낼 것 임. 

["target" : "ES6"]
	- target : 컴파일 된 js의 'ECMAScript 버전' 을 지정 
	- ES6 : ECMAScript 2015 를 의미 

["esModuleInterop" : true]
	- esModuleInterop : 'Common JS 및 AMD 의 export, import 방식' 과 'ECMAScript 2015' 가 호환이 되게 만든다. 
	- 별일 없으면, true 가 좋음 
	- false 를 하면, 호환이 깨짐.

["strict" : true, ]
	- 엄격한 타입 검사 실시 여부 
	- 대부분의 경우, true 로 하면 됨 


["baseUrl" : "./src", ] 
	- baseUrl : 경로의 시작점이 되는 base 를 지정 | 🔹절대 경로의 root🔹 를 내가 원하는 곳으로 지정하는 것과 비슷 | path mapping 또는 custom module resolution 이라고 함. 
	- "./src" : 1) 현재 파일인 tsconfig.ts 의 레벨과 동일한 곳에 있는 2) './src' 폴더를 3) custom root 로 지정 
	- 예시 
		`import a from "@user/server/user.service"` 는 실제로, `./src/user/server/user.service.ts` 를 의미함. 
    

["paths" : {"@user/*" : ["user/*"] }]
	- "paths" : 경로의 별칭(alias) 을 지정
	- "@user/*" : ["user/*"] 
		- 경로 import 할 때, import a from '@user/dj' 라고 하면, ⭐⭐⭐
			0) '@user/dj' 이 '@user/*' 규칙에 부합 하므로, 
			1) paths 에 의해  '@user/dj'는 'user/dj' 경로에 매핑 되고 
			2) baseUrl 에 의해 './src' 가 추가 매핑 된다. 
			3) 최종적으로 './src/user/dj' 를 가리키게 된다. 

	Cf. * , ** 와일드카드(wildcard) 의 사용 
		- ex) '@user/*' : '1단계 depth' 만 가능
			ex) '@user/*' 으로 별칭 설정하면 -> 'user/dj' | 가능 🔵 
			ex) '@user/*' 으로 별칭 설정하면 -> 'user/dj/abc' | 불가 ✖  

		- ex) '@user/**' : '모든 depth' 가능
				ex) '@user/*' 으로 별칭 설정하면 -> 'user/dj' | 가능 🔵 
				ex) '@user/*' 으로 별칭 설정하면 -> 'user/dj/abc' |   가능 🔵
				ex) '@user/*' 으로 별칭 설정하면 -> 'user/dj/abc/def/efg' |   가능 🔵


["include" : ["src/**/*"]  ]
	- "include" : 컴파일 할 파일 지정 
	- ["src/**/*"]
		- src 아래에 있는 '모든 디렉토리' 및 '모든 파일'
		- ["src/**"] 와 동일한 기능 
		- "src/**/*" 이렇게 하면, '파일' 까지 '명시적으로 지정' 힘. 

"exclude" : ["**/*.test.ts"]
	- exclude : 컴파일에서 제외할 파일 
	-  "**/*.test.ts" : 1) 모든 디렉토리에 있는('**/') , 2) 'test.ts' 로 끝나는 파일 ('/*.test.ts*') 

```

<br>

- `import a from "@user/server/user.service"` 는 실제로, `./src/user/server/user.service.ts` 를 의미함.
![](https://i.imgur.com/3X80Sd7.png)




<br>


### 4. 컴파일 옵션대로 '실제로 컴파일' 하기 

1. 요약 
``` bash
# tsc-alias 라이브러리 받아서 설치 
npm install -D tsc-alias

# package.json 에서 build 에 해당하는 명령어 변경 해주기 
{ "build" : "tsc && tsc-alias" }

# 터미널에서 컴파일 하기 
npm run build 

# 컴파일된 js 를 node 로 실행 
node dist/<컴파일된 파일> 
```

<br>

2. 기본 typescript compile
``` bash
// package.json에 'tsc' 추가 
{
    "build" : "tsc"
}
```

![](https://i.imgur.com/7M4RwO7.png)


<br>

3. 기본 컴파일 문제점 : 별칭이 컴파일 되지 않음 👇👇
	- js 는 `@` 이 경로를 읽지 못 함 
	- 따라서, 읽을 수 있게 변환해줘야 함 
![](https://i.imgur.com/V2IAhi8.png)



<br>

4. `tsc-alias` 라이브러리 설치 후 build 에 `tsc-alias` 추가
``` bash 
# tsc-alias 라이브러리 받아서 설치 
npm install -D tsc-alias
	# 개발에서만 필요하기 때문에 D

# package.json 에서 build 에 해당하는 명령어 변경 해주기 
        {
		    "build" : "tsc && tsc-alias"
        }

# 터미널에서 컴파일 하기 
npm run build 
	# dist 폴더가 생김
```


- `npm run build` 하면 -> dist 폴더가 생김

![](https://i.imgur.com/35fJMJq.png)


<br>

5. 컴파일 된 파일 실행하기 
``` bash
# 방법1 
	node dist/<컴파일된 파일> 
	ex) node dist/msg.js
```

- node dist/<컴파일된 파일> 로 실행 👇👇

![](https://i.imgur.com/6cNV4rj.png)



<br>







# 특정 파일 제외하고 컴파일 하기 

``` bash
'컴파일 설정'의  'exclude' 항목에서, 제외할 파일명 규칙을 기재 
```

- exclude 에 넣으면 -> compile 이 안 되어서 -> dist 폴더에 없음 
![](https://i.imgur.com/G4GTTfw.png)


<br>

- exclude 에 안 넣으면 -> compile 이 됨  -> dist 폴더에 있음. 
![](https://i.imgur.com/9cknriG.png)






<br>







# 타입 스크립트 기본 문법 
``` ts
// 🔹 javascript

    // 숫자 문자
    let num = 20;
    const str = "javascript";
    
    // 특수 타입
    const nam = NaN;    
		// 숫자를 문자로 변환했을 때?

	// 일반 타입 
    const bool = true;
    const nullValue = null;
    const undefinedValue = undefined;

	// 레퍼런스 타입
    const obj = {};
    const arr = [];

	// 함수 - any
    const fn = (a:any) => {
        console.log(a)
    }
        // any : 모든 타입을 다 통과 시킴 

	const sum = (a:any , b:any) => {
	    return a + b;
	}

	// any 와 unknown
	const any = ""
	
	const unknown = ""; 



// typescript 
	// 숫자 & 문자
    let num2 : number = 20;
    const str2 : string = "typescript";

	// 일반 타입 
    const nan2 : number = NaN;
    const infinity2 : number = Infinity;

    const bool2 : boolean = true;
    const nullValue2 : null = null;
    const undefinedValue2 : undefined = undefined;

	// 레퍼런스 타입 
    const obj2 : object = {};
    const arr2 : Array<number> = [1,2,3];
    // const arr2 : Array<number> = [1,2,"3"];
        // 배열은 '배열 안에 있는 요소' 가 어떤 타입인가! 를 지정해야 함 
        // 요소를 "3" 문자열이 들어가면 오류

    // 제네릭 타입 
        // 설정 요소가 number 라고 지정 
        // 데이터 타입을 매개변수화 시킬 수 있다. 
        const arr3 : Array<number | string> = [1,2,"3"];

    //  함수 - void
    const fn2 = (a:number):void => {
        console.log(a);
    }
    // void
        // 함수 실행 시 비어있다! 는 것을 의미.
        // 반환값이 없는 함수! 를 의미
        // 안 쓰면 -> void 임.  

    // 함수 - return 타입이 number
    const sum2 = (a:number , b : number) : number => {        
        return a+b;
        // return "1";  이건 오류! ✅ -> 왜냐면, 문자열! 을 반환하니까
    }
        // void 가 아니라, :number 로 반환값 타입을 써주면 -> 반환값이 숫자! 여야 함 


    // any : 어떤 타입이건 할당 가능
    const any2 : any = " "; 
        // any 를 남발하면, 타입 스크립트를 쓰는 이유가 없음
        // 남발 하지 말것. 
        // type 의 안정성이 보장되지 않음 
        console.log(any2.length);   // 동작함🔵
        
    // unknown2 : 1) 어떤 타입이건 가져올 수 있고 2) 타입 안정성을 지킬 수 있음. 
    const unknown2 : unknown = "";
        // console.log(unknown2.length);   // 동작 안함📛📛
            // 왜냐면, unkwno2 가 뭔지 모르니가 -> 길이 부르면 위험해! 

        if(typeof unknown2 === 'string')
        console.log(unknown2.length)
            // 이렇게 타입 검사를 하고 넘어가면 -> 오류가 안 남! 
```


- array 타입 유형 추가 
	- 출처 :  230831 수업 중 vscode > 04_syntax > array.ts
``` ts 
// 타입 추론 없이 배열 선언
    // 타입 추론이 없다는 말이 무슨 말 이지❓❓
    // generic 이랑 비교하면, 배열 안에 string 이 들어갈지, number 가 들어갈지, ts 가 판단할 필요가 없다는 의미.
    // ex) '제네릭 타입' 은 const arr3 : Array<number | string> = [1,2,"3"]; 이렇게 되어서 👉 array 안에 number 또는 string, 그 어떤 것 이든 들어갈 수 있음.
const strArr : string [] = ["1" , "2" , "3"];
const numArr : number[] = [1,2,3];

// 튜플 
    // 각 배열의 자리에 타입을 지정 
const tuple : [string , number, object] = ['hello' , 123 , {}]; 


```



