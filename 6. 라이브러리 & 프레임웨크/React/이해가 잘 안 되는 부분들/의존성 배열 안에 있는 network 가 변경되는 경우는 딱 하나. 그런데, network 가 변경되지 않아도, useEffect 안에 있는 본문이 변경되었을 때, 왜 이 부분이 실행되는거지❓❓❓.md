
- 관련 프로젝트 : [[231010_혼자서 해보기_리믹스 & 리액트_배포 및 송금#의존성 배열 안에 있는 network 의 변화가 없음에도, 왜 해당 useEffect 가 작동하는거지 ⭐⭐⭐]]
``` JS
  useEffect( () => {
    // 이벤트 등록 | 네트워크가 변경되면, 발생하는 이벤트 등록 | 이벤트가 변경되면 -> 메타마스크 가 호출 
    window.ethereum.on("chainChanged" , (chainId) => {
      console.log("네트워크가 변경 되었음!" , chainId)

      // 0x539 (가나쉬 네트워크 체인 id | 가나쉬에 접속할 때, npx ganache-cli --chain.chainId 1337 --chain.networkId 1337 | 여기에서 1337 == 0x539) 
      if(chainId == '0x539'){
        getAccounts()
      }

    })
      // 변경된 chainId 가 뭔지 , 발생하면 -> 매개변수에 해당 체인 id 가 들어감 
    
    // 지갑이 변경되면, 실행할, 이벤트 등록 
    window.ethereum.on("accountsChanged" , (account) => {
      console.log("지갑이 변경 되었어!"); // 지갑 변경하면, 호출됨. 
      getAccounts()
    });

    if(!ERC20Contract) return;
    // 컨트랙트 인스턴스가 있으면 실행시키지 말고, 네트워크가 정상적일 때, 실행시켜도, 되겠다.
      // 네트워크가 정상적이면 실행 시킬 것 
      getAccounts()
  } , [network])


  // 0x539 1337 우리가 지정한 가나쉬 chainId
  const switchNet = async () => {

    // 메타마스크에 해당 네트워크로 변경해달라고 요청 | ⭐ 성공적으로 변경하면 null 을 반환하게 됨 ⭐
    const net = await window.ethereum.request({ 
      jsonrpc : "2.0" , 
      method : "wallet_switchEthereumChain",    // wallet_switchEthereumChain : 'params 에 넣은 네트워크로, 변경을 요청' 하게 하는 메소드
      params : [{chainId : "0x539"}]    // 0x539 == 1337 == ganache 실행할 때, 해당 체인ID 로 기재했음 -> 따라서, 가나쉬로 바꿔 달라는 말 
    })
      // wallet_switchEthereumChain : 체인 아이디가 맞는지 확인 | 매개변수로 전달한 체인 id 가 맞는지 확인 ⭐⭐⭐ 
      // ⭐⭐ 체인 아이디 = 네트워크 식별자 임. ⭐⭐ | 가나쉬에 체인 아이디를 던지면 -> 오캐이고, 안 되면, 접속할 수 있게

    // net 값이, 정상적으로 없으면(null 이면), 해당 네트워크에, 있다는 뜻! 
    setNetwork(net || true);    
      /* [관련 문법] 논리 OR 연산자
        const result1 = true || false;   // result1은 true
        const result2 = false || true;   // result2도 true
        const result3 = null || "Hello"; // result3은 "Hello"
        const result4 = "" || 0;         // result4는 0     */
      // [의미] net 값이 있으면 그 값을 사용하고, 없으면 true를 사용하라
      // [해석] 한번 네트워크 검사하기 위한 것 ✅✅    
  };
  
```