

- 이 리액트 사용 문법 이해하기
``` js 
  useEffect(() => {
    (async () => {
      // 배열의 구조분해 할당
      // window
      console.log(window.ethereum);
      const [data] = await window.ethereum.request({
        method: "eth_requestAccounts",
      });
      console.log(data);
      // 0xBf79c9053F311b0C1689054c31850E4073305417
      // 현재 연결한 지갑의 주소
      // 네트워크 web3 연결
      setWeb3(new Web3(window.ethereum));
      setAccount(data);
    })();
  }, []);
```


- 즉시 실행 함수 예문
``` js 
(function() {
  console.log("This will run immediately!");
})();
```

- 관련 문법 
	- [[즉시 실행 함수]]



