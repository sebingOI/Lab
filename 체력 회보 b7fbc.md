# 체력 회복 !

상태: 시작 전
시간: 4.5
우선순위: 우선순위4
작성일시: 2022년 1월 17일 오후 12:06

### UDP

```jsx
프로토콜: heal (몬스터 체력회복 프로토콜)

message: mID(int), mcHP(int)

처리내용:
1. 요청이 온 클라이언트로부터 heal 프로토콜을 받은 경우
2. 몬스터 배열(mList)에서 mID를 조회한다.
3. 조회 후 몬스터 배열(mList)에서 mmHP를 조회한다.
4. mcHP를 mmHP로 업데이트해준다.
5. 업데이트된 정보를 클라이언트에게 heal 프로토콜로 전송한다.
```

### 검증

input:

```jsx
path: 127.0.0.1:9000
message: {cmd: heal, mID: 12, mcHP: 29 }
```

output: 

```jsx
message: {cmd: heal, mID: 12, mcHP: 100 }
```