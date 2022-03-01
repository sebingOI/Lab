# 회원가입 !

상태: 진행 중
소요시간: 1
우선순위: 우선순위1
작성일시: 2022년 1월 16일 오후 9:36
제품 관리자: 익명

# HTTP서버

```jsx
<회원가입>
path: /join
req: id, nick, password
처리내용: 1. 요청이 온 클라이언트로부터 id, nick, password를 받는다.
					2. DB를 조회한다.
					3. DB에서 같은 아이디와 닉네임이 있는지 비교한다.
					4. 없을 경우 DB에 값을 저장한다. 그 후 클라이언트에 회원가입 성공 패킷 전송
					5. 있을 경우 클라이언트에게 회원가입 실패 패킷 전송.
res: 회원가입 성공 유무(int)
<성공시>
	1. 숫자 1을 보낼 시 : 회원가입 성공       
<실패시>
	2. 숫자 2를 보낼 시 : DB에 있는 이메일과 겹칠 경우 실패
	3. 숫자 3를 보낼 시 : DB에 있는 닉네임과 겹칠 경우 실패
```

## 검증

input

```jsx
path: localhost:8000/join
body: {
  id: asdf,
  nick: hing,
  password: 1234
}
type:post
```

output

```jsx
DB에 있는 id와 password가 안 겹치고 새로운 것일경우
-> 1반환.(Response)
-> DB 결과 -> Select * from users로 조회를 했을 경우 다음 데이터가 추가되어있음.
{
  id: asdf,
  nick: hing,
  password: 1234,
  class: Default,
	pAtt: Default,
	Rz: Default,
	Lx: Default,
	Ly: Default,
	Lz: Default,
	lv: Default,
	pmHP: Default,
	pcHP: Default,
	pExp: Default,
} 
DB에 있는 id가 생성하려고 하는 id와 겹칠 경우
-> 2반환.(Response)
-> DB 결과 -> Select * from users로 조회를 했을 경우 이전과 같은 결과를 내야 함.
DB에 있는 password가 생성하려고 하는 password와 겹칠 경우 3
-> 3반환.(Response)
-> DB 결과 -> Select * from users로 조회를 했을 경우 이전과 같은 결과를 내야 함.
```