---
title: "자바의 기초: 배열"
excerpt: "자바의 신 7장"
date: 2020-06-08 18:00:00
category: skills
---
## 7장: 여러 데이터를 하나에 넣을 수는 없을까요?
### 자료구조
- 데이터를 저장하기 위한 구조
    - ex. List, Queue, Map, LinkedList, etc.

### 배열
- 한 변수에 여러 개의 값을 넣을 수 있는 것
- 일종의 자료 구조 중 하나
- `배열은 참조자료형`

### 배열 만들기1
1. 배열 변수 정의
    -  `배열 변수를 정의할 때 대괄호 안에는 아무것도 써주면 안된다.`
    - ex.  int [] lottoNumbers;  //선호
    - ex. int lottoNumbers[];
2. 배열의 선언
    - new를 써 준 후 타입 이름을 명시해주고, 대괄호 안에 해당 배열의 크기를 지정해 준다.
    - ex. lottoNumbers = new int[7];
3. 배열에 값 지정
    - ex. lottoNumbers[1]=5;

### 배열 만들기2
- 배열을 선언과 함께 초기화하기
    - 중괄호 안에 각 위치에 해당하는 값을 콤마로 구분하여 나열
    - 한 번에 변수 선언 및 초기화 하기
        - 두 줄 사용 X
    - 배열 사이 데이터 추가 콤마 사용은 ok
        - ex. int[] lottonumbers={5,1,2,3,
        4,
        6.10};

### 배열의 특징
- 배열의 위치는 0부터 시작
- 모든 기본자료형 & 참조자료형 배열 만들기 가능
- 참조자료형은 toString() 메소드가 없으면 '타입이름@고유번호'로 출력됌`
 
### ArrayIndexOutOfBoundsException
 - 배열의 위치를 벗어난 예외가 발생했다.
 - 컴파일 때는 ok, 실행에서 오류ㅣ
 - 예외 발생:
    1. 배열에 값을 잘못할당할 때
        - ex. Java.lang.ArrayIndexOutOfBoundsException:잘못 지정한 위치(Index)
    2. 값을 참조할 때

### 배열의 기본값
- 기본 자료형 배열의 기본값은 각 자료형의 기본값과 동일
- 지역번수라 하더라도, 배열의 크기만 정해주면 문제 발생 X
- `boolean의 기본값은 false`
- char은 공백
- `참조자료형은 초기화(new)를 하지 않으면 null 출력
    - ex. String [] = null;`

### 2차원 배열
- 두개의 대괄호를 타입과 변수명 사이에 선언하자
`twoDim[0]=int 배열` 
`twoDim[0][0]=int값`
    - ex. int [] twoDim[];
    - ex. int twoDim[][];
    - ex. int[][] twoDim; //선호
- 1차원 크기는 무조건 지정해야 함

### 배열의 길이 확인
- 배열 이름에 .length 붙이기
- 2차원 배열의 크기를 알고 싶으면 1차원배열에 .length 붙이기
    - ex. twoDim[0].length; 

### for루프와 배열
~~~~ java
for(타입이름 임시변수명:반복대상객체){
}
~~~~

### StringJoiner
여러문자를 구분자를 이용하여 붙임
- `StringJoiner sj = new StringJoiner("-");` //-를 붙이는 문자열 생성
    - sj .add(변수1);
- `public StringJoiner(CharSequence delimiter, CharSequence prefix, CharSequence suffix)` //접두사, 접미사 붙여주기
    - ex. StringJoiner sj = new StringJoiner("-","<",">"); 
    - ex. sj .add(변수1);
    - ex. sj .add(변수2);
    - 출력: <변수1, 변수2>

---
## 책 정보
* 책제목: 자바의 신 1
* 지은이: 이상민
* 출판사: 로드북
