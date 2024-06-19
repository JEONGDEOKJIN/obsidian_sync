```jsx
{/* 기존 코드  */}
{/* <Image
  src={
	isImgError
	  ? DEFAULT_IMG_SRC
	  : `${process.env.NEXT_PUBLIC_API_URL}${img_file_dto_list?.[0]?.img_url}`
	// : `${process.env.NEXT_PUBLIC_API_URL}${img_file_dto_list?.[0]?.img_url}` // [✅TODO] 이미지 링크 수정 필요
  }
  alt={`${category_name} 이미지`}
  fill
  className="object-cover object-top rounded-[10px]"
  onError={() => setIsImgError(true)}
/> */}

{/* 컴포넌트로 수정 | TODO: API 붙여보고, 실제로 나오는지 테스트 해봐야 함 | [0] 이런게 없어야 함. 왜냐면, 실제로 값이 0번째 배열에 없을 수도 있어 |  */}
<CustomImage
  src={`${process.env.NEXT_PUBLIC_API_URL}${img_file_dto_list?.[0]?.img_url}`}
  DEFAULT_IMG_SRC={DEFAULT_IMG_SRC}
  fill
  alt={`${category_name} 이미지`}
  className="object-cover object-top rounded-[10px]"
/>
```


내가 이렇게 생각해 낼 수 있어야 한다! 
으아악! 









