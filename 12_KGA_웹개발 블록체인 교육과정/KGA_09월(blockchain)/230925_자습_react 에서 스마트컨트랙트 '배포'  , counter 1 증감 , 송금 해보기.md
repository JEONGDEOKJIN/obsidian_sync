# TOC

1. [0. 포인트](#0-%ED%8F%AC%EC%9D%B8%ED%8A%B8)
1. [1. 리액트 환경에서 '배포' (및 '배포한 컨트랙트 실행' 프로세스 요약)](#1-%EB%A6%AC%EC%95%A1%ED%8A%B8-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-%EB%B0%B0%ED%8F%AC-%EB%B0%8F-%EB%B0%B0%ED%8F%AC%ED%95%9C-%EC%BB%A8%ED%8A%B8%EB%9E%99%ED%8A%B8-%EC%8B%A4%ED%96%89-%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4-%EC%9A%94%EC%95%BD)
	1. [0) 지금 어떤 일이 벌어지는지 이해하기](#0-%EC%A7%80%EA%B8%88-%EC%96%B4%EB%96%A4-%EC%9D%BC%EC%9D%B4-%EB%B2%8C%EC%96%B4%EC%A7%80%EB%8A%94%EC%A7%80-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0)
	1. [1) 터미널에서 ganache-cli 실행 👉 '비밀키(private keys)' 발급 👉 메타 마스크 내의 '이더리움 계정' 생성하기](#1-%ED%84%B0%EB%AF%B8%EB%84%90%EC%97%90%EC%84%9C-ganache-cli-%EC%8B%A4%ED%96%89--%EB%B9%84%EB%B0%80%ED%82%A4private-keys-%EB%B0%9C%EA%B8%89--%EB%A9%94%ED%83%80-%EB%A7%88%EC%8A%A4%ED%81%AC-%EB%82%B4%EC%9D%98-%EC%9D%B4%EB%8D%94%EB%A6%AC%EC%9B%80-%EA%B3%84%EC%A0%95-%EC%83%9D%EC%84%B1%ED%95%98%EA%B8%B0)
	1. [2) '메타마스크에 접속한 계정' 의 '이더리움 주소' 가져와서 연동하기 ⭐⭐⭐](#2-%EB%A9%94%ED%83%80%EB%A7%88%EC%8A%A4%ED%81%AC%EC%97%90-%EC%A0%91%EC%86%8D%ED%95%9C-%EA%B3%84%EC%A0%95-%EC%9D%98-%EC%9D%B4%EB%8D%94%EB%A6%AC%EC%9B%80-%EC%A3%BC%EC%86%8C-%EA%B0%80%EC%A0%B8%EC%99%80%EC%84%9C-%EC%97%B0%EB%8F%99%ED%95%98%EA%B8%B0-)
	1. [3) solidity 파일에 내용 작성](#3-solidity-%ED%8C%8C%EC%9D%BC%EC%97%90-%EB%82%B4%EC%9A%A9-%EC%9E%91%EC%84%B1)
	1. [4) 해당 파일 컴파일 하기](#4-%ED%95%B4%EB%8B%B9-%ED%8C%8C%EC%9D%BC-%EC%BB%B4%ED%8C%8C%EC%9D%BC-%ED%95%98%EA%B8%B0)
	1. [5) 컴파일된 결과물인 bin 파일 값을 가져오기](#5-%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%90%9C-%EA%B2%B0%EA%B3%BC%EB%AC%BC%EC%9D%B8-bin-%ED%8C%8C%EC%9D%BC-%EA%B0%92%EC%9D%84-%EA%B0%80%EC%A0%B8%EC%98%A4%EA%B8%B0)
	1. [6) '배포' 코드 작성](#6-%EB%B0%B0%ED%8F%AC-%EC%BD%94%EB%93%9C-%EC%9E%91%EC%84%B1)
	1. [7) 컨트랙트 배포 누르고 -> 메타마스크에서 확인 누르기](#7-%EC%BB%A8%ED%8A%B8%EB%9E%99%ED%8A%B8-%EB%B0%B0%ED%8F%AC-%EB%88%84%EB%A5%B4%EA%B3%A0---%EB%A9%94%ED%83%80%EB%A7%88%EC%8A%A4%ED%81%AC%EC%97%90%EC%84%9C-%ED%99%95%EC%9D%B8-%EB%88%84%EB%A5%B4%EA%B8%B0)
	1. [8) 완료된 컨트랙트의 CA 주소 가져오기](#8-%EC%99%84%EB%A3%8C%EB%90%9C-%EC%BB%A8%ED%8A%B8%EB%9E%99%ED%8A%B8%EC%9D%98-ca-%EC%A3%BC%EC%86%8C-%EA%B0%80%EC%A0%B8%EC%98%A4%EA%B8%B0)
1. [2. 리액트 환경에서, 배포, Counter 1 증가 및 감소 및 송금 해보기  (feat_메타마스크)](#2-%EB%A6%AC%EC%95%A1%ED%8A%B8-%ED%99%98%EA%B2%BD%EC%97%90%EC%84%9C-%EB%B0%B0%ED%8F%AC-counter-1-%EC%A6%9D%EA%B0%80-%EB%B0%8F-%EA%B0%90%EC%86%8C-%EB%B0%8F-%EC%86%A1%EA%B8%88-%ED%95%B4%EB%B3%B4%EA%B8%B0--feat_%EB%A9%94%ED%83%80%EB%A7%88%EC%8A%A4%ED%81%AC)



# 🔹 react 에서 '스마트 컨트랙트 배포', 'Counter 1 증감' 및 '송금' 해보기 (app.js 파일 참고)

## 0. 포인트 
``` bash
[js 버전과 다른 점]
- 리액트 셋팅 
- ⭐⭐ '메타마스크 인터페이스' 를 통해 '이더리움 네트워크' 와 '통신' 하는게 포인트 ⭐⭐
```


## 1. 리액트 환경에서 '배포' (및 '배포한 컨트랙트 실행' 프로세스 요약)

``` bash 
[리액트 초기 셋팅]
- [[230710_084417_리액트_3주차#2. 초기 셋팅]] 참고 

- 라이브러리 설치  : web3
	npm i web3


[메타마스크 인터페이스를 통해 이더리움 네트워크과 통신해서 배포하기]
1. 터미널에서 ganache-cli 실행 👉 '비밀키(private keys)' 발급 👉 메타 마스크 내의 '이더리움 계정' 생성하기 

2. '메타마스크에 접속한 계정' 의 '이더리움 주소' 가져와서 연동하기 ⭐⭐⭐ 

3. solidity 파일에 내용 작성 

4. 해당 파일 컴파일 하기 
	$ npx solc --bin --abi Counter_React.sol

5. 배포 코드 작성 

6. 컨트랙트 배포 누르고 -> 메타마스크에서 확인 누르기

7. 완료된 컨트랙트의 CA 주소 가져오기

```



### 0) 지금 어떤 일이 벌어지는지 이해하기 

``` bash
- javascript 환경에서는, web3 라이브러리를 사용할 때, 
	const web3 = new Web3("http://127.0.0.1:8545") 이렇게 연결했음. 
	> 8545 포트는 ganache 가 주로 실행되는 포트 임. 
	> 따라서, 위 코드는 로컬로 연결된 ganache 가 8545 포트를 통해, web3 라이브러리를 거쳐서, 이더리움 네트워크와 통신한다는 말 임. 

- 이제, web3 라이브러리를 사용하는 건 동일한데, '메타마스크 안에 있는 ganache 환경' 을 사용하게 된다. (이전에는 '로컬 ganache' 였지) ⭐⭐⭐ 

그러면, 
	1) 'ganache 환경' 을 쓴다는 건? 👉 메타마스크에서 'ganache 네트워크' 를 선택 하면 되고 
	2) web3 라이브러리를 쓴다는 건, 
		'setWeb3(new Web3(window.ethereum));'  이렇게 함으로써 
			a) 'window.ethereum' 안에 들어가 있는 '이더리움 호환 웹3.0 지갑' 중 하나 인 '메타마스크' 를 
			b) Web3 라이브러리에 넣고 
			c) setWeb3 에 의해 -> web3 변수에서 꺼내쓸 수 있다는 말 임. 

- 결국, 
	- 코드 상 Web3 의 매개변수로, 'ganache 포트' 가 들어가는 건 동일한 듯 하고 (추측임) 
	- 다른 점은 메타마스크를 사용할 경우, 메타마스크가 설치되어 있는 window.ethereum 객체 자체를 넘긴다는 것
```



### 1) 터미널에서 ganache-cli 실행 👉 '비밀키(private keys)' 발급 👉 메타 마스크 내의 '이더리움 계정' 생성하기 

``` bash
[주의 ⭐] 
	- 메타마스크 인터페이스 안에 있는 ganache 채널을 통해 이더리움 네트워크와 통신하는 것 임. -> 따라서, ganache 는 계속 켜져 있어야 함. 
	- 그런데, 컴퓨터를 재부팅 하면, ganache 는 다시 재부팅 됨 -> 그러면, 다시 privateKey 로 계정 만들어줘야 함 ⭐⭐⭐ (살짝 번거롭지만 어쩔 수 없음.)
```

1. `ganache-cli` 한 후 👉 private Keys 하나 가져오기 
![](https://i.imgur.com/eLFF4Zv.png)


2. '메타마스크' 에서 계정 생성하기 

![](https://i.imgur.com/McjSumc.png)
![](https://i.imgur.com/QAd4wqQ.png)
![](https://i.imgur.com/sIcl8Cs.png)


- 메타마스크로 만든 이더리움 지갑의 계정 가져온 것 확인하기 
![](https://i.imgur.com/DDNKiYs.png)








### 2) '메타마스크에 접속한 계정' 의 '이더리움 주소' 가져와서 연동하기 ⭐⭐⭐ 

- 메타 마스크 내에서 계정 선택 
```
아래 지구본 클릭 -> 원하는 계정으로 전환하면 됨
```
![](https://i.imgur.com/TmhL3h6.png)


- web3 라이브러리 통해서 이더리움 주소 확인하기 
``` js
  useEffect(() => {
    (async () => {
      // '⭐이더리움 계정 주소' 가져오기 | '⭐지갑 주소 아님'
      const [data] = await window.ethereum.request({
        method: "eth_requestAccounts",
      });
      /* [이 과정 이해하기] 대체, 왜, 이렇게 하면, 지갑 주소 라는게, 뽑혀 나오는거지 ?
            1. 메타마스크에 가입한다. 그러면, 자동으로 '주소가 생성' 된다. 
              1.1 비밀키 생성 : 랜덤으로 privateKey(개인키) 가 생성된다. 
              1.2 공개키 생성 : 해당 프라이빗 키를 사용해서, publicKey(공개키) 가 뽑힘
              1.3 주소 생성 : publicKey(공개키) 중 일부를 추출해서, 'Ethereum 주소' 로 생성
            
            2. await window.ethereum.request({ method : "eth_requestAccounts" }) 이해하기 
              - window.ethereum : 메타마스크 등의 '이더리움 호환, 웹 3.0 지갑' 을 설치하면, 해당 정보가 window.ethereum 객체로 들어간다.
              - request({method : "eth_requestAccounts" }) : 현재 활성화 되어 있는 '⭐이더리움 계정 주소⭐' 를 달라고 요청

            3. '이더리움 계정 주소' 와 '지갑 주소' 의 차이 이해하기 
              - 여기에서 말하는 '이더리움 계정 주소' 는 '비밀키 > 공개키 > 주소' 로 생성된 것. 
              - 메타마스크는 이렇게 생긴 '주소' 및 '개인키' 를 안전하게 관리함. 
              - 메타마스크 지갑 1개 안에는 '다양한, 하위, 이더리움 계정' 이 있을 수 있음. 
                - 이것들 중, 미리, 메타마스크에서 선택해 놓으면 -> 해당 '이더리움 계정' 을 받게 됨. 
      */

      console.log("메타마스크 내 이더리움 계정 중 현재 로그인된 계정 주소", data);
      /* [이 과정 이해하기]
          - 만약, '지갑 내 다른 이더리움 계정' 으로 연결하고 싶으면, 
            1) 메타 마스크 클릭 2) 상단에 있는 계정 선택에서, 다른 계정 선택하고 들어가면 됨. 
          - 만약, '지갑 내 다른 이더리움을 생성 계정' 하고 싶으면, 
            1) ganache-cli 하고 2) privateKey 가 나오게 되는데 이걸 3) 메타마스크 중 계정 선택 항목에서 '계정 가져오기' 누르면 됨.
        */

      // web3 라이브러리 이용해서 이더리움 네트워크와 연결 ⭐
      setWeb3(new Web3(window.ethereum));
      /* [이 연결 이해해보기]
          'index.html' 에서는 const web3 = new Web3("http://127.0.0.1:8545") 이렇게 연결 
          그 결과, '로컬에서 실행되는 ganache' 가 'web3' 를 통해 '이더리움 네트워크' 와 연결

          지금, 리액트 버전에서는, window.ethereum 안에는 이더리움과 호환되는, 웹3 지갑들이 있음. (이 객체의 내부 정보를 사용해서, 이더리움 네트워크와 연결)
          그 결과, 'web3(setWeb3 의 결과물인)' 는 'window.ethereum 안에 있는 메타마스크의 인터페이스'를 통해 web3 라이브러리를 거치게 되고 -> 그 결과, '이더리움 네트워크' 와 연결
        */

      setAccount(data); // 현재 연결된 계정 주소를 account 에 저장
    })();
  }, []);


```
![](https://i.imgur.com/Bm7MznC.png)






### 3) solidity 파일에 내용 작성 
``` solidity 
// SPDX-License-Identifier:MIT  
pragma solidity ^0.8.13;

contract Counter_React {
    uint256 value;

    constructor(){}

    function setValue(uint256 _value) public {
        // 상태 변수 변경 
        value = _value;
    }

    function getValue() public view returns(uint256) {
        return value;
    }

}
```



### 4) 해당 파일 컴파일 하기 
``` bash 
- 디렉토리 위치 : 해당 solidity 파일이 있는 곳 
	> typescript/kga/230925_솔리디티_스마트컨트랙트 (master) 

- solc 로 컴파일 하기 
$ npx solc --bin --abi Counter_React.sol
```

- 컴파일 결과 
![](https://i.imgur.com/zIdkYb3.png)



### 5) 컴파일된 결과물인 bin 파일 값을 가져오기
![](https://i.imgur.com/cnrJQN7.png)



### 6) '배포' 코드 작성 

``` js
// 상태 관리 
	  const [web3, setWeb3] = useState(null);  // web3 라이브러리를 상태로 관리
	  const [account, setAccount] = useState(null); // 계정 주소 | 가스비 지불할 계정
	  const [receiveAccount , setReceiveAccount] = useState("0x4148D6cE5e7B7A901Ff7fe7b3c90d97bFa97A15e")   // 송금시 받는 주소
	  const [balance, setBalance] = useState(); // 계정 잔액
	  const [gasUpperLimit, setGasUpperLimit] = useState("300000"); // 사용할 gas 상한선
	  const [moneyToSend , setMoneyToSend] = useState()   // 송금할 금액
	  // ⭐⭐ solidity 로 작성하고 -> 컴파일 해서 -> bin 을 여기에 붙여넣기
	  const [contractValue, setContractValue] = useState("solidity 파일에 적고 컴파일한 bin 파일을 여기에 넣기"  ); // 컨트랙트에 넣은 data



  // 스마트 컨트랙트 배포 (트랜잭션 생성)
  const sendTransaction = () => {
    // 배포할 계정 | 가스비 낼 계정
    console.log("현재 가스비 낼 계정 = 트랜잭션 배포할 계정 : ", account);

    // 사용할 가스 상한선
    console.log("사용할 gas 상한선", gasUpperLimit);

    // 컨트랙트로 배포할 data | ⭐⭐ solidity 로 작성하고 -> 컴파일 해서 -> bin 을 여기에 붙여넣기
    console.log("배포할 data", contractValue);

    web3.eth
      .sendTransaction({
        from: account, // ⭐⭐⭐ 컨트랙트 배포자 계정 | 컨트랙트 배포할 때 수수료지불할 계정 | 여기에 web3 를 통해 가져온 계정이 들어간다. ⭐⭐⭐ 
        gas: 300000, // 가스 상한선
        data: contractValue, // 컨트랙트 내용이 컴파일 되고 -> 바이트 코드로 들어감 | ⭐⭐⭐ 여기에 컴파일된 bin 내용이 들어간다. 
      })
      .then(receipt => {
        console.log("스마트 컨트랙트 영수증" , receipt)
        setContractAddress(receipt.contractAddress)
        console.log("CA 설정 완료" , contractAddress)
      });
  };

return (
      {/* 컨트랙트 배포 */}
      <button onClick={sendTransaction}>컨트랙트 배포</button>
      )
```




### 7) 컨트랙트 배포 누르고 -> 메타마스크에서 확인 누르기 

![](https://i.imgur.com/eDe33oO.png)





### 8) 완료된 컨트랙트의 CA 주소 가져오기 
```
스마트 컨트랙트가 발행되면, 
contract address 가 발행된다. 
이 부분을 꼭 갖고 있어야 한다. 
```

![](https://i.imgur.com/KemoIWI.png)












## 2. 리액트 환경에서, 배포, Counter 1 증가 및 감소 및 송금 해보기  (feat_메타마스크)
``` bash 
1️⃣ [메타마스크 통해 리액트 & 브라우저 연결]
	1. 크롬에서 메타마스크 미리 로그인 해두기 


	2. VS CODE 에서 ganache 에 연결해두기
		npm i ganache-cli        #ganache 설치 | 보통 전역으로 설치해서, 문제는 없을 수도.
		ganache-cli        #ganache 실행 


	3. (필요하면) ganache-cli 실행해서 받은 '비밀키' 로 메타 마스크 내의 '이더리움 계정' 생성하기


2️⃣ [메타마스크 통해 계정 잔액 확인]
	1. 메타마스크로 만든 이더리움 지갑의 계정 가져오기 
		  // '⭐이더리움 계정 주소' 가져오기 | '⭐지갑 주소 아님' 
			  const [data] = await window.ethereum.request({
				method : "eth_requestAccounts"
			  })

		- 이해하는 과정 👇👇 
				- 근데, 그러면, '지갑' 을 만든다는 건, '블록으로 지갑을 만들었던 때' 가 있었잖아? 그것과 동일한건가?  👉 응. UTXO 모델로, 지갑 생성, 보상 주는 예제를 했었어. 그때의 지갑과 아무래도 비슷할거야 참고 : [[230921_이더리움_솔리디티]]
				- 그러면, '지갑' 이라는 건, 구체적으로 뭘 의미해? #❓ (아직 부족함... 지갑, EOA, CA 등에 대한 이해가 부족. 특히, UTXO 모델을 다시 해볼 필요가 있음.)
			
			CF. 메타마스크에서 이더리움 지갑 주소가 생성되는 과정  
			0) 메타마스크에 가입한다. 
			1) 비밀키 생성 : 랜덤으로 privateKey(개인키) 가 생성된다. 
			2) 공개키 생성 : 해당 프라이빗 키를 사용해서, publicKey(공개키) 가 뽑힘
			3) 주소 생성 : publicKey(공개키) 중 일부를 추출해서, 'Ethereum 주소' 로 생성
			4) 이렇게 생성된 'Ethereum 주소' 가 const [data] = await window.ethereum.request({
		        method : "eth_requestAccounts" }) 를 통해, 반환된다. 
				      
	2. 'web3' 변수를 'window.ethereum 안에 있는 web3 지갑인 메타마스크 인터페이스' 에 연결시켜서 -> web3 라이브러리를 거쳐서 -> 이더리움과 통신하게 될 예정.  
      setWeb3(new Web3(window.ethereum))


	3. web3 가 갖고 있는 'window.ethereum' 안에 있는 '지갑의 API' 를 통해, 잔액 가져오기 


3️⃣ [리액트에서 컨트랙트 배포 하기 : 상태 변수에 counter 변수 만들고, 증감 시켜보기]

	1. soldity 파일로 상태 변수에 들어갈 내용 작성 
			// SPDX-License-Identifier:MIT  
			pragma solidity ^0.8.13;
			contract Counter_React {
			    uint256 value;
			    constructor(){}
			    function setValue(uint256 _value) public {
			        // 상태 변수 변경 
			        value = _value;
			    }
			    function getValue() public view returns(uint256) {
			        return value;
			    }
			}

	2. 컴파일 하기 
		# solc 로 '컴파일' ⭐⭐⭐
		- npx solc --bin --abi '파일의 경로'
		- ex) npx solc --bin --abi Counter_React.sol

	3. bin 확장자에서, 컴파일된 결과값 가져와서 -> 리액트 파일에 넣어주기 
			  const [contractValue , setContractValue] = useState("요기에 bin 복붙")   // 컨트랙트에 넣은 data

	4. 버튼 클릭했을 때, 'web3.eth.sendTransaction' 메소드 실행되도록, 필요한 매개변수 준비하고, 실행시키기. 
		web3.eth.sendTransaction({
	      from : account, 
	      gas : gasLimit, 
	      data : contractValue, 
	    }).then(console.log)
	
		- 특히, 
			- 'from : account' 는, 'window.ethereum.request' 로 확인한, '현재 연결된 이더리움 계정 주소' 가 들어가야 함  
			- 'data : contractValue' 는 'solidity 작성 -> solc 로 컴파일 -> bin 파일의 결과값' 이 들어가야 함 ⭐ 


	5. 배포하게 되면, CA 가 나옴 ⭐⭐⭐ 
		- "0xd7608c4ca796b240decb60586d621898f7ea965f"
			- 이건, 지금 발생시킨 스마트 컨트랙트의 주소가 된다.❓❓ | 이 의미를 좀 더 공부할 필요 
			- CA 가 있으니까 -> 이더리움 네트워크 내에 '영구 저장된 값' 에 접근할 수 있어 


	6. 현재 CA 의 'value(영구 저장 storage, 상태 변수)' 에 어떤 값이 있는지 확인해보기 | solidity 로 작성된 'getValue' 를 사용해야 함 👉 so, abi 를 가져와서, 컨트롤 해야 함. 

		1) abi 을 useState 사용해서 넣어주기 
		2) index.html 에서 getValue 함수를 참조해서 기재 ⭐⭐ 
					  // 상태 변수 에 값이 얼만큼 있는지 확인해보기 
							  const getValue = async () => {
							
							    // 1. solidity 파일에 적은 getValue 함수를 hash 화 시키기             
							    const getValueFuntionHash = web3.eth.abi.encodeFunctionCall(abi[1] , [])
							    console.log("abi[1] 인 getValue 함수를 hash 화 시키기 : " , getValueFuntionHash)
							
							    // 2. hash 화 된 getValue 함수를 web3 라이브러리를 통해 EVM 으로 넘겨서 '상태변수인 value' 값 가져오기
							    const data = await web3.eth.call({
							      to : "0xd7608c4ca796b240decb60586d621898f7ea965f" , 
							      data : getValueFuntionHash,
							    })
							
							    console.log("상태변수인 value 값 가져오기 : " , data)
							
							    // 3. 받아온 16진수 상태변수를 10진수로 
							    // const result = await web3.utils.toBN(data).toString(10) | 원래 코드는 이건데 아래껄로 바꿔도 되겠지❓❓ 
							    const result = parseInt(data , 16).toString(10)   
							    // console.log("10진수로 변화한 상태변수" , result)
							
							    // 4. 렌더링 위해 setStorageValue 에 넣어주기 
							    setStorageValue(result)
							  }
				  // 상태 변수 에 값이 얼만큼 있는지 확인해보기
					  const getValue = async () => {
					    // 1. solidity 파일에 적은 getValue 함수를 hash 화 시키기
					    const getValueFuntionHash = web3.eth.abi.encodeFunctionCall(abi[1], []);
					    console.log("abi[1] 인 getValue 함수를 hash 화 시키기 : " , getValueFuntionHash);
					
					    // 2. hash 화 된 getValue 함수를 web3 라이브러리를 통해 EVM 으로 넘겨서 '상태변수인 value' 값 가져오기
					    const getValueData = await web3.eth.call({
					      to: contractAddress,    // 스마트 컨트랙트 배포되면, receipt 를 통해, 바로 CA 가져오기
					      data: getValueFuntionHash,
					    });
					
					    console.log("상태변수인 value 값 가져오기 : ", getValueData);
					
					    // 3. 받아온 16진수 상태변수를 10진수로
					      // 3.1 web3.utils.toBN 사용
					      // const getValueDataResult = await web3.utils.toBN(getValueData).toString(10)
					      // | 원래 코드는 이건데 아래껄로 바꿔도 되겠지❓❓
					
					      // 3.2 js 에서 변환
					      const tempGetValueDataResult = parseInt(getValueData, 16).toString(10);
					      console.log("10진수로 변화한 상태변수", tempGetValueDataResult);
					
					      const getValueDataResult = isNaN(Number(tempGetValueDataResult))
					        ? parseInt(0)
					        : tempGetValueDataResult;
					      console.log("10진수로 변화한 상태변수", getValueDataResult);
					
					    // 4. 렌더링 위해 setStorageValue 에 넣어주기
					    setStorageValue(getValueDataResult);
					    return Number(getValueDataResult);    // setValue 에서 바로 사용하기 위해 숫자화 시켜줌
					  };


	7. '증가' 버튼 누르면, 'value(영구 저장 storage, 상태 변수)' 의 값 '1 증가'  시키기 ('감소' 버튼 누르면, 'value(영구 저장 storage, 상태 변수)' 의 값 1 감소 시키기 ))
		- index.html 에 있는 setValue 참고 ⭐⭐
		- 함수 하나로 만들고, 매개변수를 다르게 넣어주면 됨.

		- setValue 정의 
				// setValue 로, 이더리움 네트워크에 저장되어 있는 상태 변수 변경
				  const setValue = async ( setNumber ) => {
				    
				    // 1) 현재 상태변수(이더리움 storage) 에 있는 값 가져오기
				    const _getValue = await getValue();
				    
				    console.log("setValue 에서 getValue값", typeof(_getValue));
				
				    // 2) solidity 파일에 적은 setValue 함수를 hash 화 시키기
				    const setValueFuncHash = await web3.eth.abi.encodeFunctionCall(abi[2], [Number(_getValue+setNumber),]);
				
				    // 3) 컨트랙트 배포자(수수료 지불할 계정) 있는지 확인
				    if (!account) return alert("가스비 낼, 컨트랙트 배포자 필요함!");
				
				    // 4) 트랜잭션 | storage 데이터를 어떻게 변경할지
				    const tx = {
				      from: account, // 트랜잭션 발생 시키는 계정
				      to: contractAddress, // 누가 받았나 CA 계정 주소 | 스마트 컨트랙트 배포되면, receipt 를 통해, 바로 CA 가져오기 
				      data: setValueFuncHash, // solidity 파일에 적은 hash 화된 파일. setValue 함수,
				      gas: 500000, // 1) 정확히 얼마의 gas 가 쓰일지는 모름 2) 사용할 gas의 upperLimit
				      gasPrice: 100000000, // gas 당 얼마의 price 를 지불할 건지 | 너무 낮으면,
				    };
				
				    // 5) web3 라이브러리를 통해, sendTransaction 메소드 실행 시키기
				    const data = await web3.eth.sendTransaction(tx);
				    console.log(
				      " setValue 함수를 abi 로 컨트롤 해서, storage 데이터를 변경시킨 트랜잭션 결과 ",
				      data
				    );
				  };

		- setValue 실행
		      {/* 상태변수 값 증감 */}
		      <button onClick={() => setValue(1)}> storage 에 있는 값 1 증가 시키기 </button>
		      <button onClick={() => setValue(-1)} > storage 에 있는 값 1감소 시키기 </button> <br/>


	9. 송금 하기 
			  // 송금하기 
			  const sendWei = async () => {
			
			    try {
			      console.log("송금할 금액 , ether" , moneyToSend)
			
			      // 이더를 wei 로 변환
			      const weiToSend = Number(web3.utils.toWei(moneyToSend.toString() , 'ether'))
			      console.log("송금할 금액 , wei" , weiToSend)
			  
			      const receipt = await web3.eth.sendTransaction({
			        from : account,   // 돈을 낼 계정 | 가스비 지불할 계정
			        to : receiveAccount,    // 송금시 돈 받을 계정 
			        gas : 300000,     // 가스 상한선 | 해당 연산에 사용할 최대 가스 
			        value : weiToSend    // 송금할 금액 | 😥😥 이걸 어케 가져오지
			      })
			      console.log("트랜잭션 영수증" , receipt)
			      
			    } catch (error) {
			      console.log(error)
			    }
			  }
```


--- 




