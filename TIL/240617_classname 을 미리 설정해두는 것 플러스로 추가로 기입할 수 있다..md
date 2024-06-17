

```
공통 컴포넌트인 Input, Textarea 를 보면 

1) 처음 들어가는 classname 이외에 
2) 추가로 넣을 수 있다. 

이걸 잘 활용하면 굉장히 좋을 것 같다. 
```


``` jsx
/* eslint-disable react-hooks/exhaustive-deps */
"use client";

import { useEffect, useRef, useState } from "react";
import Link from "next/link";

import { FormProvider, useForm } from "react-hook-form";

import useMutationGiftCoin from "@/querys/gift/useMutationGiftCoin";
import useQuerySearchNickname from "@/querys/gift/useQuerySearchNickname";
import useMutationSendMsg from "@/querys/gift/useMutationSendMsg";
import { useObserver } from "./useObserver";
import { useModal } from "@/libs/hooks/useModal";

import Button from "@/components/Form/Button/Button";
import Input from "@/components/Form/Input/Input";
import TextArea from "@/components/Form/TextArea/TextArea";
import { useFetchMyInfo } from "@/querys/MypageQuerys";

// TODO 사용자 정보에 있는 잔여 코인 정보를 받아와야 한다.
// TODO 닉네임 검색 -> 다른 키워드 넣고 검색 이때, 이전의 데이터가 보이는 문제

const MessageGiftModalContent = () => {
	const [nicknameSearchModal, setNicknameSearchModal] = useState(false);

	const methods = useForm({
		defaultValues: {
			nickname: "",
			messageTitle: "",
			messageContents: "",
			battleCoin: null,
			toId: 0,
		},
	});

	const modal = useModal();
	const searchResultsRef = useRef<HTMLUListElement | null>(null); // 검색 결과 ul 요소를 참조하기 위한 useRef

	// 내정보 조회
	const { data: myInfo } = useFetchMyInfo();
	// 코인 선물 API
	const { mutate: mutateSendCoin } = useMutationGiftCoin();
	// 메시지 전송 API
	const { mutate: mutateSendMsg } = useMutationSendMsg();

	// 닉네임 검색 API
	const { data, fetchNextPage, refetch, isFetching } = useQuerySearchNickname({
		nicknameKeyword: methods.watch("nickname"),
		rowsPerPage: 10,
		pageOffset: 1,
	});

	const bottom = useRef<HTMLDivElement | null>(null); // 하단 감지를 위한
	const onIntersect = ([entry]: IntersectionObserverEntry[]) =>
		entry.isIntersecting && fetchNextPage();

	useObserver({
		// 첫 마운트시에 data가 undefined가 나옴 그렇기 때문에 data 값이 변경됨에 따라
		// 제대로된 값을 넣어줘야 한다. 검색 -> 닉네임 선택 -> 다시 검색 시에 target이 할당 안됨
		// data fetching시에 target 다시 할당
		target: data !== undefined && !isFetching ? bottom : null,
		onIntersect,
	});

	// 확인 버튼
	const handleConfirmGiftCoin = (data: any) => {
		const { messageTitle, messageContents, battleCoin, toId } = data;

		// 닉네임 입력만 하고, 검색버튼을 누르지 않았을 때
		if (toId === 0 || toId === undefined) {
			alert("닉네임을 검색해주세요");
			return;
		}

		// 메시지 제목만 있는경우
		if (messageTitle !== "" && messageContents === "") {
			alert("메시지 내용도 입력해주세요");
			return;
		}
		// 메시지 내용만 있는경우
		if (messageContents !== "" && messageTitle === "") {
			alert("메시지 제목도 입력해주세요");
			return;
		}
		// 메시지, 코인 둘다 없는 경우
		if (
			messageTitle === "" &&
			messageContents === "" &&
			(battleCoin === null || battleCoin === "")
		) {
			alert("코인, 메시지 중 하나는 입력해야 합니다");
			return;
		}

		if (battleCoin === null || battleCoin === "") {
			mutateSendMsg({
				title: messageTitle,
				text: messageContents,
				recv_id: toId,
			});
		} else {
			if (parseInt(battleCoin) > myInfo.battle_coin) {
				alert("가지고 있는 코인 보다 더 많은 코인을 보낼 수 없습니다.");
				return;
			}

			mutateSendCoin({
				title: messageTitle,
				text: messageContents,
				recv_id: toId,
				coin: parseInt(battleCoin),
			});
		}

		modal.closeModal();
	};

	// 취소 버튼
	const handleCancel = () => {
		modal.closeModal();
	};

	// 닉네임 검색 Fn
	const handleSearchNickname = () => {
		if (methods.watch("nickname") !== "") {
			setNicknameSearchModal(true);
			refetch();
		}
	};

	const handleChoiceNickname = (nickname: string, memberId: number) => {
		methods.setValue("toId", memberId);
		methods.setValue("nickname", nickname);
		setNicknameSearchModal(false);
	};

	useEffect(() => {
		const handleClickOutside = (event: any) => {
			if (
				searchResultsRef.current &&
				!searchResultsRef.current.contains(event.target)
			) {
				setNicknameSearchModal(false);
				methods.reset({
					nickname: "",
				});
			}
		};

		document.addEventListener("mousedown", handleClickOutside);
		return () => {
			document.removeEventListener("mousedown", handleClickOutside);
		};
	}, []);

	return (
		<FormProvider {...methods}>
			<div>
				{/* 닉네임 검색창 */}
				<div className="flex items-end gap-x-[8px]">
					<div className="relative w-full">
						<Input
							type="text"
							name="nickname"
							label="닉네임"
							className="w-[100%]"
						/>
						{/* 닉네임 검색 InfiniteScroll */}
						{data !== undefined && nicknameSearchModal && (
							<ul
								ref={searchResultsRef}
								className="z-10 absolute top-[70px] mt-[5px] w-full h-[80px] bg-grayF1 p-[3px] rounded-[5px] overflow-y-scroll"
							>
								{/* 검색결과 없을 때 */}
								{data?.pages[0].id_nick.length === 0 && (
									<div className="flex justify-center items-center h-full">
										<span>검색결과 없음</span>
									</div>
								)}
								{/* 검색결과 있을 때 */}
								{data?.pages.map((_, idx) =>
									data?.pages[idx].id_nick.map((element: any) => (
										<button
											key={element.member_id}
											className="flex w-full border-b-[1px]"
											onClick={() =>
												handleChoiceNickname(
													element.nick_name,
													element.member_id
												)
											}
										>
											{element.nick_name} / {element.member_id}
										</button>
									))
								)}
								{/* 하단 감지를 위한 */}
								<div ref={bottom}></div>
							</ul>
						)}
					</div>
					<Button
						label="검색"
						onClick={handleSearchNickname}
						variant="defaultOutlineLight"
						size="lg"
					/>
				</div>
				<Input name="messageTitle" label="제목" type="text" />
				<TextArea
					name="messageContents"
					label="쪽지 내용"
					className="mb-[10px]"
				/>
				<div className="flex justify-between">
					<p className="text-[24px] mb-[40px]">
						선물 가능 배틀페이 : {myInfo?.battle_coin}
					</p>
					<Link href="/charge-point">
						<span className="text-[24px] text-brand1 font-bold">
							배틀페이 충전
						</span>
					</Link>
				</div>
				<Input
					type="number"
					name="battleCoin"
					label="배틀페이"
					className="mb-[10px]"
				/>
				<div className="flex gap-x-[15px]">
					<button onClick={handleCancel} className="w-[50%] bg-grayD9 py-[8px]">
						취소
					</button>
					<button
						onClick={methods.handleSubmit(handleConfirmGiftCoin)}
						className="w-[50%] bg-brand1 py-[8px] text-[#fff]"
					>
						확인
					</button>
				</div>
			</div>
		</FormProvider>
	);
};

export default MessageGiftModalContent;

```