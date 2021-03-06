---
title: "자바의 기초: 자바의 계산 처리와 조건"
excerpt: "자바의 신 5장에서 6장"
date: 2020-06-08 18:00:00
category: skills
---
## 5장: 계산을 하고 싶어요

### 연산자(Operator)
* String이라는 클래스만 + 연산이 가능
* / 연산을 할 때 타입이 double 혹은 float일 경우에만 소수형으로 출력됌

### 산술연산자(Arithmetic Operator)

* +: 더하기 연산자(additive operator)
* -: 빼기 연산자(subtraction operator)
* *: 곱하기 연산자(multiplication operator)
* /: 나누기 연산자(division operator)
* %: 나머지 연산자(remainder operator) 

### 대입연산자(Compound Assignment Operator)
* += : 기존 값에 우측 항의 값을 더함
* -= : 기존 값에 우측 항의 값을 뺌
* *= : 기존 값에  우측 항의 값을 곱함
*  /=  : 기존 값을 우측 항의 값으로 나눔
*  %= : 기존 값을 우측 항의 값으로 나눈 나머지
 
### 단항 연산자
* 피연산자가 하나인 것(한 개의 값을 처리하는 것)
    * ex. + or - 앞에 아무런 변수나 숫자가 없다면 단항 연산자로 분류
* +: 단항 플러스 연산자 (Unary plus operator)
* -:단항 마이너스 연산자(Unary minus operator)
* ++:증가 연산자(Increment operator)
* --:감소 연산자(Decrement operator)
* !:논리 부정 연산자(Logical complement operator)     
 
### +, -
* +: 양수
* -: 음수

### ++, --
* ++: 1만큼 증가
* --: 1만큼 감소
* ++, --는 변수의 앞 혹은 뒤에 붙을 수 있음
* =이 없이 0이나 5와 같은 숫자가 아닌 변수에만 사용 가능
* ++를 뒤에 붙이면 변수를 참조한 후에 1을 더 함

### !
* boolean 타입에서만 사용 가능
* ex. boolean flag = true
* ex. !flag (=false)

### 연산 우선순위
* ( ) 소괄호 사용

### 연산자의 우선순위
* 우선순위 1. 단항 연산자: ++, --, +, -, !, ~
* 우선순위 2. 산술 연산자: *, /, %
* 우선순위 3. 산술연산자: +, -

### ~(틸드)
* 2진수로 되어 있는 비트 값을 거꾸로 바꾸는데 사용
* 비트 값의 0을 1로, 1을 0으로 바꿈


### 비교연산자
* 왼쪽 값과 오른쪽 값을 비교하는데 사용
* `모든 비교 연산자의 결과는 반드시 boolean이다`
* ==: 같음(equal to)
* !=: 같지 않음(not equal to)
* `>: (왼쪽 값이) 큼(greater than)`
* `>=: (왼쪽 값이) 같거나 큼(greater than or equal to)`
* <:(왼쪽 값이) 작음(less than)
* <=:(왼쪽 값이) 같거나 작음(less than or equal to)

### 등가 비교 연산자(Equality Operator)
* 기본자료형과 참조자료형에서 사용 가능
* `기본 자료형은 같은 종류끼리 비교 가능`
* 참조자료형은 그 주소 값이 같은지 확인한다

* ==:두 개의 값이 같으면 true
* !=:두 개의 값이 다르면 true

### 대소 비교 연산자(Relational Operator)
* ` boolean이나 참조 자료형에서는 사용 불가`
* 식(**두 기호의 순서 주의**): true 조건
* a<b: a가 b보다 작을 때
* a>b: a가 b보다 클 때
* a<=b: a가 b와 같거나, b보다 작을 때
* a>=b: a가 b와 같거나, b보다 클 때

### 논리 연산자(Conditional Operator)
* 조건 연산자로서 `공백이 있으면 안됌`
* &&: AND 결합(Conditoinal AND)
* `||: OR 결합(Conditional OR)`

### 삼항 연산자(Conditional Operator?:)
* `변수 = (boolean 조건식) ? true일때 값 : false일때 값;`
* 장점: 어떤 변수에 값을 할당할 때 조건이 있는 문장을 한 줄로 처리 가능
* 단정: 삼항 연산자보다 if 문장을 사용하는 것이 가독성이 더 좋다

