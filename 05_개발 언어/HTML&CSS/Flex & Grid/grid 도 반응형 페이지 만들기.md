


### 만들고자 하는 gird 레이아웃 

![](https://i.imgur.com/V5zlqBJ.png)




<br>

### 숫자 비율지정 방식 

``` bash
- grid-template-columns : 1fr 2fr 1fr 
	- 문제점 : item 요소들 중 '버팅기는 요소' 가 있으면, 1fr 2fr 1fr 같이, 원하는 비율대로 나오지 않음 
	- 해결방안 : '버팅기는 요소' 가 있음에도, 원하는 비율대로 나오게 하려면, '%' 단위를 사용하는게 낫다. 

```


