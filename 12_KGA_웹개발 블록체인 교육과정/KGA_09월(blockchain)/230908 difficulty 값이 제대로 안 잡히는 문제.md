


# 오류
- 문제 상황
```
difficulty 값이 들어오는 로직이 문제 
```
![](https://i.imgur.com/8bLeSmu.png)


- 문제 되는 코드 👇👇
![](https://i.imgur.com/zpdgqHu.png)


- 왜 저기가 문제? 
![](https://i.imgur.com/hmYkMEh.png)


- 동적으로 지정된 포트 
	- 
![](https://i.imgur.com/vLYpCQh.png)



- 새로고침하면, 여러개 생김 
	- 계속 내용이 들어감 
![](https://i.imgur.com/z2HCFdz.png)




![](https://i.imgur.com/b5j68EJ.png)



```
http://172.25.176.1:8080/peer/add
```


<br>



# 다시 내용 파악하기 

- 지금 이게 뭘 테스트하는 파일이야? 
- 이걸 굳이 TDD 로 해야 하는 이유가 뭐야? 
- TDD 하려면, 어떤 과정을 거쳐야 해? 






## 해결 코드 

- 허무하게도, 이 부분, 오타 였음. 
![](https://i.imgur.com/otu52VJ.png)





# 잘 몰랐던 것 | 배운 것 | 😥😥😥 | 또 틀렸음 이걸 

```
우선, TDD 로 block.test.ts 파일 돌리려면, npm run test 로 돌렸어야 했음. 
```