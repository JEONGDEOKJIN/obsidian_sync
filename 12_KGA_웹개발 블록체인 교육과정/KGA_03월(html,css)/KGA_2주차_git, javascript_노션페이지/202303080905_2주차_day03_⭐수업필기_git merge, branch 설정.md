
# <center> <b> 1️⃣ 이번 회차 학습 목표 (goal) </b> </center>
--- 

## 1. 배우고자 하는 것 


- header 사이 `<br>` 2개! -> 가독성 괜찮음!

<br>
<br>


<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-6995655056361596"
     crossorigin="anonymous"></script>
<ins class="adsbygoogle"
     style="display:block"
     data-ad-format="fluid"
     data-ad-layout-key="-fb+5w+4e-db+86"
     data-ad-client="ca-pub-6995655056361596"
     data-ad-slot="8096424356"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>



# <center> <b> 2️⃣ 해보기 </b> </center>  
--- 


## ◼ 요약 

> 20자 요약해보기 


```
- 브랜치 만들기 
git branch "생성할 branch 이름"
(브랜치 만들고 push 해주기 ✅)

- 브랜치 목록 확인
git branch 
git branch -a 

- 생성한 브랜치로 이동 
git checkout main
git switch "이동할 브랜치 이름"
(❓ checkout 과 switch 차이점❓)

- 이동한 브랜치에서 뭔가를 작성 -> 스테이징 -> 커밋 -> push
(블라블라)
git add .
git commit -m "커밋 내용"
git push origin _브랜치 이름_ ⭐⭐ (빼먹지말기)


- 저장소 병합 
1. main 으로 이동 (병합할 기준)
2. main 에서 commit 할 내용 확인 (commit 하려면, 뭔가를 작성해놓으면 된다.)
3. `git merge dev` 
(main 브랜치에서, dev 를 가져와서 병합하기 / main 으로 이동해 있어야 함)


- 깃헙 repository 에 push 하기 


- 생성한 브랜치 제거 
git branch -d "제거할 브랜치 이름"

- 기타 
1. 저장이 충돌될 때, 선택하는게 있네 음. 



```


<br>


## 브랜치 6번 만들고, 병합 해보면서, 느낀점 (WIL🤟)

### merge 전,후 충돌 표시


1) merge 전에, main 에서 적으면 -> 충돌 표시 남 -> 선택해주면 돼

2) merge 전에, 안 적으면 -> 충돌 표시 안남




--- 

[수업 내용]

### 10번 반복을 하면서 느끼는 것 

1. 위에 처럼 '프로세스를 요약' 해놓는다. 
2. 반복 해가면서, 어떤 말인지, 어떤 뉘앙스 인지, 내가 어떻게 적용할 수 있는지 파악해본다. 



### branch 를 생성하면, ==그 순간의 master 내용==이 전부 복붙 됨. 

그래서 새롭게 만들어진 branch 에서는, 별걸 하지 않아도, master 에서 만들어진게 복붙해서 들어가짐. 



### 협업 하는거 

#### 내가 다른 거 받아오기 ⭐⭐⭐ 
1. 로컬에서 원격저장소랑 "동일이름" 으로 branch 생성하기 -> 그래야 pull 을 받아올 수 있음. 
```
$ git branch jhdev
$ git checkout jhdev
```

2. pull 받아오기 
```
$ git pull origin jhdev
```

#### 내가 브랜치 만들어보기 

