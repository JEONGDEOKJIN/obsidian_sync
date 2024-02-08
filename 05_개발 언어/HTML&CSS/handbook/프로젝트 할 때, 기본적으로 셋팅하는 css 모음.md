# 바닐라 JS 프로젝트 
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
```

- 출처 : FLEX 스터디 `C:\Users\user11\Desktop\kga\studynote\CSS\flex\default.css`


<br>

# React 프로젝트 
``` CSS
/* tailwind 를 css 에 넣어주는 설정 */
@tailwind base;
@tailwind components;
@tailwind utilities;


/* 기본 폰트 pretendard 설정 */
@font-face {
  font-family: 'Pretendard-Regular';
  src: url('https://cdn.jsdelivr.net/gh/Project-Noonnu/noonfonts_2107@1.1/Pretendard-Regular.woff') format('woff');
  font-weight: 400;
  font-style: normal;
}

body {
  font-family: 'Pretendard-Regular';
}


/* 스크롤바 설정 */
/* width */
::-webkit-scrollbar {
  border-radius: 8px; /* 둥근 모서리의 크기 조정 */
  width: 10px;
}

/* 스크롤바 트랙(경로)에 대한 스타일 */
::-webkit-scrollbar-track {
  border-radius: 8px; /* 둥근 모서리의 크기 조정 */
  background: #fcfcfc;
}

/* 스크롤바 핸들(스크롤 막대)에 대한 스타일 */
::-webkit-scrollbar-thumb {
  background: #d9d9d9;
  border-radius: 8px;
}

/* 스크롤바 호버 */
::-webkit-scrollbar-thumb:hover {
  background: #f0eded;
}

```

- 출처 : 포트폴리오 개정 프로젝트 (`C:\Users\user11\Desktop\dj_dev\portfolio_revise\frontend\src\index.css`)

