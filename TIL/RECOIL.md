```tsx

// 쪽지(메시지) 보내기 (POST)
export const usePostMessage = () => {
  const { errorHandler } = useErrorHandle();

  return useMutation(["postMessage"], async (body: IReqMessage) => {
    try {
      const { data } = await MypageService.postMessage(body);

      console.log("usePostMessage 서버 응답 data : ", data);
    } catch (error) {
      errorHandler(error);
    }
  });
};

```

이렇게 usePostMessage 가 정의되어 있는 상태에서

```
  const { mutate: postMessage } = usePostMessage();

```

이렇게 되면

두 번째 매개변수 함수가 mutate 가 되고

mutate 가 postMessage 가 된다