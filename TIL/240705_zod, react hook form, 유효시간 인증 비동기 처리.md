

```
[문제상황]
const updateTimer = (targetTime: Date) => {
    const duration = differenceInSeconds(targetTime, new Date());
    /* [differenceInSeconds 기능] 
        - 두 개의 날짜(Date 객체) 사이의 차이를 초 단위로 계산
        - 이걸, 실시간으로 계산 
      */
    setTimer(duration);
    console.log("duration" , duration)
    console.log("duration type" , typeof(duration))
    console.log("isTimerExpired" , isTimerExpired)

    // 만료되면, isTimerExpired 상태값 변경 -> verifyCode 검증 필드 종료 및 재실행
    if (duration <= 55) {
      setVerifyCodeMessage("인증 코드 유효 시간이 만료되었습니다.")
      setIsTimerExpired(true);
      clearInterval(timeInterval.current!); //  setInterval 종료

    } else {
      setIsTimerExpired(false);
    }
  };


```


``` jsx
"use client";

import { zodResolver } from "@hookform/resolvers/zod";
import { getCookie, setCookie } from "cookies-next";
import React, { use, useEffect, useRef, useState } from "react";
import { z } from "zod";
import { ACCOUNT, ISREMEMBER } from "@/libs/constant/common";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";
import { FormProvider, useForm } from "react-hook-form";
import { usePostLogin } from "@/querys/AuthQuerys";
import {
  FormControl,
  FormField,
  FormItem,
  FormLabel,
  FormMessage,
} from "@/components/ui/form";
import { cn } from "@/libs/utils";
import Header from "@/components/Header/Header";
import { CountDown } from "@/components/Countdown/Countdown";
import { addMinutes, differenceInSeconds } from "date-fns";
import { clear } from "console";

export default function page() {
  const [isPwResetSuccess, setIsPwResetSuccess] = useState(false);
  const [isVerifyCodeRequested, setIsVerifyCodeRequested] = useState(false);
  const [isNameEmailVerified, setIsNameEmailVerified] = useState(false);
  const [isVerifyCompleted, setIsVerifyCompleted] = useState(false);
  const [isUserEnteringVerifyCode, setIsUserEnteringVerifyCode] =
    useState(false);
  const [isEmailVerified, setIsEmailVerified] = useState(false);
  const [isUserNameVerified, setIsUserNameVerified] = useState(false);
  const [isCodeVerified, setIsCodeVerified] = useState(false);

  const [defaultCountDown, setDefaultCountDown] = useState<number>(5);
  const [timer, setTimer] = useState<number>(defaultCountDown * 60);
  const timeInterval = useRef<NodeJS.Timeout | null>(null);
  const [isTimerExpired, setIsTimerExpired] = useState(false);

  const [verifyCodeMessage, setVerifyCodeMessage] = useState("본인인증 코드는 6자리 숫자여야 합니다.");

  // 검증 기준 만들기
  const formSchema = z.object({
    userName: z
      .string()
      .trim()
      .regex(/^[가-힣]+$/, {
        message: "이름은 한글만 사용할 수 있습니다.",
      })
      .max(35, {
        message: "이름은 최대 35자까지 가능합니다.",
      })
      .min(1, {
        message: "이름 형식이 유효하지 않습니다.",
      }),
    email: z
      .string()
      .trim()
      .regex(/^[^\s@]+@[^\s@]+\.[^\s@]+$/, {
        message: "이메일 형식이 유효하지 않습니다.",
      }),
      
      // ✅ 샵바이 연동하는 본인인증의 경우 6자리 숫자라고 가정
    verifyCode: z
      .string()
      .trim()
      .regex(/^\d{6}$/, {
        // message: "본인인증 코드는 6자리 숫자여야 합니다.",
        // message: { isTimerExpired ? "만료!" : "본인인증 코드는 6자리 숫자여야 합니다 " } 
        message: verifyCodeMessage,
      })
      // isTimerExpired이 false 인 경우 -> 1) 경고 메시지 띄우고 2) 검증을 다시 하기
      .refine((val) => !isTimerExpired, {
          message: "인증 코드 유효 시간이 만료되었습니다.",
        }),
  });

  const form = useForm({
    resolver: zodResolver(formSchema), // formSchema 형식을 전달하면 -> 해당 스키마에 맞게 입력했는지를 검증 -> react hook 에게 전달
    mode: "onBlur", // 유효성 검사가 실행되는 시점 | onBlur : input 에서 focus 가 벗어나는 순간.
    defaultValues: {
      // 기본값 설정
      userName: getCookie(ACCOUNT) ?? "", // login_id 의 기본값으로 쿠키에 저장된 ACCOUNT 값을 사용 -> 만약, 빈값이면 "" 사용
      email: "",
      verifyCode: "",
      timeExpired: false,
    },
  });

  // [필요] 전체 필드 유효성 확인
  const {
    formState: { isValid },
  } = form;
  /* 
      isValid 는 전체 필드 유요성을 확인
      isValid 는 아래와 같은 구조에서, isValid 값을 가져옴
        const form = {
        formState: {
          isValid: boolean
        }
    };*/

  const handleInputChange = async (field: any, value: any) => {
    await form.trigger(field, value);

    if (field === "email") {
      verifyEmail();
    }

    if (field === "userName") {
      verifyUserName();
    }

    if (field === "verifyCode" && value.length > 0) {
      console.log("verifyCode value", value);
      verifyCode();
    }
  };

  const verifyEmail = async () => {
    const emailResult = await form.trigger("email");
    setIsEmailVerified(emailResult);
  };

  const verifyUserName = async () => {
    const userNameResult = await form.trigger("userName");
    setIsUserNameVerified(userNameResult);
  };

  const verifyCode = async () => {
    const codeResult = await form.trigger("verifyCode");
    setIsCodeVerified(codeResult);
  };

  // 인증번호 요청 버튼 클릭
  const onClickRequestCode = async (item: any) => {
    // e.preventDefault() // form.handleSubmit(onClickRequestCode) 을 사용하면, 적지 않아도 됨.

    // 1. 백엔드에 데이터 전송
    alert("이름&핸드폰 번호 제출 -> 인증번호 요청함 완료");
    setIsVerifyCodeRequested(true); // 이게 굳이 필요한가 [❓]

    // 2. 타이머 받아오고 -> 타이머 함수에 넣고 -> return 받고 -> 상태값 업데이트
    /* 타이머함수(백엔드에서준시간) 의 기능
        1) 타이머 함수가 실행됨. 
        2) 타이머가 지나면, 검증필드가 종료.
        3) 타이머 안에 작성하면, 검증필드 통과
      */

    const timeCountFromBack = 1; // 백엔드에서 받아온 시간
    resetTimer(timeCountFromBack); // 타이머 재설정
    setDefaultCountDown(timeCountFromBack); // ex) 7분 카운트다운으로 설정

    // 3. 정상통신되면, '사용자 기재 시작'
    setIsUserEnteringVerifyCode(true);
  };

  // 타이머 재설정
  const resetTimer = (minutes: number) => {
    if (timeInterval.current) {
      clearInterval(timeInterval.current);
    }
    const targetTime = addMinutes(new Date(), minutes);
    updateTimer(targetTime);

    // 1초마다 실행 -> 숫자가 계속 변하는 이유⭐⭐
    timeInterval.current = setInterval(() => updateTimer(targetTime), 500);
  };

  // setInterval 에 의해 1초마다 실행됨
  const updateTimer = (targetTime: Date) => {
    const duration = differenceInSeconds(targetTime, new Date());
    /* [differenceInSeconds 기능] 
        - 두 개의 날짜(Date 객체) 사이의 차이를 초 단위로 계산
        - 이걸, 실시간으로 계산 
      */
    setTimer(duration);
    console.log("duration" , duration)
    console.log("duration type" , typeof(duration))
    console.log("isTimerExpired" , isTimerExpired)

    // 만료되면, isTimerExpired 상태값 변경 -> verifyCode 검증 필드 종료 및 재실행
    if (duration <= 55) {
      setVerifyCodeMessage("인증 코드 유효 시간이 만료되었습니다.")
      setIsTimerExpired(true);
      clearInterval(timeInterval.current!); //  setInterval 종료

    } else {
      setIsTimerExpired(false);
    }
  };
 

  useEffect( () => {
    console.log("isTimerExpired 🔥🔥 실시간 확인" , isTimerExpired)
  } , [isTimerExpired])

  // 인증번호를 백엔드로 제출
  const onClickCheckVerifyCode = async (item: any) => {
    alert("사용자가 적은 인증번호를 back으로 제출");

    // 1. 백엔드에 데이터 전송

    // 2. 정상 return 받음
    setIsVerifyCompleted(true);
  };

  // 본인인증 완료
  const completeVerification = () => {
    alert("본인인증 완료");
  };

  // Date 객체에서 '분' 과 '초' 를 추출
  const parseTimer = () => {
    const minutes = Math.floor(timer / 60);
    const seconds = timer % 60;
    return `${String(minutes).padStart(2, "0")}:${String(seconds).padStart(
      2,
      "0"
    )}`;
  };


  useEffect(() => {
    console.log("defaultCountDown👉", defaultCountDown);
  }, [defaultCountDown]);

  return (
    <>
      <Header content="비밀번호 재설정" />
      <section className="w-full p-[20px] h-full   ">
        <article className=" flex flex-col w-full pt-[34px]   h-[calc(100vh-176px)] relative">
          <article>
            <FormProvider {...form}>
              <form onSubmit={form.handleSubmit(completeVerification)}>
                <div className="gap-4 flex flex-col w-full ">
                  {/* 이름 */}
                  <FormField
                    control={form.control}
                    name="userName"
                    render={({ field }) => (
                      <FormItem>
                        <FormLabel>
                          <span className="text-[#DE3636] font-[600] text-[15px]">
                            *
                          </span>
                          이름
                        </FormLabel>
                        <FormControl>
                          <Input
                            className={cn(
                              "",
                              isValid ? "border-[#000] border-[1px]" : ""
                            )}
                            placeholder="이름을 입력해 주세요"
                            {...field}
                            onChange={async (e) => {
                              field.onChange(e);
                              await handleInputChange(
                                "userName",
                                e.target.value
                              );
                            }}
                          />
                        </FormControl>
                        <FormMessage />
                      </FormItem>
                    )}
                  />
                  {/* 이메일 */}
                  <FormField
                    control={form.control}
                    name="email"
                    render={({ field }) => (
                      <FormItem>
                        <FormLabel>
                          <span className="text-[#DE3636] font-[600] text-[15px]">
                            *
                          </span>
                          이메일
                        </FormLabel>
                        <FormControl>
                          <div className="flex relative jus w-full h-full  gap-[5px]">
                            <Input
                              className={cn(
                                "w-full",
                                isValid ? "border-[#000] border-[1px]" : ""
                              )}
                              placeholder="이메일을 입력해주세요."
                              // type="tel"
                              {...field}
                              onChange={async (e) => {
                                field.onChange(e);
                                await handleInputChange(
                                  "email",
                                  e.target.value
                                );
                              }}
                            />
                            <Button
                              className="w-[121px] h-[48px] shrink-0  text-[17px] bottom-[2px] bg-[#505050]"
                              // className={cn("text-[17px] bottom-[2px] absolute" , isValid ? "bg-[#24C307] text-white font-[600] text-[17px]" : "")}
                              // type="submit"
                              size="default"
                              disabled={!isEmailVerified || !isUserNameVerified}
                              variant={
                                isEmailVerified && isUserNameVerified
                                  ? "default"
                                  : "secondary"
                              }
                              onClick={onClickRequestCode}
                            >
                              {isUserEnteringVerifyCode
                                ? "인증번호 재요청"
                                : "인증번호 요청"}
                            </Button>
                          </div>
                        </FormControl>
                        <FormMessage />
                      </FormItem>
                    )}
                  />
                  {/* 인증번호 */}
                  {isUserEnteringVerifyCode && (
                    <FormField
                      control={form.control}
                      name="verifyCode"
                      render={({ field }) => (
                        <FormItem>
                          <FormLabel>
                            <span className="text-[#DE3636] font-[600] text-[15px]">
                              *
                            </span>
                            인증 번호
                          </FormLabel>
                          <FormControl>
                            <div className="flex relative jus w-full h-full  gap-[5px]  ">
                              <Input
                                className={cn(
                                  "w-full",
                                  isValid ? "border-[#000] border-[1px]" : ""
                                )}
                                placeholder="인증번호를 입력해주세요."
                                {...field}
                                onChange={async (e) => {
                                  field.onChange(e);
                                  await handleInputChange(
                                    "verifyCode",
                                    e.target.value
                                  );
                                }}
                              />
                              <span className="absolute right-[132px] flex top-[12px]">
                                <span>
                                  {timer > 0 ? parseTimer() : "00:00"}
                                </span>
                              </span>

                              <Button
                                className="w-[121px] h-[48px] shrink-0  text-[17px] bottom-[2px] bg-[#505050]"
                                // className={cn("text-[17px] bottom-[2px] absolute" , isValid ? "bg-[#24C307] text-white font-[600] text-[17px]" : "")}
                                type="submit"
                                size="default"
                                disabled={!isCodeVerified}
                                onClick={onClickCheckVerifyCode}
                                variant={
                                  isCodeVerified ? "default" : "secondary"
                                } // isValid 로 컨트롤 하면 바로 적용됨
                              >
                                인증번호 확인
                              </Button>
                            </div>
                          </FormControl>
                          <FormMessage />
                        </FormItem>
                      )}
                    />
                  )}
                </div>
                <Button
                  className="text-[17px] bottom-[2px] absolute"
                  // className={cn("text-[17px] bottom-[2px] absolute" , isValid ? "bg-[#24C307] text-white font-[600] text-[17px]" : "")}
                  type="submit"
                  size="default"
                  disabled={!isVerifyCompleted}
                  variant={isVerifyCompleted ? "default" : "secondary"}
                >
                  확인
                </Button>
              </form>
            </FormProvider>
          </article>
        </article>
      </section>
    </>
  );
}

```