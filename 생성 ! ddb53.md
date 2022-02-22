# 생성 !

상태: 시작 전
시간: 1
우선순위: 우선순위1
작성일시: 2022년 1월 16일 오후 9:55

## UDP서버

```jsx
message: nick(string), class(int), pmHP(int), pcHP(int), pAtt(int), cc(int)

처리내용:  
1. 유저DB에서 패킷으로 받은 id를 조회한다. [(접속 참고)](https://www.notion.so/6311901606094d23b3bfccad1c9dfa73)
2. 조회한 id와 일치하는 유저 정보의 class를 조회
3. class가 0일 경우
	3-1. 요청이 온 클라이언트에게 캐릭터 생성 패킷(cc: 1, id, class: 0)을 전송한다.
	3-2. 요청이 온 클라이언트로부터 캐릭터 생성 성공 패킷(cc: 1, id, class: 1~3, pmHP, pAtt)을 받는다.
	3-3. 유저DB에서 패킷으로 받은 id를 조회한다.
	3-4. 조회 후 유저 DB에 class, pmHP, pAtt를 업데이트한다.
	3-5. pcHP에 pmHP를 넣어준 뒤 유저DB에 업데이트한다.
4. 접속으로 돌아간다. [(접속)](https://www.notion.so/6311901606094d23b3bfccad1c9dfa73)
```

- 참고
    
    
    | 직업/스탯 | Lv. 1 Att | Lv. 1 Hp | Lv.1 Exp | Increase Att | Increase Hp | Increase Exp | Lv. 10 Att | Lv. 10 Hp | Lv.10 Exp |
    | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
    | 워리어 | 8 | 80 | 10 | 4 | 80 | 5 | 44 | 800 | 55 |
    | 아처 | 10 | 60 | 10 | 5 | 60 | 5 | 55 | 600 | 55 |
    | 팔라딘 | 6 | 100 | 10 | 3 | 100 | 5 | 33 | 1000 | 55 |

## 검증

input

```jsx
path: 127.0.0.1:9000
message: { id: mola, class: 1 }
```

class가 1일 경우

```jsx
캐릭터 생성 전: { class: 0, nick: warriar, pmHP: 0, pcHP: 0, Ly: 0,Lx: 0,Lz: 0, lv: 0, pExp: 0,Rz: 0, act: 0, pAtt: 0 }
캐릭터 생성 후: { class: 1, nick: warriar, pmHP: 100, pcHP: 100, Ly: 441.21,Lx: 453.2335,Lz: 929.193, lv: 1, pExp:9,Rz: 50, act: 01, pAtt: 8 }
```

class가 2일 경우

```jsx
캐릭터 생성 전: { class: 0, nick: NULL, pmHP: 0, pcHP: 0, Ly: 0,Lx: 0,Lz: 0, lv: 0, pExp: 0,Rz: 0, act: 0 }
캐릭터 생성 후: { class: 2, nick: warriar, pmHP: 60, pcHP: 60, Ly: 441.21,Lx: 453.2335,Lz: 929.193, lv: 1, pExp:9,Rz: 50, act: 01, pAtt: 10 }
```

class가 3일 경우

```jsx
캐릭터 생성 전: { class: 0, nick: warriar, pmHP: 0, pcHP: 0, Ly: 0,Lx: 0,Lz: 0, lv: 0, pExp: 0,Rz: 0, act: 0 }
캐릭터 생성 후: { class: 3, nick: warriar, pmHP: 100, pcHP: 100, Ly: 441.21,Lx: 453.2335,Lz: 929.193, lv: 1, pExp:9,Rz: 50, act: 01, pAtt: 6 }
```