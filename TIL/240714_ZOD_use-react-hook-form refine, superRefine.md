- 여기에서 refine, superRefine 이 뭐지 대체?
    
    `C:\\Users\\user11\\OneDrive\\바탕 화면\\nextInnovation\\marathon\\marathon-web\\src\\app\\signup\\page.tsx`
    
    ```tsx
    "use client";
    
    import { FormProvider, useForm, useWatch } from "react-hook-form";
    import { z } from "zod";
    import { zodResolver } from "@hookform/resolvers/zod";
    import { getCookie } from "cookies-next";
    import { ACCOUNT } from "@/libs/constant/common";
    import { usePostLogin } from "@/querys/AuthQuerys";
    import Header from "@/components/Header/Header";
    import { BackChevronIcon } from "@/components/Header/_components/icons";
    import InputFormItem from "@/components/Input/InputFormItem";
    import { Button, buttonVariants } from "@/components/ui/button";
    import {
      useGetSMSVerification,
      usePostSMSVerification,
      usePostUser,
    } from "@/querys/UserQuerys";
    import { useRouter } from "next/navigation";
    import InputFormItemWithTimer from "@/components/Input/InputFormItemWithTimer";
    import { JOIN } from "@/libs/constant/authentication";
    import { useErrorHandle } from "@/libs/hooks/useErrorHandle";
    import { useState } from "react";
    
    export default function Page() {
      const router = useRouter();
      const [isPhoneValid, setIsPhoneValid] = useState(false);
    
      const formSchema = z
        .object({
          login_email: z
            .string()
            .trim()
            .max(35)
            .min(5, { message: "이메일은 5자 이상이어야 합니다." })
            .email({ message: "이메일 형식이 유효하지 않습니다." }),
          login_pw: z
            .string()
            .trim()
            .min(4, {
              message: "비밀번호는 4글자 이상이어야 합니다.",
            })
            .max(512, {
              message: "비밀번호 형식이 유효하지 않습니다.",
            }),
          login_pw_confirm: z
            .string()
            .trim()
            .min(4, {
              message: "비밀번호는 4글자 이상이어야 합니다.",
            })
            .max(512, {
              message: "비밀번호 형식이 유효하지 않습니다.",
            }),
          name: z.string().min(2, { message: "이름을 입력해주세요." }),
          nickname: z.string(),
          phone_num: z
            .string()
            .min(10, { message: "휴대폰 번호는 10자 이상이여야합니다." })
            .max(15, { message: "휴대폰 번호는 15자 이하여야합니다." })
            .refine(value => /^[0-9]+$/.test(value), {
              message: "휴대폰 번호는 숫자만 가능합니다.",
            }),
          verification_code: z
            .string()
            .min(4, { message: "인증번호는 4자 이상이어야 합니다." }),
        })
        .superRefine(({ login_pw_confirm, login_pw }, ctx) => {
          if (login_pw_confirm !== login_pw) {
            ctx.addIssue({
              code: "custom",
              message: "비밀번호가 일치하지 않습니다.",
              path: ["login_pw_confirm"],
            });
          }
        })
        .superRefine(({ login_pw }, ctx) => {
          const hasLetter = /[a-zA-Z]/.test(login_pw);
          const hasNumber = /[0-9]/.test(login_pw);
          const hasSpecialChar = /[!@#$%^&*(),.?":{}|<>]/.test(login_pw);
    
          if (!hasLetter || !hasNumber || !hasSpecialChar) {
            ctx.addIssue({
              code: "custom",
              message:
                "비밀번호는 영어, 숫자, 특수문자를 각각 최소 한 글자 포함해야 합니다.",
              path: ["login_pw"],
            });
          }
        });
    
      const form = useForm({
        resolver: zodResolver(formSchema),
        mode: "onBlur",
        defaultValues: {
          login_id: "",
          login_email: "",
          login_pw: "",
          login_pw_confirm: "",
          phone_num: "",
          nickname: "",
          name: "",
          verification_code: "",
        },
      });
    
      // ===========================================================
      // ===========================================================
    
      const { mutate: postSMSVerification } = usePostSMSVerification();
    
      const memberName = useWatch({
        control: form.control,
        name: "name",
      });
    
      const mobileNo = useWatch({
        control: form.control,
        name: "phone_num",
      });
    
      const verification_code = useWatch({
        control: form.control,
        name: "verification_code",
      });
    
      const { errorHandler } = useErrorHandle();
    
      const handlerTimerFn = async (): Promise<{ code: number }> => {
        return new Promise(resolve => {
          postSMSVerification(
            {
              usage: JOIN,
              memberName: memberName,
              mobileNo: mobileNo,
            },
            {
              onSuccess: data => {
                resolve(data);
              },
              onError: error => {
                errorHandler(error);
                throw error;
              },
            },
          );
        });
      };
    
      const { checkEmailHandler: getSMSVerification } = useGetSMSVerification();
    
      const handlerVerifyButtonFn = async () => {
        try {
          if (memberName && mobileNo && verification_code) {
            const { data } = await getSMSVerification({
              usage: JOIN,
              memberName: memberName,
              mobileNo: mobileNo,
              key: verification_code,
            });
            if (data) {
              setIsPhoneValid(true);
            } else {
              form.setError("verification_code", {
                type: "custom",
                message: "인증번호가 일치하지 않습니다.",
              });
            }
          } else {
            form.setError("verification_code", {
              type: "manual",
              message: "이름, 전화번호, 인증번호를 모두 입력해주세요.",
            });
          }
        } catch (error) {
          // errorHandler(error);
          form.setError("verification_code", {
            type: "custom",
            message: "다시 시도해주세요.",
          });
        }
      };
    
      // ===========================================================
      // ===========================================================
    
      const { mutate: postSignUp } = usePostUser();
    
      const onSubmit = async (item: any) => {
        if (isPhoneValid) {
          const {
            login_id,
            login_email,
            login_pw,
            login_pw_confirm,
            phone_num,
            nickname,
            name,
          } = item;
          await postSignUp({
            login_id,
            login_email,
            login_pw,
            login_pw_confirm,
            phone_num,
            nickname,
            name,
          });
        }
      };
    
      // ===========================================================
      // ===========================================================
    
      return (
        <>
          <Header content="회원가입" leftIcon={<BackChevronIcon />} />
          <div className="w-full flex flex-col px-[20px]">
            <div className="w-full h-[calc(100vh-56px)] relative">
              <h1 className="pt-[20px] text-[17px] font-[600] leading-[20.29px]">
                이메일로 회원 가입
              </h1>
              <section className="h-[calc(100vh-200px)] overflow-y-auto pb-10">
                <FormProvider {...form}>
                  <form onSubmit={form.handleSubmit(onSubmit)}>
                    <div className="gap-[36px] flex flex-col mt-[34px]">
                      <InputFormItem
                        control={form.control}
                        name="id"
                        label="아이디"
                        type="text"
                        placeholder="아이디를 입력해 주세요"
                        isButton
                        buttonVariants={{ variant: "mouse" }}
                        buttonContent="중복 확인"
                        required
                      />
                      <InputFormItem
                        control={form.control}
                        name="login_pw"
                        label="비밀번호"
                        type="password"
                        placeholder="영문, 숫자, 특수문자를 조합하여 8자 이상"
                        required
                      />
                      <InputFormItem
                        control={form.control}
                        name="login_pw_confirm"
                        label="비밀번호 재입력"
                        type="password"
                        placeholder="비밀번호를 한 번 더 입력해 주세요."
                        required
                      />
                      <InputFormItem
                        control={form.control}
                        name="name"
                        label="이름"
                        type="text"
                        placeholder="이름을 입력해주세요."
                        required
                      />
                      <InputFormItem
                        control={form.control}
                        name="nickname"
                        label="닉네임"
                        type="text"
                        placeholder="닉네임을 입력해주세요."
                        isButton
                        buttonVariants={{ variant: "mouse" }}
                        buttonContent="중복 확인"
                        required
                      />
                      <InputFormItem
                        control={form.control}
                        name="login_email"
                        label="이메일"
                        type="email"
                        placeholder="이메일를 입력해 주세요"
                        isButton
                        buttonVariants={{ variant: "mouse" }}
                        buttonContent="중복 확인"
                        required
                      />
                      <div className="relative w-full">
                        <InputFormItemWithTimer
                          control={form.control}
                          name="phone_num"
                          label="휴대폰 번호"
                          type="tel"
                          placeholder="‘-’ 없이 입력해 주세요."
                          required
                          isCountDown
                          handleTimerFn={handlerTimerFn}
                          handlerVerifyButtonFn={handlerVerifyButtonFn}
                        />
                      </div>
                    </div>
                    <div className="flex w-full gap-[8px] absolute bottom-[22px] text-[17px] right-0 bg-white">
                      <Button
                        className="mt-[30px] text-[17px]"
                        variant="secondary"
                        type="button"
                        onClick={() => router.back()}
                        size="default"
                      >
                        이전
                      </Button>
                      <Button
                        className="mt-[30px] text-[17px]"
                        variant="default"
                        type="submit"
                        size="default"
                      >
                        다음
                      </Button>
                    </div>
                  </form>
                </FormProvider>
              </section>
            </div>
          </div>
        </>
      );
    }
    
    ```