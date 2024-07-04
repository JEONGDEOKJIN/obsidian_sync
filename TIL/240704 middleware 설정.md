
```
1. gamebattle fo 코드를 기반으로 -> 앤트스쿨에 적용
```


``` js 
import type { NextRequest } from "next/server";
// import { ACCESSTOKEN, REFRESHTOKEN } from "./libs/constant/common";

export function middleware(request: NextRequest) {
  const accessToken = request.cookies.get("accessToken")?.value;

  /* 콘솔 확인 결과 
        console.log('middleware cookies 👉', request.cookies)
        middleware cookies 👉 RequestCookies 
            {"next-auth.csrf-token":
                {"name":"next-auth.csrf-token",
                    "value":"2b04..............."},
                    "next-auth.callback-url":{"name":"next-auth.callback-url","value":"http://localhost:3000"},"GameBattle_fo_AccessToken":{"name":"GameBattle_fo_AccessToken","value":"eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzMTYiLCJyb2xlIjoiVVNFUiIsImlhdCI6MTcyMDA3NjYxMCwiZXhwIjoxNzIwMDgwMjEwfQ.FDpKMJEnZz_bzv7_xUY4kh_uPDsbL1aS8QFDQjY6sCtsubxEDsN6BDSKln7xwU3E5iXld28wULPbSrhho1Rz9A"},"GameBattle_fo_RefreshToken":{"name":"GameBattle_fo_RefreshToken","value":"eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiIzMTYiLCJyb2xlIjoiVVNFUiIsImlhdCI6MTcyMDA3NjYxMCwiZXhwIjoxNzUxNjEyNjEwfQ.KJFVak2REKPEcJ_8J92qY4Cq9_NXQWvUymVc3gACA1Y_OBXdLSVm1Xynq5CrlJ0smuBV6EkzaPP5ZrAmtVBjZg"},"GameBattle_fo_Nickname":{"name":"GameBattle_fo_Nickname","value":"나랑드"},
                    "accessToken":{"name":"accessToken","value":"eyJhbGciOiJIUzUxMiJ9."}  // ✅ 이게 존재하는 토큰 목록 -> so, 'accessToken' 이 토큰 이름에 해당하는 값을 가져오게 함
                }
        - 따라서,  const accessToken = request.cookies.get("accessToken")?.value 이렇게 가져오면, accessToken 값에 접근할 수 있음. 
    */

  // 로그인한 사용자만 접근
  const loginPaths = [`/totalList/totalChannel` , `/totalList/totalCommunity` , `/totalList/totalFanart` , `/totalList/totalWiki` , `/privacy`];

  // 로그인하지 않아도 접근
  const noLoginPaths = [`/login`, `/register`, `/forgetPassword` , `/terms` ];

  if (
    (accessToken && noLoginPaths.includes(request.nextUrl.pathname)) || // 로그인한 사용자가, 로그인하지 않아도 되는 페이지에 접근하려 할 때
    (!accessToken && loginPaths.includes(request.nextUrl.pathname))     // 로그인 하지 않은 사용자가, 로그인해야 하는 페이지(인가 페이지)에 접근하려 할 때
  ) {
    if (noLoginPaths.includes(request.nextUrl.pathname)) {      
      return Response.redirect(new URL("/", request.url));      // 허용 안 된 페이지로 접근시, 메인페이지로 리디렉션
    } else {
      return Response.redirect(new URL("/login", request.url)); // 허용 된 페이지로 접근시, 로그인페이지로 리디렉션
    }
  }
}

export const config = {
  matcher: ["/((?!api|_next/static|_next/image|.*\\.png$).*)"],
};

```