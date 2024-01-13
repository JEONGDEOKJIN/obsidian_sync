
### 1. 정의된 함수를 참조 하기 
- 함수가 '참조' 만 된 경우 
	- 클릭 되었을 때 반응함
``` js
  {/* 컨트랙트 배포 */}
  <button onClick={sendTransaction}>컨트랙트 배포</button> <br/><br/>
```


- 만약, 이때, 'sendTransaction( )' 이렇게 실행해버리면, 클릭하지 않아도 계속 실행되는 상태로 남겨져 있게 됨 ⭐⭐⭐⭐⭐ 
``` js
  {/* 컨트랙트 배포 */}
  <button onClick={ sendTransaction( ) }>컨트랙트 배포</button> <br/><br/>
```


### 2. 함수 호출 

2.1 이미 정의되어 있는 화살표 함수를 추가하는 경우 

- '인자' 를 넣을 수도 있고
``` JS
{/* 상태변수 값 증감 */}
<button onClick={() => setValue(1)}> storage 에 있는 값 1 증가 시키기 </button>
<button onClick={() => setValue(-1)} > storage 에 있는 값 1감소 시키기 </button>
```

- 여러 함수를 연속적으로 호출 할 수 있음. 
``` js 
<button onClick={() => { functionOne(); functionTwo(); }}>클릭해주세요</button>
```



2.2 '익명 함수' 추가하는 경우
``` js
<button onClick={() => { console.log("버튼 클릭됨!"); }}>클릭해주세요</button>
```







``` js
      <label> 송금 금액 입력 👇 </label>
      <input onChange={ e => { fixSendMoney(e.target.value) } }>    </input>
      <button onClick={sendWei} > 송금하기 </button>

여기에서 

e  이거는 매개변수 인데 왜 (e) 이렇게 안 써? 
```