### 형 변환(Casting)
* 서로 다른 타입 사이에 변환하는 작업을 하는 것
* 괄호로 묶어 줌
* boolean 은 형변환이 불가
* 기본자료형→참조자료형 혹은 그 반대의 경우도 불가
    * 숫자 값을 참조 자료형으로 변경은 가능
* `범위가 큰 타입에서 작은 타입으로 변환할 때는 소괄호 안에 볌위가 작은 타입을 명시해주어야 한다`
    * 변환할 때 앞의 1바이트는 버린다

### 타입별 사용 가능한 연산자
* 책 참고 p.123

### 참고
* instanceof: 자바의 예약어 및 연산자
* 비트 연산을 하는 7개의 연산자
* 연산의 순서를 위해 소괄호 사용은 추천
    * 허나, 소괄호 4개 이상 사용하지 않는게 좋음

## 6장: 제가 조건을 좀 따져요
### if
~~~~ java
if(boolean값) 처리문장;
~~~~
~~~~ java
if(boolean값){
 처리문장1;
 처리문장2;
 ...}
~~~~

### if~else
~~~~ java
if(boolean값) 처리문장1;
 else 처리문장2;
~~~~
~~~~ java
if(boolean값) {
처리문장1;
처리문장2;
...;
} else {
처리문장1;
처리문장2;
....;
}
~~~~

### if~else if~else
~~~~ java
if(boolean값1) A;
else if(boolean값2) B;
else C;
~~~~

* 같은 의미: 
`결과값 = boolean값1 ? "A" : boolean값2 ? "B" : "C";`

### &&와 ||
* &&은 첫 조건이 false면 두 번째 조건은 무시
* `||`은 첫 조건이 true면 두 번째 조건은 무시
* &&와 `||`을 조건식에서 함께 사용할 경우 먼저 계산할 조건에 ()을 사용

### switch
* 하나의 값이 여러 범위 걸쳐 비교되어야 할 때 사용
~~~~ java
switch(비교대상변수){
case 점검값1;
처리문장1;
...
break;
case 점검값2;
처리문장2;
...
break;
...
default:
기본처리문장;
...
break;
}
~~~~
* default: 앞에 있는 조건에 맞지 않는 경우에 수행
    `무조건 실행이 아니다`
* 비교대상변수는 `long을 제외한 정수형과 몇몇 특별한 타입만 가능`

### 반복문
* 지정한 횟수만큼 반복하거나 조건에 맞을 떄까지 반복하는 문장
    * for 루프
    * while문

### while
~~~~ java
while(boolean조건){
처리문장;
...
}
~~~~
~~~~ java
while(boolean조건){
처리문장;
...
if(조건) break;
}
~~~~
~~~~ java
while(boolean조건){
처리문장1;
...
if(조건) continue;
처리문장2;
}
~~~~
* break; 현재 수행중인 중괄호에서 빠져나간다
* continue; 그 뒤에 있는 문장(처리문장2)은 건너뛰고 "boolean" 조건 점검 부분으로 다시 가라 

### 무한루프(Infinite loop)
* 해당 반복문이 빠져나갈 수 없는 경우 자바 프로세스가 멈출 때까지 계속 반복
* 서비스가 장애로 연결될 가능성이 있음

### do ~ while vs while
* do ~ while문은 적어도 한 번은 반복문장이 실행됌
* while문은 조건에 한 번도 맞지 않으면 한 번도 실행되지 않음

### for
```
for (초기화; 종료조건; 조건 값 증가){
반복문장
}
```

### label
* 예약어
* 두 개 이상의 for나 while 루프가 있을 때 사용

### 참고
* 어떤 문장이든 세미콜론(;)만 있으면 컴파일/실행이 정상적으로 가능
* 코드는 가독성이 좋아야 한다
    * 중괄호{ }를 잘 사용하자!
* switch구문은 숫자 비교시에 적은 숫자부터 증가시켜 가자

---
## 책 정보
* 책제목: 자바의 신 1
* 지은이: 이상민
* 출판사: 로드북
