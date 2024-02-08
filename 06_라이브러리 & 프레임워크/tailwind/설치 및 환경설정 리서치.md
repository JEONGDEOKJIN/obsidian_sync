# 리소스 
- https://tailwindcss.com/docs/installation | 공식 홈페이지 꼭 
- 어드민 kmmoc 강의 | https://kmooc.udemy.com/course/tailwind-css-course/learn/lecture/29019738#overview
- 공식 문서 : https://tailwindcss.com/docs/guides/nextjs




# 0. 설치 및 환경 설정 

	
### 기본적으로 되는지 보기 
- 참고 자료
	- https://tailwindcss.com/docs/guides/nextjs
	- https://mingmeng030.tistory.com/275


``` bash
# Tailwind CSS 설치 (postcss , autoprefixer 도 함께 설치)
npm install -D tailwindcss postcss autoprefixer

# Tailwind configs 파일 만들기 위한 초기화 커맨드
npx tailwindcss init -p

# 생성된 Tailwind.configs.js 파일에서 Tailwind를 적용시킨 파일들의 path를 정해주기 
	# Add the paths to all of your template files in your `tailwind.config.js` file.
	# ✅ 우선 공식 문서 버전으로  하면 작동함 🔵
	# 📛📛 이 부분 설정하는게 살짝 헷갈렸음 
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: [
    "./app/**/*.{js,ts,jsx,tsx,mdx}",
    "./pages/**/*.{js,ts,jsx,tsx,mdx}",
    "./components/**/*.{js,ts,jsx,tsx,mdx}",
 
    // Or if using `src` directory:
    "./src/**/*.{js,ts,jsx,tsx,mdx}",
  ],
  theme: {
    extend: {},
  },
  plugins: [],
}

# global.css 에 아래 코드 추가 
@tailwind base;
@tailwind components;
@tailwind utilities;


# 실행해보기 
npm run dev


# 테스트 작성 
text-3xl font-bold underline

```

![](https://i.imgur.com/yApVZNX.png)



### extension 설치
- HTML CSS Support ⭐⭐⭐ 
	- 이거 설치하면, 자동완성 기능 됨


- tailwind intelligence 이걸 하니까, 자동완성 기능이 됨! 
	- 


- postCSS language support 다운
	- https://mingmeng030.tistory.com/275


- extension 모음 ⭐⭐⭐⭐⭐ 
	- https://medium.com/@annguyenhieuduc/3-tailwindcss-vscode-extension-makes-your-life-easier-9067b065c4f0
```
Tailwind CSS IntelliSense
Tailwind CSS Shades
Headwind
```


- [번역] Tailwind CSS에서 혼란을 방지하기 위한 5가지 모범 사례
	- https://velog.io/@lky5697/5-best-practices-for-preventing-chaos-in-tailwind-css


- tailwind 클래스 이름의 통일성을 유지하기 위한 'prettier-plugin-tailwindcss'
	- https://github.com/tailwindlabs/prettier-plugin-tailwindcss





# 1. 기본 리서치


- tailwind 공식 홈페이지 가면, 괜찮은 튜토리얼들이 있음. 
	- tailwind 공식 홈페이지 튜토리얼
		- https://www.youtube.com/watch?v=elgqxmdVms8&list=PL5f_mz_zU5eXWYDXHUDOLBE0scnuJofO0

- Tailwind CSS를 사용하여 Figma 구성 요소를 Next.js로 변환하는 방법
	- https://oneoneone.kr/content/bf00ca63


- 1차 결론 (11/09)
```
- tailwind 공식 문서 튜토리얼이 나쁘지 않은거 같으니, 우선 봐보자 
```








