---
title: "자바의 기초: 프로그래밍이란 무엇인가"
excerpt: "자바의 신 1장에서 4장"
date: 2020-06-08 18:00:00
category: skills
---
## 1장: 프로그래밍이란 무엇인가?

### 객체지향 프로그래밍 언어(Object Oriented Programming Langugage)
    * ex. 자바

### 클래스(class)
* 선언법: public class 클래스 이름
    * public class DoorLockManager(){}
* 자바의 가장 작은 단위

``` 클래스 = 상태(변수) + 행동(메소드)```

### 메소드(method)
* 어떤 값을 주고 결과를 넘겨주는 것(행동)
* 선언법: 접근제어자, 리턴타입, 메소드 이름, (매개 변수) 순
    * ex. public boolean checkPassword(String password){}

### 변수(variable)
* 클래스의 특성을 결정짓는 상태 
* 선언: 타입 변수명;
    * ex. int a;

### 참고
* 중괄호 시작시 tab
* 계산식은 오른쪽에 작성
* ; 으로 줄 구분
* 예약어(public, class, int, return 등)은 다른 것에 이름으로 사용 불가

## 2장: Hello God Of Java
### 컴파일
* 내가 만든 프로그램 코드를 컴퓨터가 이해할 수 있도록 엮어주는 작업
* 컴파일러→디스크→JVM→운영체제
* .java소스를 컴파일 하면 .class확장자를 가진 파일이 생성됌
* .class는 바이너리 파일

### 바이너리파일
* 바이너리: 0과 1로 이루어진 2진법
* 2진수로 이루어진 파일

### main method
 * public static void main(String[] args){
}

### 메소드 내 단어
* public: 접근제어자
* static: 객체를 생성하지 않아도 호출할 수 있는 예약어
* void: return 값이 없는 것
* main: 메소드(method) 이름
* (String[] args): 소괄호 안은 매개변수 목록

### System.out.println()
* 화면에 뭔가 출력할 때 사용하는 것
* 메소드의 매개 변수로 문자열을 넘겨줌

### System.out.println() vs System.out.print()
* System.out.println(): 줄바꿈 O
* System.out.print(): 줄바꿈 X

### 주석(Comment)
* //: 한줄 주석
* /* */:  블록 주석
*  /** */: 문서용 주석

### 메소드
``` 리턴타입, 메소드이름, 메소드 내용 반드시 포함```
* 제어자(modifier): 메소드의 특성 ex. public
* 리턴 타입(return type): 메소드가 끝났을 때 반환하는 값
* 메소드 이름(method name): 소괄호 앞에 있는 메소드 이름
* 매개 변수 목록(paremeter list): 소괄호 안에 있는 매개 변수 목록
* 예외 목록(exception list): 메소드의 소괄호와 중괄호 시작하는 부분 사이에 있는 무언가
* 메소드 내용(method body): 중괄호 안에 있는 내용

## 3장: 자바를 제대로 알면 객체가 무엇인지를 알아야해요
### 객체
* Instance = Object
* 객체 이름은 간단하게
    * 길면 앞은 소문자, 다음 단어의 첫문자는 대문자

### 객체 생성
* new라는 예약어 사용
* 클래스 이름과 동일한 생성자 호출
* 객체를 생성해야 메소드 호출 가능

### 클래스 vs 객체
* 클래스는 대부분 그 자체만으로 일을 할 수 없고, 객체를 생성해야만 우리가 일을 시킬 수 있다.

### 생성자(constructor)
* 객체를 생성하기 위한 도구
* 기본생성자(default constructor): 매개변수가 없는 생성자
    * 클래스를 컴파일 할 때 javac를 실행하면 클래스 파일안에 자동 생성됌

## 4장: 정보를 어디에 넣고 싶은데
* 자바의 변수
    * 지역 변수(local variables): 중괄호 내에서 선언된 변수
    * 매개 변수(parameters): 메소드에 넘겨주는 변수
    * 인스턴스 변수(instance variables): 메소드 밖에, 클래스 안에서 선언된 변수로 staic 예약어가 없음
    * 클래스 변수(class variables): 메소드 밖에, 클래스 안에서 선언된 변수로 stiatic 예약어가 있음

```
public class VariableTypeKor{
    int 인스턴스_변수;
    static int 클래스_변수;
    public void method(int 매개_변수) {
        int 지역_변수;
    }
}
``` 

### 가비지 콜렉터(Garbage collector)
* 메모리 청소

### 변수 선언
* 하나의 메소드에서는 하나의 이름으로만 선언하자
* 선언한 중괄호 내에서의 같은 이름의 변수는 선언은 에러발생!

### 상수(constant value)
* 변하지 않는 값
* 단어와 단어사이 _로 구분
* 대문자로 지정

### 자바의 타입(자료형)
* 기본 자료형(Primitive data type): new 사용하지 않고 초기화
* 참조 자료형(Reference data type): new 예약어 사용하여 초기화
    * 예외) 문자열 초기화: String은 new 사용안해도 객체 생성 가능
        * String hwk1="Good";
        * String hwk2=new String("Good");

### 기본 자료형
* 정수형: byte, short, int, long, char
* 소수형: float, double
* 기타: boolean

### byte
* 8비트의 부호가 있는 타입
* 8비트=1byte
* 적은 공간에 보다 많은 내용을 저장할 수 있음

### 참고
* long타입: 명시적 지정은 숫자 뒤에 L 붙이기
* float: 32비트
* double: 64비트
* 지역변수는 초기화하자

---
## 책 정보
* 책제목: 자바의 신 1
* 지은이: 이상민
* 출판사: 로드북
