

	
# [섹션 1] OT

## 피그마 특징 
``` bash
[피그마 특징]
- 동시접속

[우측 상단 탭]
- prototype 
	- 실제 구현되는 작동 되는 방식 
- inspect 
	- 스펙 볼 수 있는 것

- dev 모드 
```


- 우측 상단에 dev 모드 있음 -> 여기에서 Tailwind 사용할 수 있음. 
![](https://i.imgur.com/i32NFlq.png)

```
무브 툴은 space 누르면 가능
```



# [섹션 2] 피그마 시작하기 

## 피그마 기본 기능 및 단축키 

![](https://i.imgur.com/soaO3Bd.png)



### 피그마 기능 정리 1 
![](https://i.imgur.com/q1ujNB3.png)



- 되돌리고 싶을 때는 옆에 있는 버튼 클릭 -> 삭제하기 
![](https://i.imgur.com/dStn5ks.png)



### 피그마 정리 2 
![](https://i.imgur.com/EuEENGR.png)

### 피그마 정리 3
![](https://i.imgur.com/6Tv7YkX.png)




# [섹션 3] 와이어 프레임 만들기 

### [04] UI 요소 이해하기 

``` bash
- header 
	- 제일 윗 부분
	- 상단 붙어있는 것

- GNB 
	- general navigation bar : 일반적인 네비게이션 바 
	- 보통 헤더에 들어감 

- dept ⭐⭐
	- 첫 번째 페이지에서, 두 번째 페이지로 들어가면, dept 증가 

- toggle 
	- 열고 닫기만 할 수 있는 것

- Accodian
	- 토글 열면 나오는 부분 

- Floating Button 
	- 계속 따라다니는 버튼

- CTA 
	- 클릭을 유도하는 액션을 유도하는 버튼 

- side bar 
	- 검색 버튼 누르면 -> '옆에서' 나오는 경우 


```

![](https://i.imgur.com/aWFW4rJ.png)



### [05] 와이어 프레임 그리기 01 : 메인 페이지 (feat.아이콘 플러그인) 


```
와이어 프레임은 
디자이너가 기본적으로 디자인 하기 전에 나오는 단계 

그 전에, 기획이 나왔어야 함 
```


#### 플러그인 받기 
- 아이콘 플러그인 받으려면, 이쪽으로 우선 들어가기 
![](https://i.imgur.com/t1C9njr.png)


- feather icons
![](https://i.imgur.com/4dYzMBK.png)


- try it out 
![](https://i.imgur.com/6kWrOls.png)


- run 클릭 
![](https://i.imgur.com/EGXdEup.png)


- 왼쪽 상단에서 확인 가능 
![](https://i.imgur.com/tjatKuc.png)




#### 와이어프레임 만들 때 포인트 

1. '정렬하고자 하는 대상' 과 '정렬 배경' 을 '동시에' 잡아야 함 
![](https://i.imgur.com/Gl3unez.png)


2. stroke 속성을 center 로 하면, 겹침 현상 해결 가능 
```
혹은 화살표를 살짝 움직이거나 
```
![](https://i.imgur.com/NQVsxiZ.png)


3. 도형을 그려서, 이렇게 조절 가능 
![](https://i.imgur.com/YYoEDtI.png)

4. 서식 복사 
![](https://i.imgur.com/yxNWZbe.png)

5. 이전과 동일하게 복사 하려면 CNTRL D 
![](https://i.imgur.com/cNxHmGM.png)


6. 그룹 안에서, 글자만 선택하고 싶으면, cntrl 누르기 ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/NNHzOpZ.png)



### [06] 와이어 프레임 그리기 02 : 상세 페이지 (feat. 오토 레이아웃) 


- 겹친 선 살짝 내리려면, 화살표 아래로 or center 로 정렬시키기 


- 와이어 프레임 간격 요소 ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/TFn8OXK.png)



- ruler 로 가이드 라인 만들기 ⭐⭐⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/WRfOkXq.png)



- 20 간격 만큼 떨어진 ruler 지정 | ruler 사용할 때, 더미 박스 꼭 만들어서 사용 ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/3K8bbgd.png)




![](https://i.imgur.com/gsSTQ6t.png)


- 여러 객체 정렬할 때는 윗 부분
![](https://i.imgur.com/7AFx3sh.png)



- 이런 선을 만들 때는, box 를 많이 사용 함 ⭐⭐⭐ 
	- 스트로크 1로 줄여서 
![](https://i.imgur.com/HtW0v59.png)
![](https://i.imgur.com/PuNhRu9.png)


- 클릭할 때, 아이콘 말고, 파일 이름을 클릭해야 함 ⭐⭐⭐⭐⭐⭐⭐ 
	- 그래야 정렬 할 때, 오류가 안 남 ⭐⭐⭐⭐⭐ 



- 아이콘들이 내 마음에 안 들면, 변경이 가능해 ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/GmJP9At.png)



#### 정렬 시키려고 할 때 ⭐⭐⭐⭐⭐⭐ | 오토 레이아웃 때문에 겁먹었음 걱정안해도됨 이건 
```
auto layout 같은거 없음 

1.  '부모 요소의 크기' 안에서  '각 개체들' 이 차지하는 박스 크기로 정렬이 됨 
2. auto layout 없이, 상단에, distribute horizontal spacing 누르면 -> 정렬이 됨 

```


![](https://i.imgur.com/glIFclx.png)


![](https://i.imgur.com/nDBnZL8.png)


![](https://i.imgur.com/JjXt11w.png)





#### 얇은 선 그리기 
```
height 를 1 로 놓는게 중요함 ⭐⭐⭐⭐⭐ 
```

![](https://i.imgur.com/B2Y67oC.png)


#### 오토 레이아웃 맛보기 ⭐⭐⭐ 

``` BASH
[언제 쓰나? 어떤 느낌으로 받아들이면 되나?]
1. '자식 요소' 들을 감쌀 '부모 요소' 를 하나 만드는 느낌 
	- 그래서, 부모 요소 안에서, 자식 요소들이, 어떻게 배치 될 것 인가를 결정하는 느낌 
	- 그리고, 하나 감싸고, 그 다음 또 저네 

2. 뭔가, 플렉스를 쓰는 느낌. 부모 요소를 하나 만드는 느낌 

[순서]
1. 필요한 요소 '선택'
2. 'align' 기능으로 먼저 사전 정렬 
3. '2개 요소' 를 'group(ctrl + B)' 으로 묶기
4. 'auto layout' 클릭 


[포인트]
- 이런 경우, 오토레이아웃 쓰는구나 하는거 정도
- 오토레이아웃 하위 요소를 cntr c + v 하면 -> 자동으로 생겨남 ⭐⭐⭐⭐⭐⭐⭐ | 이걸 하려고 
- 글자 길어져도 -> X 는 안 움직임 ⭐⭐⭐⭐⭐ 

```



![](https://i.imgur.com/gygNHwQ.png)


![](https://i.imgur.com/hFQDgtS.png)


![](https://i.imgur.com/vKK9SJw.png)


![](https://i.imgur.com/PWNH1QU.png)



### [07] 와이어 프레임 그리기 03 : 검색탭 



#### 오토 레이아웃 기능 : 글자 길어져도 -> X 는 안 움직임 ⭐⭐⭐⭐⭐ 
```
- grid 기능이 들어간 듯 


[방법]
1. 포토샵 = 변동가능성이 있는 것의 범위를 넓혀주기 ⭐⭐⭐⭐⭐⭐⭐ 
2. 그리고 x 와 오토레이아웃으로 묶기 
3. 그러면, 포토샵에 글씨가 많이 들어와도, x 의 위치가 변경되지는 않음 ⭐⭐⭐⭐⭐⭐ 
```


![](https://i.imgur.com/f0wNtA8.png)





#### 간격 조절할 때, 이 사이에 '커서' 를 넣어서 조절할 수도 있음 
```
0. 각 요소를 group 으로 묶어줘야 함 
1. 드래그 해서 선택 
2. 빈공간 가면 -> 핑크색이 있음 -> 그걸로 클릭해서 이동 
```
![](https://i.imgur.com/PWV0h8c.png)



### [08] 오토 레이아웃 맛보기 

#### 오토레이아웃 포인트
```
오토 레이아웃 포인트 

[전제]
- 부모 요소 안에 자식 요소들이 있고, auto layout 켜져 있기

[기본]
- 하위 요소 중 하나를 잡고 -> 복사 붙여넣기 하면, 똑같이 들어감 

[응용]
- layout wrap 하면 -> 아래로 떨어짐 (grid 같은 역할)
- 중간 부분을 복붙했을 때, 아랫부분들이 여백 고려해서, 늘어남


[중간 부분을 복붙했을 때, 아랫부분들이 여백 고려해서, 늘어나게 하기]
1. 비율적으로, 늘어나게 하려면, '전체 부분 잡고' -> ⭐ 전체를 auto layout⭐ 잡아주기 
2. 그 다음 hug 설정 ⭐⭐⭐⭐⭐ 
3. 그 다음 복붙 해보기 


확장 가능한 형태로 만들기 위함 
```



- layout wrap 하면 -> 아래로 떨어짐 (grid 같은 역할)
![](https://i.imgur.com/2wE109I.png)



- hug 누르면, 가운데 부분을 넣었을 때, 밑에 부분들이 자연스럽게 간격 벌어짐
![](https://i.imgur.com/dCBBD9K.png)
![](https://i.imgur.com/snVRxDD.png)




#### 오토 레이아웃 정리 ⭐⭐⭐⭐⭐⭐ 


1. 기본 기능 
```
상위 요소 아래에 있는 하위요소를 복붙 했을 때, 똑같이 들어감.
```
![](https://i.imgur.com/jJk0g2e.png)




2. 문제점

2.1 동일한 row 인데, 글자 길이가 다르면 -> 그 만큼 밀리게 됨 
![](https://i.imgur.com/VM4wXcb.png)



2.2 row 는 추가 되는데, 아랫줄이 추가가 안 되어서 -> 겹치는 문제가 발생 

```
이상하게 들어가짐
```
![](https://i.imgur.com/6iYDcZT.png)






3. 해결  #오토레이아웃정리

3.1 '포토샵이 들어갈 수 있는 공간' 을 마련해서, 글자 크기에 따른 변동이 없게 하기 
```
[방법]
1. 포토샵 = 변동가능성이 있는 것의 범위를 넓혀주기 ⭐⭐⭐⭐⭐⭐⭐ 
2. 그리고 x 와 오토레이아웃으로 묶기 
3. 그러면, 포토샵에 글씨가 많이 들어와도, x 의 위치가 변경되지는 않음 ⭐⭐⭐⭐⭐⭐ 
```
![](https://i.imgur.com/f0wNtA8.png)


3.2 '늘어나 줬으면 하는 전체 부분' 을 '오토레이아웃' 으로 잡아서, 하나를 추가하면, 자동적으로 밀리게 하기 ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/snVRxDD.png)



























# [섹션 4] UI 기획안 작성 

### [09] UI 기획안이 뭔가요? 

``` BASH
- 전체 개발 단계
기획 -> 디자인 -> 개발 -> 런칭

- UI 기획안은 
	- '기획과 디자인의 중간 단계'
	- 디자이너가 그림을 붙이기 전 단계 
	- '와이어 프레임 형태' 에서 '기능 설명' 이 들어간 것 
		- EX) 이 버튼 누르면, 이렇게 된다, 

- UI 기획안에는 
	- 유저 플로우, 메뉴 구조 , UI 설계, 기능 명세서(누르면, 뭐가 나온다) 가 있어야 함 
	- 지금 하는 건 UI 설계 

- UI 기획안 종류
	1. 기능 명세서랑 비슷한 | 와이어 프레임 띄우고, 각각의 버튼 설명 
	2. FLOW 형태로 보여주기 | FLOW 중심으로 보여주기 
```

- 전체 개발 단계 중 UI 기획 안의 위치 
![](https://i.imgur.com/PV6l3Y2.png)


- UI 기획안 예시 ⭐⭐⭐⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/wS7y6B4.png)



### [10] 피그마 활용하여 기획안 만들기 



#### FLOW 그리는 플러그인 : AUTO flow ⭐⭐⭐⭐⭐ 

- 이거 다운 
![](https://i.imgur.com/H5gPsEa.png)


- 사용법 
```
auto flow 플러그인 켜놓고 
잇고 싶은거 shift 로 잡으면 -> 연결됨
```

![](https://i.imgur.com/hHMWRxT.png)



- 그러면, 어떤 설명을 하면 좋은가 ⭐⭐⭐⭐⭐ 
``` bash
- 디자이너가 어떻게 만들어야 하는지  
하트 색깔 채워지고, 숫자 올라감  
  
- 개발자가 이걸 어떻게 만들어야 하는지  
ex) 조회수가 많은 순으로, 카테고리 보여주기
```

![](https://i.imgur.com/rVnhIi8.png)

















# [섹션 5] 모바일 웹을 디자인 해보자 01 : 디자인 준비하기 

### [11] 컬러 스타일 만들기 | ✅ 우선 pass 


### [12] 텍스트 스타일 만들기 | 필요할 수도, 지금 텍스트 넣는 김에? 

```
다만, 완전히, 이걸 먼저 정해놓고 가지는 않음 

[디자인 시스템 만드는 방식]
- 먼저 정해놓고 -> 따라가는 방식 
- 만들어놓고 -> 그걸 기록하는 방식이 있지 않을까. 
	그러니까, 와이어프레임 잡을 때, 다 잡을 필요는 없다는 말 

```



### [13] 컴포넌트 활용해서, 버튼과 아이콘 구성 | ⭐⭐⭐⭐⭐⭐⭐⭐ 아이콘 컴포넌트는 '와이어프레임 단계' 에서 사용하면 편할 것 같음 

```
버튼의 경우는, 디자인 단계에서 만들면서, 확정되게 된다. -> 그걸 이제, 디자인 시스템에 넣게 된다. 
```




#### '컴포넌트' 사용법 

```
1. 파일 이름 앞에 '접두사' 넣기 
	1. 이름에 위계를 넣기 ⭐⭐⭐⭐⭐
		ex) button/big/able
		ex) button/big/disable
		ex) button/small/able
		ex) button/small/disable
		
2. 각각 컴포넌트 버튼 클릭

3. 묶고 나서 -> variants 로 묶기 ⭐⭐⭐⭐⭐⭐ 
```

- 공통 이름을 앞에 붙이기 
![](https://i.imgur.com/5r9M5u8.png)

- 컴포넌트 버튼 클릭
![](https://i.imgur.com/4YANGzO.png)


- 그러면, 같은 그룹 안에 있는 건, 변경해서 사용 가능 
![](https://i.imgur.com/0CkkTeE.png)


- variants 로 만들기 
![](https://i.imgur.com/tiFUhjJ.png)




### [14] 이미지 활용 | 이건 아직은, 필요는 없음. 






# [섹션 6] 모바일 웹을 디자인 해보자 01 : 컴포넌트와 오토레이아웃 활용하여 카드 UI 구성하기 

### [15] GUI 디자인 하기 01 : 컴포넌트와 오토레이아웃 활용하여 카드 UI 구성하기 

```
그럼 나도, 반복되서 사용되는게 있나? 
CARD? 
와이어프레임을 보고 한다고 생각 
처음에 너무 많은 걸 한다기 보다, 우선, 지금 아는 지식으로 하자
```













# [반응형] 페이지를 반응형으로 만들려면 

## 이슈 
- 단위를 rem? px? 
- media query? 

## 리소스 
- https://brunch.co.kr/@eddwardpark/13


## rem ? 
### rem 에 대한 오해 

### 1. 반응형을 할 때 rem 을 사용? 




### rem 을 사용해야 하는 이유 | 그런데, 반응형에서는 아닌거 같은데 

### 1. device 별로 사용되는 기본 폰트가 다름 -> 따라서, px 을 사용하면, 핸드폰에서는 상대적으로 큰 화면으로 보임 -> 사용자 경험 저하
https://brunch.co.kr/@eddwardpark/13
![](https://i.imgur.com/TynPw9F.png)


### 2. 브라우저 설정에서 '글꼴' 을 '크게' 변경하면 -> 그에 따라서 콘텐츠 들도 변경되어야 자연스럽게 보임. 하지만, px 로 변경하면, 이 변경에 반응하지 못 함. 

![](https://i.imgur.com/8EDH0Qb.png)





### 피그마에서 rem 설정법 

### 1. dev 모드 👉 css 👉 `rem` 으로 설정
![](https://i.imgur.com/dmUEw3T.png)






## max-width? vh? vw? %? 
### 피그마에서 max-width 설정하기
- https://youtu.be/rn71Y-Hjr00?t=1046



### 피그마에서 작업한 걸 어떻게 프론트로 가져와서 반응형으로 보여줄 것 인가는 좀 더 스터디가 필요

```
현재, 일일이 단위를 다 바꾸거나, 하는 방법 밖에 모르겠음...

우선, 피그마에서, 먼저, 패드 버전을 만들고 -> 그 다음에 그걸 반영해줘야 하는 거 잖아. 

```








# 피그마 리소스 

### 피그마 필수 플러그인 들 
- https://yozm.wishket.com/magazine/detail/2247/


# 🐣 중요한 점 정리 

### 오토 레이아웃 정리 ⭐⭐⭐⭐⭐⭐ 


1. 기본 기능 
```
상위 요소 아래에 있는 하위요소를 복붙 했을 때, 똑같이 들어감.
```
![](https://i.imgur.com/jJk0g2e.png)




2. 문제점

2.1 동일한 row 인데, 글자 길이가 다르면 -> 그 만큼 밀리게 됨 
![](https://i.imgur.com/VM4wXcb.png)



2.2 row 는 추가 되는데, 아랫줄이 추가가 안 되어서 -> 겹치는 문제가 발생 

```
이상하게 들어가짐
```
![](https://i.imgur.com/6iYDcZT.png)






3. 해결  #오토레이아웃정리

3.1 '포토샵이 들어갈 수 있는 공간' 을 마련해서, 글자 크기에 따른 변동이 없게 하기 
```
[방법]
1. 포토샵 = 변동가능성이 있는 것의 범위를 넓혀주기 ⭐⭐⭐⭐⭐⭐⭐ 
2. 그리고 x 와 오토레이아웃으로 묶기 
3. 그러면, 포토샵에 글씨가 많이 들어와도, x 의 위치가 변경되지는 않음 ⭐⭐⭐⭐⭐⭐ 
```
![](https://i.imgur.com/f0wNtA8.png)


3.2 '늘어나 줬으면 하는 전체 부분' 을 '오토레이아웃' 으로 잡아서, 하나를 추가하면, 자동적으로 밀리게 하기 ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/snVRxDD.png)
















# 🚀 알게 된 것 



- [오토레이아웃] 반복되는 패턴에서 반드시 사용 ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/fqEAJPR.png)


- [오토레이아웃] 이렇게 요소 간 중간을 잡고 늘리면, 간격 조절이 바로 된다 
![](https://i.imgur.com/YOpTmDF.png)



- 문제는 글자를 바꿀 때, 빈 간격이 비뚤 빼뚤 해진다는 점 ⭐⭐⭐ 
	- 이건, group 으로 묶고 -> 칸을 최대한 늘인다음 -> auto layout 을 걸어줘서 해결해야 한다 ⭐⭐⭐ 

![](https://i.imgur.com/GD0EjMH.png)








- [레이어 관리] 레이어를 일일이 지정해주지 않고, 밖으로 나갔다가, 들어오면, 레이어자 가동으로 지정된다. ⭐⭐⭐⭐⭐ 
![](https://i.imgur.com/06ms37E.png)






- 네이밍 
![](https://i.imgur.com/XDI6MtP.png)




- 선택할 때 '드래그' 해서 선택하면 -> 그룹으로 싹 잡힘 ⭐⭐⭐⭐⭐ 




- 어떤 frame 안에 들어가는지를 잘 알아야 함 
![](https://i.imgur.com/uiwcG9M.png)



- 픽셀 단위는 기본적으로 `8px` 단위 로 하기. 즉, ⭐8의 배수!⭐ 로 하기 
ex) 8의 배수로 


- 선이 겹치게 되는 부분이 있으면 -> 화살표 한번 눌러서 위로 가게 하면 됨 ⭐⭐ 


- autolayout 으로 버튼 만들기  
```
수강하기 쓰고  
cnrol g -> 빈 그룹! 을 만든다.  
오른쪽에 ‘auto layout’ 버튼 누른다.  
배경색 누르고 -> 검정으로 만들기  
글자를 control 로 선택하고 -> 색상을 변경한다.  
간격을 조정한다.
```
![](https://i.imgur.com/G87BLKo.png)




















