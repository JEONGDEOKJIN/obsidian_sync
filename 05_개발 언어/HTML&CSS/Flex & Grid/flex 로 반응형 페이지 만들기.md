
# 만들고자 하는 것 

### 1. 모바일 사이즈 (360x640 기준)
![](https://i.imgur.com/KpGJpfg.png)


### 2. PC 사이즈 (1920 x 1080 기준) 
![](https://i.imgur.com/jpMDI9j.png)


<br>

### 3. 클래스(컴포넌트) 구성 

![](https://i.imgur.com/cYFcrwp.png)

<br>

## ✅ 체크할 부분  
``` bash 
1. pc 사이즈면 1920x1080 으로 해도 되는건가 
2. 폰트
3. 그리드 시스템 적용해서 다시 해야? 
4. 혹시, 클래스 구성을 다르게 하는게 더 효율적일지도 체크 

![](https://i.imgur.com/6dUn7rh.png)

👉 우선, 지금은 반응형 분석이니까, 이 부분에 좀 더 집중하자
```


---


# [작업 중] 1단 컬럼 모바일 
## 결과물 

- 코드펜 : https://codepen.io/anotheryear-hm/pen/abMGyzZ

- 로컬출처 : C:\Users\user11\Desktop\kga\studynote\CSS\11_grid_반응형웹만들기.html

- 포인트 ⭐⭐⭐ 
``` bash 
1. 이미지를 figure 태그의 background 속성으로 처리 
2. figure 태그의 y축 값을 'padding-bottom : 56%' 으로 구현 (16:9 사진 비율 유지하기 위해) (구체적인 수치는 변경 가능) 👉 브라우저 너비 변화에 대응해서, 일정한 사진을 보여줄 수 있음. 
3. 설명 부분의 패딩 수치를 'em' 으로 줌 👉 폰트 사이즈에 대응해서, 일정한 padding 을 줄 수 있음. ⭐⭐⭐ 
```

![](https://i.imgur.com/4GW47Ze.gif)



- 예시 코드 
``` html
    <div class="page">

        <!-- header -->
        <header class="header">

            <h1 class="website-title">DJ코딩</h1>

            <form class="search-form">
                <input type="search">
                <input type="submit" value="찾기">
            </form>

        </header>

        <!-- menu -->
        <ul class="menu">
            <li class="menu-list">
                <a href="#" class="menu-link">Home</a>
            </li>
            <li class="menu-list">
                <a href="#" class="menu-link">About</a>
            </li>
            <li class="menu-list">
                <a href="#" class="menu-link">Product</a>
            </li>
            <li class="menu-list">
                <a href="#" class="menu-link">Contact</a>
            </li>

        </ul>

        <!-- 기본 콘텐츠 영역 | main | 여기에서는 primary -->
        <section class="main">

            <ul class="card-list">

                <li class="card-item">
                    <!-- background 속성이 있는 태그의 width, height 가 있어야 -> 그림이 나옴  -->
                    <figure class="card-image" style="background-image: url(./images/gradient_large.jpg)">

                    </figure>
                    <div class="card-desc">
                        Lorem ipsum dolor sit amet consectetur adipisicing elit. Suscipit, deleniti.
                    </div>
                </li>
            </ul>

        </section>

        <!-- sidebar-L | 여기에서는 secondary 를 사용 | 
            ⭐ 포인트 : secondary 클래스 이름을 공통으로 사용해서, 왼쪽, 오른쪽 사이드바를 공통으로 조절한다.⭐⭐
        -->
        <aside class="sidebar sidebar-L ">

        </aside>

        <!-- sidebar-R | 여기에서는 secondary 를 사용 | -->
        <aside class="sidebar sidebar-L ">

        </aside>

        <!-- footer -->
        <footer class="footer">
            Lorem ipsum dolor, sit amet consectetur adipisicing elit. Vel cum quam corrupti voluptatem iste ab dolores
            voluptate doloremque molestiae nisi.
        </footer>
    </div>
```

``` css
ol, ul, li {
	list-style: none;
}

html, body {
  	margin: 0;
	padding: 0;
	border: 0;
}



.card-item {
  margin-bottom: 2rem;
}

.card-image {
  /* height: 300px; */

  /* 가로 세로 비율이 유지되는 박스 만들기⭐ : 이걸로 인해, 가로 세로 비율이 유지?  */
  padding-bottom: 56.25%;

  /* background 속성 설정 */
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
  background-color: lightgray;
}

.card-desc {
  padding : 1em;
  background: whitesmoke;
}
![](https://i.imgur.com/3en7C5e.gif)

```




## 배운 점 모음 

### 1. 왼쪽 메뉴바, 오른쪽 메뉴바를 '동일한 클래스 이름' 을 줘서, 컨트롤 한다. ⭐⭐⭐⭐⭐ 
``` css 
<aside class="sidebar sidebar-L "> </aside>

<!-- sidebar-R | 여기에서는 secondary 를 사용 | -->
<aside class="sidebar sidebar-L "> </aside>
```

<br>

### 2. 이미지를 다룰 때, 'img 태그' 보다, 'background 속성' 으로 컨트롤 하는게, 더 편함 ⭐⭐⭐⭐⭐ 

- 주의할 점 : background 속성을 쓰는 태그의 width, height 가 있어야 함. 그렇지 않으면, 아무런 사진도 안 나옴. ⭐⭐⭐ 
	
``` html
 <li class="card-item">
	<figure class="card-image" style="background-image: url(./images/gradient_large.jpg)">
		<img src="./images/gradient_large.jpg" alt="">
	</figure>
	<div class="card-desc">
		Lorem ipsum dolor sit amet consectetur adipisicing elit. Suscipit, deleniti.
	</div>
</li>
```

<br>

### 3. 가로 세로 비율 유지 ex) 16:9 로 하고 싶은 경우 (feat. `padding-bottom`)⭐⭐⭐⭐⭐ 

``` bash 
- 문제 상황
	- '브라우저의 width'를 늘림에 따라서, 'image의 비율' 을 유지하면서, 줄어들어야 함 
	- 하지만, 이미지의 'width' 만 들어들고 있음. 

- 하고 싶은 것 ⭐⭐⭐⭐⭐ 
	1. 원본 사진의 비율이 1:1 인 상황에서, 브라우저에서는 16:9 로 보여주고 싶음
	2. 브라우저의 너비 변화에 대응하여, 사진 비율이 16:9 로 계속 유지 되었으면 함! 


- 해결방안 
	- image 에 padding-bottom : 60% 를 준다. 

- 이렇게 했을 때 해결되는 이유 
	- 화면의 비율을, '16:9' 로 하고 싶은 경우, 'width 160px & height 90px' 이면 -> 16:9 가 됨. 
	- padding-bottom 은, '테두리 기준, 아랫쪽 안쪽 여백' 을 채운다. 
	- '% 비율로 채운다' 라는 건, '부모의 너비를 기준' 으로 해당 비율만큼 채운다! 라는 말 ⭐⭐⭐⭐⭐ (와.. 몰랐음.)
	- '16:9' 비율을 x 너비 기준으로 보면 9/16 = 0.5625 임
	- 따라서, 'padding-bottom : 56.25%' 로 주면, 사진 비율을 16:9 로 유지할 수 있음. 

CF. '비율%' 계산 로직 
	- 'width : 50%' -> 부모 width 의 50% 만큼을 자식의 width 로 한다. 
	- 'height : 50%' -> 부모 height 의 50% 만큼을 자식의 height 로 한다.
	- 'padding-bottom : 30%' -> 부모 width 의 30% 만큼을 자식의 padding-bottom 값으로 한다. (이때, 부모 width 가 기준인 이유는 CSS 가 이렇게 잡아놓았음!⭐⭐)


CF. 만약, 부모의 width 가 설정되지 않은 경우엔, 어떤 값이 기준이 되는가? 
- css
	.card-image{
		padding-bottom : 56.25%
	}

- HTML
	<li class="card-item">
	<figure class="card-image" > </figure>

- 문제 상황
	- card-image 의 padding-bottom 값은 부모인 card-item 의 width 를 기준으로 한다. 
	- 그런데, card-item 의 width 값은 따로 설정되어 있지 않은 상황이다. 
	- 그러면, card-item 의 width 값은 어떻게 계산이 되는가! 

- css 계산 방식
	- 블록 레벨 요소의 기본셋팅은, '부모 요소의 너비' 를 상속 받는다. 
	- 만약, 부모도 없다면, 부모의 부모 chain 을 따라가면서, 상속 받는다. 
```


- padding-bottom 을 주는 경우와 주지 않는 경우 
![[padding-bottom으로 비율 유지 1.gif]]

- 예시 코드 
``` html 
<style>
	.card-item {
		margin-bottom: 2rem;
	}

	.card-image {
		/* height: 300px; */

		/* 가로 세로 비율이 유지되는 박스 만들기⭐⭐⭐⭐⭐ */
		padding-bottom: 56.25%;

		/* background 속성 설정으로 이미지 컨트롤 ⭐⭐ */
		background-repeat: no-repeat;
		background-position: center;
		background-size: cover;
		background-color: lightgray;
	}
</style>

<body>
	<div class="page">
			<ul class="card-list">
				<li class="card-item">
					<!-- background 속성이 있는 태그의 width, height 가 있어야 -> 그림이 나옴  -->
					<figure class="card-image" style="background-image: url(./images/gradient_large.jpg)">
	
					</figure>
					<div class="card-desc">
						Lorem ipsum dolor sit amet consectetur adipisicing elit. Suscipit, deleniti.
					</div>
				</li>
	
	</div>
</body>
```

<br>


### 4. 사진비율을 `width = 236px` 기준으로 다시 계산해서 보여주기 😥😥😥 

- 출처 : https://chat.openai.com/share/a0ec0f17-c547-4609-a459-c0745134a033

``` html 
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Dynamic Aspect Ratio Calculation</title>
    <style>
        .image-container {
            width: 100%; /* 요소의 너비 설정 */
            overflow: hidden;
            position: relative; /* 배경 이미지의 포지셔닝 기준 */
        }
        .image-container:before {
            content: '';
            display: block;
            width: 100%;
        }
        .image-background {
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background-size: cover;
            background-position: center;
        }
    </style>
</head>
<body>

<div class="image-container" id="imageContainer">
    <div class="image-background" id="imageBackground"></div>
</div>

<script>
    function setAspectRatio(imgSrc, containerId, backgroundId) {
        var img = new Image();
        img.onload = function() {
            var height = img.height;
            var width = img.width;
            var aspectRatio = (height / width) * 100;
            
            // Set the padding-bottom of the container to maintain aspect ratio
            var container = document.getElementById(containerId);
            container.style.paddingBottom = aspectRatio + '%';
            
            // Set the background image
            var background = document.getElementById(backgroundId);
            background.style.backgroundImage = `url(${imgSrc})`;
        };
        img.src = imgSrc;
    }

    // Example usage:
    setAspectRatio('path_to_your_image.jpg', 'imageContainer', 'imageBackground');
</script>

</body>
</html>

```


<br>

### card-list 에서 padding 을 잡아줄 때, 폰트의 단위를 `em` 으로 설정 -> 폰트 사이즈에 대응할 수 있도록 

``` css 
.card-desc {
	padding : 1em;
	background: whitesmoke;
}
```




### default css 로 넣어준 것 
``` css 
html {
	font-family: 'Apple SD Gothic Neo', Roboto, 'Noto Sans KR', NanumGothic, 'Malgun Gothic', sans-serif;
	color: #555;
	line-height: 1.2;
	word-wrap: break-word;
}
body {
	background: #eee;
	-webkit-font-smoothing: antialiased;
}
html, body, div, span, applet, object, iframe,
h1, h2, h3, h4, h5, h6, p, blockquote, pre,
a, abbr, acronym, address, big, cite, code,
del, dfn, em, img, ins, kbd, q, s, samp,
small, strike, strong, sub, sup, tt, var,
b, u, i, center,
dl, dt, dd, ol, ul, li,
fieldset, form, label, legend,
table, caption, tbody, tfoot, thead, tr, th, td,
article, aside, canvas, details, embed,
figure, figcaption, footer, header, hgroup,
menu, nav, output, ruby, section, summary,
time, mark, audio, video {
	margin: 0;
	padding: 0;
	border: 0;
}
article, aside, details, figcaption, figure, footer, header, hgroup, menu, nav, section {
	display: block;
}
div, span, article, section, header, footer, aside, p, ul, li, fieldset, legend, label, a, nav, form {
	box-sizing: border-box;
	/* content-box */
}
ol, ul, li {
	list-style: none;
}
table {
	border-collapse: collapse;
	border-spacing: 0;
}
img {
	max-width: 100%;
	height: auto;
	border: 0;
}
a {
	display: inline-block;
}
button {
	border: 0;
	background: transparent;
	cursor: pointer;
}

.flex-container {
	/* padding: 10px; */
	background: lightgray;
}
.flex-item {
	padding: 10px;
	border: 3px solid rgb(50,50,40);
	color: white;
	background: mediumseagreen;
}
```


<br>


---

<br>
# [작업중] 2단, 3단 컬럼 























# 추가로 해볼 것 
``` bash 
1. 개별적으로 UI 를 만들어놓고 -> 이것들을 합치는 형태이기 때문에, 평소에 UI  를 꾸준히 제작해놓으면 도움이 될 것 같아! 
```



