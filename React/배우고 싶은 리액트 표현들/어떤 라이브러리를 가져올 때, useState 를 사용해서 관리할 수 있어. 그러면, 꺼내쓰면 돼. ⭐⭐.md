
``` js
function App() {
  
  // web3 라이브러리를 상태로 관리 
  const [web3 , setWeb3] = useState(null)
  const [account , setAccount] = useState(null)   // 계정 주소
  const [balance , setBalance] = useState(0)  // 계정 잔액


  useEffect( () => {
    ( async () => {

      // '⭐이더리움 계정 주소' 가져오기 | '⭐지갑 주소 아님' 
      const [data] = await window.ethereum.request({
        method : "eth_requestAccounts"
      })
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

      console.log("메타마스크 내 이더리움 계정 중 현재 로그인된 계정 주소" , data)
        /* [이 과정 이해하기]
          - 만약, '지갑 내 다른 이더리움 계정' 으로 연결하고 싶으면, 
            1) 메타 마스크 클릭 2) 상단에 있는 계정 선택에서, 다른 계정 선택하고 들어가면 됨. 
          - 만약, '지갑 내 다른 이더리움을 생성 계정' 하고 싶으면, 
            1) ganache-cli 하고 2) privateKey 가 나오게 되는데 이걸 3) 메타마스크 중 계정 선택 항목에서 '계정 가져오기' 누르면 됨.
        */

    // web3 라이브러리 이용해서 이더리움 네트워크와 연결 ⭐
      setWeb3(new Web3(window.ethereum))
        /* [이 연결 이해해보기]
          'index.html' 에서는 const web3 = new Web3("http://127.0.0.1:8545") 이렇게 연결 
          그 결과, '로컬에서 실행되는 ganache' 가 'web3' 를 통해 '이더리움 네트워크' 와 연결

          지금, 리액트 버전에서는, window.ethereum 안에는 이더리움과 호환되는, 웹3 지갑들이 있음. (이 객체의 내부 정보를 사용해서, 이더리움 네트워크와 연결)
          그 결과, 'web3(setWeb3 의 결과물인)' 는 'window.ethereum 안에 있는 메타마스크의 인터페이스'를 통해 web3 라이브러리를 거치게 되고 -> 그 결과, '이더리움 네트워크' 와 연결
        */

      setAccount(data)    // 현재 연결된 계정 주소를 account 에 저장

    }) ();
  } , [])

```


- 관련 프로젝트 
	- [[230925_블록체인_솔리디티_스마트컨트랙트배포#[메타마스크 통해 리액트 & 브라우저 연결] 이해하기]]



