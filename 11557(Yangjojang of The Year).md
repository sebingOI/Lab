# 11557(Yangjojang of The Year)

> 문제
> 

입학 OT때 누구보다도 남다르게 놀았던 당신은 자연스럽게 1학년 과대를 역임하게 되었다.

타교와의 조인트 엠티를 기획하려는 당신은 근처에 있는 학교 중 어느 학교가 술을 가장 많이 먹는지 궁금해졌다.

학교별로 한 해동안 술 소비량이 주어질 때, 가장 술 소비가 많은 학교 이름을 출력하여라.

> 입력
> 

입력의 첫 줄에는 테스트 케이스의 숫자 T가 주어진다.

매 입력의 첫 줄에는 학교의 숫자 정수 N(1 ≤ N ≤ 100)이 주어진다.

이어서 N줄에 걸쳐 학교 이름 S(1 ≤ |S| ≤ 20, S는 공백없는 대소문자 알파벳 문자열)와 해당 학교가 지난 한 해동안 소비한 술의 양 L(0 ≤ L ≤ 10,000,000)이 공백으로 구분되어 정수로 주어진다.

같은 테스트 케이스 안에서 소비한 술의 양이 같은 학교는 없다고 가정한다.

> 출력
> 

각 테스트 케이스마다 한 줄에 걸쳐 술 소비가 가장 많은 학교의 이름을 출력한다.

> 예제 입력
> 

```jsx
2
3
Yonsei 10
Korea 10000000
Ewha 20
2
Yonsei 1
Korea 10000000
```

> 예제 출력
> 

```jsx
Korea
Korea
```

> 전체 코드
> 

```jsx
let fs = require('fs');
let input = fs.readFileSync('/dev/stdin').toString().split('\n');

let result = '';
let index = 1; 
let max = 0; 

for (let i = 0; i < parseInt(input[0]); i++){
        for (let j = 0; j<parseInt(input[index]); j++)
            {
                let sc = input[j+index+1].split(' ')
                let a = sc[0] 
                let b = parseInt(sc[1])
                if(b > max) 
                    {
                        max = b;
                        result = a;
                    }
            }
        max = 0;
        index += parseInt(input[index])+1
        console.log(result)
    }
```

> 코드 설명
> 
1. require()을 사용하여 fs모듈을 불러와서 fs 변수에 저장한다.
2. fs.readFileSync()를 사용하여 파일을 동기적으로 읽어와서 toString()을 사용하여 문자열로 만든 후, split('\n')을 사용하여 계행을 기준으로 나눠서 배열에 넣고 배열을 input에 저장한다.
3. 출력에 사용할 result 를 빈 문자열로 저장
4. 1을 index 변수에 저장
5. max에 0을 저장하여 초기화  
6. input0인덱스를 parseInt()로 정수화하여 그만큼 for문 카운트 합니다
7. input[index]로 하여 1로 하여 학교 명수 갯수를 받고 그 수만큼 for문 카운트를 합니다.
8. sc이라는 변수를 선언하고 그 안에 j+index+1을 하여 학생들의 이름과 숫자를 split(’ ‘)사용하여 띄어쓰기 기준으로 나눠 저장합니다. 
9. 변수 a에 sc[0]를 정수형으로 형변환 하여 저장합니다 (학생의 술 소비)
10. 변수 b에 sc[1]을 저장합니다.(학생) 
11. 변수 b가 max보다 크다면 if문을 실행합니다
12. 변수 b가 max보다 크다면 max안에 a를 넣어 저장하고 출력값에 사용할 result값에 b를 저장합니다. 
13. max를 다시 초기화 해줘야 중복이 없기 때문에 초기화를 해줍니다.
14. index에 input[index]+1을 하여 다음 구단주를 볼수 있도록 저장합니다.
15. result를 console.log사용하여 출력합니다.