1. 로컬 브랜치랑 원격 저장소 브랜치랑 확인 
``` 
$ git branch -a

빨강 : 원격 저장소
흰색 : 로컬 저장소
```
![](https://i.imgur.com/NAnNchB.png)


2. 로컬 저장소로 이동해서 -> push 날려주기 

```
$ git checkout dj_dev_test
$ git push origin dj_dev_test
```


[결과물] 
![](https://i.imgur.com/ufAFbsW.png)


#### 내가 만든거 지우려면 

- `git 원격 브랜치 삭제` 로 검색해서 하기 
```
git push origin --delete dj_dev_test
```




--- 

## 수업 내용 필기 


### git 다시 해보기

  

1. 새 저장소 만들기

    git init

  

2. 터미널 git bash 열기

  

3. 파일 스테이징

`git add .`

  

4. 커밋 메시지 작성

`git commit -m "메시지 작업 내용"

  

5. git hub 원격 저장소 연결

`git remote add origin https://github.com/JEONGDEOKJIN/230308.git`

깃헙에 보면 나옴

  

6. push

  
  

### 브런치를 나누기

- 브런치는 저장소의 작업 공간

- master 는 최종 작업물,

- 다른 브런치를 만들어서, 다수가 협업할 때, 혹은 혼자 할 때,

- 작업 내용을 나눠서 ⭐⭐⭐ -> 최종 작업물로 병합!

<br>

- 1) master(v0.1) 를 만들어서 작업을 함 -> 2) dev 라는 브랜치를 만듦 -> 계속 dev 에서 작업 -> dev -> 그리고 master(v0.2) 로 병합

- 왜냐면, master 에는 '완벽한 파일' 만 올리려고 하는 것 ⭐⭐⭐

  

- 마스터에는 '버전' 을 붙인다. ⭐⭐

<br>

- master -> dev1, dev2를 각자 하고 있음 -> dev1 에 병합 (또는 dev2 에 병합) -> master 에 dev1 을 병합.

<br>

- 작업자 마다 따로 branch 를 파고, dev 작업 하는게 나음.

  

<br>

  

### 브랜치 목록 확인

- `git branch`

로컬 저장소의 브랜치 목록 확인

지금은 master 만 있음.

  

<br>

  

- `git branch -a`

원격 저장소와 로컬 저장소 브랜치 목록 확인

  

<br>

  

- 현재 선택되어 있는 branch 는 `* + 초록색 글씨` 로 나옴

  

<br>

  

### 브랜치 생성

- `git branch "생성한 branch 이름"`

  

<br>

  

### 생성한 브랜치로 이동

- `git checkout main`

    - 'main' branch 로 이동하겠다~!

  

- `git switch "이동할 브런치 이름"`

  

### 생성된 브랜치 제거

- `git branch -d "제거할 브랜치 이름"

    - 내가 이 브랜치에 있으면 안 지워짐

  
  

### 주의사항

1. 브랜치를 만들었으면, push 를 해서, 원격 저장소에 브랜치를 생성해야 함 ⭐⭐

  

### 저장소 벙합 merge

- `git merge dev`

master 로, dev 에서 작업한 걸 가져오기

  

- 만약, 충돌이 나면, 파일 보여주고 선택하게 한다. 📛📛📛

    - 그러면, 변경된거를 push 해줘야 함?

  
  

### 할거

dev push 하고

dev 파일 삭제

작업 공간이 서로 다름


## 미j니 과제 
브랜치 생성 병합 6개 해보기 








> 요약해보기 



<br>
<br>







<br>
<br>


# <center> <b> 🤯 팀 과제 </b> </center> 
--- 

## 내가 맡은 부분 

- https://kgaplan.oopy.io/

<br>

## 해보기 


## 자주 쓰게 되는 css 모음 

``` 
- 자식 태그가 부모 div 의 상하좌우 가운데로 오게하기 
@ 부모 div 의 css 에 붙이기 
display: flex;
align-items: center;
justify-content: space-between;


