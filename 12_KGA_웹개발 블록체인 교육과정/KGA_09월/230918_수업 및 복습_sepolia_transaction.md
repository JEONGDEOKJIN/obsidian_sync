# 수업 
## 세폴리아 

### 세폴리아 얻기 

![](https://i.imgur.com/zXww5cN.png)



- 이걸로 세폴리아 얻기 
https://jerryjerryjerry.tistory.com/126



- 이거 이렇게 만들자 꼭 
![](https://i.imgur.com/e8WYCY9.png)





## 트랜잭션 


![](https://i.imgur.com/u2zN6YZ.png)


![](https://i.imgur.com/U9AxyJN.png)



- 사용하고 난 다음 
![](https://i.imgur.com/DpJu7rw.png)




![](https://i.imgur.com/BAl7jj4.png)






- 보내고 나면 이렇게 보낸 사람에게 찍히고 , 받는 사람에게도 찍힘
- 가스비는 네트워크가 바쁘면, 더 비싸게 나옴 
![](https://i.imgur.com/3YnmYUA.png)





    // 어떤 사람이 얼마를 받는 것에 대한

    // 트랜잭션 어떻고 -> 발생하면, in 에는 누가 누구에게 보내는게 있고

    // out 에는 마지막 UTXO 에 이는 내용이 있고

    UTXO 에는 미사용 객체가 있는것들



# 자습 

## 흐름도 
![](https://i.imgur.com/Ok5hULb.png)




- 우선, 이렇게 흐름 이해 했는데, 수정 필요 ㅠㅠ 


![](https://i.imgur.com/q6rJJEB.png)






- UTXO (Unspent Transaction Output)
```BASH 
UTXO 는 각 단어의 의미를 풀어서 쉽게 생각해보면 알 수 있다. 

'Unspent' 는 
	- 아직 '사용되지 않은' , '앞으로 쓰일 수 있는' 이라는 의미
	- 뒤에 나올 transaction 의 의미와 함께 생각해보면, 특정 디지털 화폐 거래가 발생한 상황에서, '지금 발생한 이 거래 이후에도 쓸 수 있는 돈' 을 가리키게 된다.

'Transaction' 은 
	- 발음상 TX 으로 합쳐지는 듯 하고 
	- '디지털 화폐' 의 '거래' 를 의미한다.
	- 쉽게 생각하면, 'A가 B에게 디지털 화폐를 전송하는 행위' 를 생각하면 될 것 이다. 

'Output' 은 
	- '소비되지 않은(거래에 쓰이지 않은) 돈의 양' 과 '그 돈의 주소(위치, 소유자)' 정보를 갖고 있음. 
	- 곰곰이 생각해보면, 'unspent 된 transaction' 은 'transaction 이 spent' 된 것과 비교해서 생각해보면, 
		- 'transaction' 자체는 spent 될 수 있는 대상 이고 
		- 누가 누구에게 돈을 주는 건, '전체 파이 안에서 유한' 하게 벌어지니까, spent 라고도 붙이는게, 적절하게 느껴진다. 
		- 그러면, '돈을 주고 받은 행위' 를 'spent transaction' 이라고 본다면, '잔고가 남아 있어서 돈을 주고 받을 수 있는 상황' 을 'unspent' 라고 보는 것 이고, 그 중 '필요한 정보를 output' 으로 뽑은게 '돈의 양과 주소(장소, 소유자)' 인 듯 하다. 


- 결국, UTXO 는 '디지털 화폐 트랜잭션' 을 '관리' 하는 방식 으로써, '현재 거래가 가능한 잔고의 양과 주소' 를 주로 다룬다.  
```



### 교수님 흐름으로 다시 TDD 해보기 

[[230918_내가이해한건데, 이렇게 말고, 교수님 흐름대로 코드 짜보고 - 그걸 토대로 UXTO 전체 이해하자 ]]

- [[230915_교수님흐름으로 다시 TDD 해보기]]







