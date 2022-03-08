# 생성 !

상태: 시작 전
시간: 4.3
우선순위: 우선수위1 🔥
작성일시: 2022년 1월 17일 오후 2:35

### UDP

```jsx
message: mID(string), mcHP(int), mExp(int), mAtt(int), 
				 cLx(float), cLy(float), cLz(float), cRz(float), dLx(float), dLy(float), 
				 dLz(float), dRz(float), mAct(int)

처리내용:
1. 서버가 처음 켜진 후 mID(몬스터 아이디), mcHp(몬스터 현재 체력), 
   mAtt(몬스터 공격력), cLx,cLy,cLz(현재 위치 값), dLx,dLy,dLz(기본 위치 값), 
   mExp(몬스터 경험치),cRz(회전값)를 넣어 mList(몬스터 배열) 생성 (기본선언)
2. 접속한 클라이언트에게 dLx, dLy, dLz, dRz, mExp, mAtt를 제외한 mList(몬스터 배열)를 [접속](https://www.notion.so/6311901606094d23b3bfccad1c9dfa73)에서 전송 [(접속)](https://www.notion.so/6311901606094d23b3bfccad1c9dfa73)
```

### 검증

몬스터 배열

```jsx
{ mID: 1, mcHP: 100, cLx: -2400, cLy: -9510, cLz: -111.6, cRz: 90, dLx: -2400, dLy: -9510, dLz: -111.6, dRz: 90, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 2, mcHP: 100, cLx: -3580, cLy: -9660, cLz: -168, cRz: 50, dLx: -3580, dLy: -9660, dLz: -168, dRz: 50, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 3, mcHP: 100, cLx: -3160, cLy: -8680, cLz: -168, cRz: 140, dLx: -3160, dLy: -8680, dLz: -168, dRz: 140, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 4, mcHP: 100, cLx: -1960, cLy: -8390, cLz: -168, cRz: 100, dLx: -1960, dLy: -8390, dLz: -168, dRz: 100, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 5, mcHP: 100, cLx: -890, cLy: -7140, cLz: 72, cRz: 110, dLx: -890, dLy: -7140, dLz: 72, dRz: 110, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 6, mcHP: 100, cLx: 2340, cLy: -5660, cLz: -8, cRz: 40, dLx: 2340, dLy: -5660, dLz: -8, dRz: 40, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 7, mcHP: 100, cLx: 310, cLy: -5610, cLz: 42, cRz: 0, dLx: 310, dLy: -5610, dLz: 42, dRz: 0, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 8, mcHP: 100, cLx: 240, cLy: -3480, cLz: 202, cRz: 190, dLx: 240, dLy: -3480, dLz: 202, dRz: 190, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 9, mcHP: 100, cLx: 2630, cLy: -4340, cLz: -28, cRz: 100, dLx: 2630, dLy: -4340, dLz: -28, dRz: 100, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 10, mcHP: 100, cLx: 1640, cLy: -1690, cLz: -98, cRz: 230, dLx: 1640, dLy: -1690, dLz: -98, dRz: 230, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 11, mcHP: 100, cLx: 1870, cLy: -250, cLz: 152, cRz: 150, dLx: 1870, dLy: -250, dLz: 152, dRz: 150, mAct: 101, mExp: 3, mAtt: 10, mRT: 10000 }
{ mID: 21, mcHP: 500, cLx: -7210, cLy: -7360, cLz: -98, cRz: 100, dLx: -7210, dLy: -7360, dLz: -98, dRz: 100, mAct: 101, mExp: 30, mAtt: 25, mRT: 30000 }
{ mID: 22, mcHP: 500, cLx: -8070, cLy: 680, cLz:  62, cRz: 30, dLx: -8070, dLy: 680, dLz:  62, dRz: 30, mAct: 101, mExp: 30, mAtt: 25, mRT: 30000 } 
```

### 일반 몬스터

```jsx
몬스터 아이디(mID): 1~20
몬스터 현재 채력(mcHP): 100
경험치(mEXP): 3
공격력(mAtt): 10
리스폰 타임(mRT): 10초
기본 x좌표(dLx):몬스터 마다 기본 x좌표가 다름, 몬스터 배열 확인 요함.
기본 y좌표(dLy):몬스터 마다 기본 y좌표가 다름, 몬스터 배열 확인 요함.
기본 z좌표(dLz):몬스터 마다 기본 z좌표가 다름, 몬스터 배열 확인 요함.
회전값(Rz): 1 ~ 360
```

### 보스 몬스터

```jsx
몬스터 아이디(mID): 21~22
몬스터 현재 채력(mcHP): 500
경험치(mEXP): 30
공격력(mAtt): 25
리스폰 타임(mRT): 180초
기본 x좌표(dLx):몬스터 마다 기본 x좌표가 다름, 몬스터 배열 확인 요함.
기본 y좌표(dLy):몬스터 마다 기본 y좌표가 다름, 몬스터 배열 확인 요함.
기본 z좌표(dLz):몬스터 마다 기본 z좌표가 다름, 몬스터 배열 확인 요함.
회전값(Rz): 1~360
```