```



<br>


## 느낀점 (WIL🤟)
- 코드 스니펫만 요약해서 칠 수 있으면, 좋을 것 같음. (Git 했던 것 처럼)
- 위에 처럼 만들었으면, 10번 반복해서 써보고, 그 다음에 느낀점들을 기록하는게 필요. (정제되는 과정이 필요)

- class 이름 지을 때, area, frame, container 같은거, 어떤 규칙이 있지 않을까. 
- '효율적인 노가다' 를 하고 싶은데 ㅠㅠ 
- `em` 같은것도 좀 더 잘 이해하고 싶음. 노션에서 왜 그 단위를 썼는지도 알고 싶기도 함. 

- 여러개를 만들어주고 한꺼번에 변화하게 하는 테스트를 하면, 연장하는게 좀 더 쉬울거 같은데? ⭐⭐⭐⭐⭐ 

<br>

- 한줄 쓰기, 2줄 쓰기 각각 class 가 있으면 좋을거 같다는 생각
	- ![](https://i.imgur.com/bCVmxyg.png)
	- 이렇게 하나하나 다 해야 하는 건가. 

<br>

- 이런 '글자line 간의 간격' 을 바꾸려면? 
	- ![](https://i.imgur.com/Isuc7Fs.png)
	- 이건 publisher? 가 하는 영역인가? 

<br>

- 언제든 꺼내쓸 수 있게 만드는 느낌 ⭐⭐⭐⭐⭐ 

<br>
- ![](https://i.imgur.com/eAc5eTv.png)
``` css
.main_page_item_callout_box {
    width: 700px;
    height: 82px;
    background-color: rgb(238, 238, 199, 0.3)
    /* border: 3px solid black; */
    /* border-radius: 20px; */
}
```
- 이 부분인데, `border-radius` 로도 안 되는거 같은데 
- 우산 `style` 태그에 넣어두자.

<br>


- 이걸 padding, margin 으로 줄이는 법은 없나? 
- ![](https://i.imgur.com/fiH4zll.png)

<br>

- 글씨 크기 조절 하는 것들도 좀 더 효율적으로 딱 하는게 있을거 같은데 
	1. 애초의 것을 잘 잡았으면 -> 기존 것 보고, 가져와서 쓰면 된다. 
	2. 가로, 세로 높이가 동일하게 작동하는 것들이 있음. 변수화 하면 좋을거 같은데



<br>

- 요놈 소스를 못 찾겠네 
	- ![](https://i.imgur.com/JxOJGqC.png)


<br>

- bookmark bar 를 실제로 눌리는 버튼으로 만들려면? 
	- 우선은, 그냥... 만든다... div 로... 
	- ![](https://i.imgur.com/ZksMWaN.png)


<br>





# <center> <b> ✅ 추가로 해야할 것  </b> </center> 
--- 

- 

<br>
<br>

# <center> <b> 🤟 What i learned </b> </center>  
--- 
- git branch 작성 및 merge 병합을 6번 했다. 그러면서, 느껴지는게 있었다. 이 상태에서 git 관련된 책을 읽으면 좀 더 이론적인게 보완되지 않을까, 그런 생각도 든다. 
- `가운데로 오게 하기`, `000 해보기` 같이 반복할 때, 1번째 느낀 것과, 5번째 하면서 느끼는 것은 분명 다르다. ⭐⭐⭐⭐⭐ 
	- 완전히 이해하지 않더라도, 5번 반복하는 것. 그것이 먼저다. 
	- 5번 반복할 수 있게 요약해놔야 한다. ⭐⭐⭐⭐⭐ 
	- 이 수업에서 얻을 수 있는 건 그것. 
	- 좀 더 deep 한 이해는 추가적인 몫이다. 


 <br>
 <br>
 
<script async src="https://pagead2.googlesyndication.com/pagead/js/adsbygoogle.js?client=ca-pub-6995655056361596"
     crossorigin="anonymous"></script>
<ins class="adsbygoogle"
     style="display:block"
     data-ad-format="fluid"
     data-ad-layout-key="-fb+5w+4e-db+86"
     data-ad-client="ca-pub-6995655056361596"
     data-ad-slot="8096424356"></ins>
<script>
     (adsbygoogle = window.adsbygoogle || []).push({});
</script>
--- 
## 참고자료 
- KGA_경일게임아카데미_블록체인과정_WEEK01_HTML
--- 
