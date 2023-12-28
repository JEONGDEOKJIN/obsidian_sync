``` js 

  // 스마트 컨트랙트 배포 (트랜잭션 생성)
  const sendTransaction = () => {
    // 배포할 계정 | 가스비 낼 계정 
    console.log( "현재 가스비 낼 계정 = 트랜잭션 배포할 계정 : " ,  {account})

    // 사용할 가스 상한선 
    console.log("사용할 gas 상한선" , gasLimit)

    // 컨트랙트로 배포할 data
    console.log("배포할 data" , contractValue)

    web3.eth.sendTransaction({
      from : account, 
      gas : gasLimit, 
      data : contractValue, 
    }).then(console.log)
  }

```
- 관련 프로젝트 
	- [[230925_블록체인_솔리디티_스마트컨트랙트배포#[메타마스크 통해 리액트 & 브라우저 연결] 이해하기]]

