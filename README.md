# 이동교 202230124

## 04월 10일 (6주차)
#### README 파일 편집
~~~~java
import java.util.Scanner;

public class Ex313DivideByZeroHanding {

    public static void main(String[] args) {
        Scanner Scanner = new Scanner(System.in);
        int dividend;
        int divisor;

        System.out.print("나뉨수를 입력하시오:");
        dividend = scanner.nextInt();
        System.out.print("나눗수를 입력하시오:");
        divisor = scanner.nextInt();
        try {
            System.out.println(dividend+"를"+ divisor + "로 나누면 몫은 " + dividend/divisor + "닙니다.");

        }
        catch(ArithmeticException e) {
            System.out.println("0으로 나눌 수 없습니다");
        }
        Scanner.class();
    }
}
~~~~

### 입력 오류시 발생하는 오류

~~~~java
import java.util.Scanner;

public class Ex313DivideByZeroHanding {

    public static void main(String[] args) {
        Scanner Scanner = new Scanner(System.in);
        int dividend;
        int divisor;

        System.out.print("나뉨수를 입력하시오:");
        dividend = scanner.nextInt();
        System.out.print("나눗수를 입력하시오:");
        divisor = scanner.nextInt();
        try {
            System.out.println(dividend+"를"+ divisor + "로 나누면 몫은 " + dividend/divisor + "닙니다.");

        }
        catch(ArithmeticException e) {
            System.out.println("0으로 나눌 수 없습니다");
        }
        Scanner.class();
    }
}
~~~~
### 자바의 객체 지향 특성 : 상속
* 상속 : 상위 객체의 속성이 하위 객체에 물려 줌
*  하위 객체가 상위 객체의 속성을 모두 가지는 관계

### 자바의 상속
*   상위 클래스 : 수퍼 클래스
*  하위 클래스 : 서브 클래스, 수퍼 클래스 코드의 재사용, 새로운 특성 추가 가능

### 자바의 객체 지향 특성 : 다향성
*  다향성 : 같은 이름의 메소드가 클래스 혹은 객체에 따하 다르게 구현되는 것
*  메소드 오버로딩 : 한 클래스 내에서 같은 이름이지만 다르게 작동하는 여러 메소드
*  메소드 오버라이딩 : 슈퍼 클래스의 메소드를 동일한 이름으로 서브 클래스마다 다르게 구현 

### 객체 지향 언어의 목적
1. 소프츠웨어의 생산성 향상
*  소프트웨어를 빠른 속도로 생산할 필요성 증대

#### 객체 지향 언어
*  상솓, 다향성, 객체, 캡슐화 등 소프츠웨어 재사용을 위한 여러 장치 내장
*  소프트웨어 재사용과 부분 수정 빠름
*  소프트웨어를 다시 만드는 부담 대폭 줄임
* 소프트웨어 생산성 향상

2. 실세계에 대한 쉬운 모델링 
*  초기 프로그래밍
*  수학 계산/통계 처리를 하는 등 처리 과정,계산 절차 중요

### 절차 지향 프로그래밍과 객체 지향 프로그래밍
#### 절차 지향 프로그래밍
* 작업 순서를 표현하는 컴퓨터 명령 집합
* 합수들의 집합으로 프로그램 작성

#### 객체 지향 프로그래밍
* 컴퓨터가 수행 하는 작업을 객체들 간의 상호 작용으로 표현
* 클래스 혹은 객체들의 집합으로 프로그램 작성

### 클래스와 객체
#### 클래스 
* 객체의 속성과 행위 선언, 객체의 설계도 혹은 틀

#### 객체
* 클래스의 틀로 찍어낸 실체
* 프로그램 실행 중에 생성되는 실체
* 메모리 공간을 갖는 구체적인 실체
* 인스턴스라고도 부름

### 자바 클레스 구성
* 클래스 
* 맴버 : 클래스 구성 요소, 필드(멤버 변수)와 메소드(멤버 함수)
* 클래스에 대한 public 접근 지정 : 다른 모든 클래스에서 클래스 사용 허락
* 멤버에 대한 public 접근 지정 : 다른 모든 클래스에게 맴버 접근 허용 

### circle 클래스의 객체 생성 및 활용 
~~~~java
public class Ex41Circle {
    int radius;
    String name;

    public double getArea() {
        return 3.14 * radius * radius;
    }

public static void main(String[] args) {
    Ex41Circle pizza;
    pizza = new Ex41Circle();
    pizza.radius = 10;
    pizza.name = "자바피자";
    double area = pizza.getArea();
    System.out.println(pizza.name + "의 면적은 " + area);

    Ex41Circle donut = new Ex41Circle();
    donut.radius = 2;
    donut.name = "자바도넛";
    area = donut.getArea();
    System.out.println(donut.name + "의 면적은 " + area);
    }   
}
~~~~

### 객체 생성과 활용 
1. 래퍼런스 변수 선언 
* Circle pizza

2. 객체 생성
* new 연산자 이용 
* pizza = new Circle();

3. 객체 맴버 접근
* 점(.) 연산자 이용
* pizza.radius = 10;
* area = pizza.getArea();

#### 생성자 개념과 목적
#### 생성자 
* 객체가 생성될 때 초기화 목적으로 실행되는 메소드
* 객체가 생성되는 순간에 자동 호출

~~~~java
public class Ex43Circle {
    int radius;
    String name;

    public Ex43Circle() {
        radius = 1;
        name = "";
    }

    public Ex43Circle (int r, String n){
        radius = r;
        name = n;
    }
    public double getArea(){
        return 3.14 * radius * radius;
    }

    public static void main(String[] args) {
        Ex43Circle pizza = new Ex43Circle(10,"자바피자");
        double area = pizza.getArea();
        System.out.println(pizza.name + "의 면적은 " + area );


        Ex43Circle donut = new Ex43Circle();
        donut.name = "도넛피자";
        area = donut.getArea();
        System.out.println(donut.name + "의 면적은 " + area);
    }
}
~~~~

### 생성자의 특징
* 생성자 이름은 클래스 이름과 동일
* 생성자는 여러 개 작성 가능(생정자 중복)

#### 셍성지는 객체 생성시 한 번만 호출
* 자바에서 객체 생성은 반드시 new 연산자로 함

* 생성자의 목적은 객체 생성 시 초기화
* 생성자는 리턴 타입을 지정할 수 없음


## 04월 03일 (5주차)
#### README 파일 편집

### for문
~~~java
public class Ex31ForSample {
    public static void main(String[] args) {
        int i, sum = 0;

        for(i = 1; i <= 10; i++) {
            sum +=i;
            System.out.println(i);

            if (i <= 9)
                System.out.print("+");
            else{
                System.out.println("=");
                System.out.println(sum);

            }
        }
    }
~~~

### while문
~~~~java
import java.util.Scanner;

public class Ex32whilesSample {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int count = 0, n = 0;
        double sum = 0;

        System.out.println("정수를 입력하고 마지막에 0을 입력하세여.");
    while ((n = scanner.nextInt()) != 0) {
        sum = sum + n;
        count++;
    }
    System.out.print("수의 개수는 " + count + "개이며");
    System.out.println("평균은 " + sum/count + "입니다");
    }
}
~~~~

### do-while문
~~~java
public class Ex33DowhilesSample {
    public static void main(String[] args) {
        char a = 'a';

        do {
            System.out.print(a);
            a = (char) (a + 1);
        } while (a <= 'z');
    }
}
~~~

### 중첩 방복
~~~~java
public class Ex34NestedLoop {

    public static void main(String[] args) {
        
        for(int i =1; i < 10; i++){
            for (int j = 1; j < 10; j++){
                System.out.print(j + '*' + i +"=" + i * j);
                System.out.print('\t');
            }
            System.out.println();
        }
    }
}
~~~~

### continue문
~~~~java
import java.util.Scanner;

public class Ex35ContinueExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("정수를 5개 입력하세요.");
        int sum = 0;

        for(int i = 0; i < 5; i++){
            int n = scanner.nextInt();
            if(n <= 0) continue;
            else sum +=n;
        }
        System.out.println("양수의 합은 " + sum);

        scanner.close();
    }
}

~~~~
### break문
* 반복문 하나를 즉시 벗어날 떄 사용
* 중첩 반복의 경우 안쪽 반복문의 break문이 실행 되면 안쪽 반복문만 벗어남.



~~~~java
import java.util.Scanner;

public class Ex36BreakExample {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("exit를 입력하면 종료합니다.");

        while (true) {
            System.out.print(">>");
            String text = scanner.nextLine();
            if (text.equals("exit")) {
                break;
            }
            System.out.println("종료합니다");
            scanner.close();
        }
    }
}
~~~~

#### 자바 배열 
* 인덱스와 인덱스에 대응하는 데이터들로 이루어진 자료 구조로 한 번에 많은 메모리 공간 선언
* 같은 타입의 데이터들이 순차적으로 저장되는 공간으로 인덱스를 이용하여 원소 데이터 접근

### 배열 선언 및 생성 디테일
* 배열은 선언과 생성의 두 단계 필요 : 선언과 동시에 생성할 수 있음.
~~~~java
import java.util.Scanner;

public class Ex37ArrayAccess {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int intArray[];
        intArray =new int[5];
        
        int max = 0;
        System.out.println("양수 5개를 입역하세요.");

        for (int i = 0; i < 5; i++){
            intArray[i] = scanner.nextInt();
            if (intArray[i] > max)
                max = intArray[i];
        } 
        System.out.print("가장 큰 수는 " + max + "입니다.");

        scanner.close();
        
    }  
}
~~~~

### for-each문
*  배열이나 나열의 원소를 순차 접근하는데 유용한 for문

### 메소드의 배열 리턴
* 배열의 레퍼런스만 리턴 되며, 배열 전체가 리턴되는 것이 아님
#### 메소드의 리턴 타입
* 리턴하는 배열 타입과 리턴 받는 배열 타입 일치
* 리턴 타입에 배열의 크기를 지정하지 않음

### 자바의 예외 처리 
* 자바에서는 실행 중 발생하는 에러를 예외로 처리
#### 예외 발생 경우
* 점수를 0으로 나누는 경우
* 배열의 크기보다 큰 인뎃스로 배열의 원소를 접근하는 경우
* 정수를 읽는 코드가 실행되고 있을 떄 사용자가 문자를 입력한 경우 

### 예외 발생으로 응용프로그램이 강제 종료되는 경우 
~~~~java 
import java.util.Scanner;

public class Ex312DivideByZero {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int dividend;
        int divisor;

        System.out.print("나뉨수를 입력하시오:");
        dividend = scanner.nextInt();
        System.out.print("나눈수를 입력하시오:");
        divisor = scanner.nextInt();
        System.out.println(dividend+"를" + divisor + "로 나누면 몫은" + dividend/divisor + "입니다");
        scanner.close();
    }
}
~~~~
#### 자바의 예외 처리, try-catch-finally문
* 예외 처리 : 발생한 예외에 대해 개발자가 작성한 프로그램 코드에서 대응하는 것 
* try-catch-finally문, finally 블록은 생략 가능

## 3월 27일 (4주차)
#### README 파일 편집

### 자바의 특징(2)
#### 가비지 컬렉션 
* 자바 언어는 메모리 할당 기능은 있어도 메모리 반환 기능은 없음
* 사용하지 않는 메모리는 JVM에 의해 자동 반환 - 가비지 컬렉션

### 자바의 특징(3)
* 실시간 응용프로그럄애 부적합
* 타입 체크 엄격
* 자바는 바이트 코드를 인터프리터 방식으로 실행
* 기계어가 실행되는 것보다 느림

* 소스코드 : 사람이 읽을 수 있는 고수준 언어

* 바이트코드 : Java 컴파일러가 소스코드를 변환한 중간 코드, 바이트코드는JVM이 해석

* 기계어 : CPU가 직접 실행할 수 있는 0과 1의 이진코드

#### 바이트코드와 기계어 차이점 
* 바이트코드는 JVM이 실행하는 중간 코드 -> 운영체제와 CPU에 관계없이 사용
* 기계어는 CPU가 직접 실행하는 코드 -> 특정 하드웨어에 종속됨 

### 식별자 - 명명 규칙
* 식별자 : 클레스, 변수 상수, 메소드 등에 붙이는 이름

#### 식별자의 원칙
* '_','$'는 사용 가능
* 유니코드 문자 사용 가능, 한글 사용 X
* 키워드는 식별자로 사용불가
* 첫 번쨰 문자로 숫자는 사용불가
* '_',"$'를 시별자 첫 번쨰 문자로 일반적으로 잘 사용핮 않는다 
* 불린 리터럴과 널 리터럴은 식별자로 사용불가
* 길이제한 없음
* 대소문자 구별

### JAVA의 데이터 타입 
* 기본 자료형 : 8개
* 크기는 CPU나 운영체제에 따라 변하지 않음

#### 래퍼런스형의 용도는 3가지
* 클래스
* 인터페이스
* 배열

* 문자열은 String 클래스로 문자열 표현

### 참조 자료형 
* 주소를 저장할 수 없다
* JVM이 해당 주소로 안내
힙(Heap) 영역에 저장딘 객체의 메모리 주소
* 배열, 인터페이스, 혹은 열거형도 객체이기에 참조 자료형이다

### 참조 자료형을 사용 하는 이유
#### 메모리 안전성
* 잘못된 메모리 접근 문제가 발생 할 수 있다

#### 보안 강화 
* 버퍼 오버플로우 같은 보안 취약점 생길 가능성 높음
* 포인터를 활용한 해캉 기법은 JAVA에서 거의 불가능

### 메모의 구조 
* 힙(heap - FIFO)영역은 Java의 경우 JVM이 담당
* 스택 (stack - LIFO) 영역은 프로그램이 자동으로 사용하는 임시 메모리 영역 
* 힙이 스택을 침범 -> 힙 오버 플로우
* 스택이 힙을 침범 -> 스택 오버 플로우

### 변수의 선언 
* 번수 : 값을 임시로 저장 
* 변수 선언 : 데이터 타입에서 정한 크기의 메모리 할당

### 상수 선언ㄴ
* final 키워드 사용
* 상수 이름은 대문자

### var 키워드
* 타입을 생략하고 변수 선언
* 컴파일러가 추론하고 변수 타입 결정
* 변수 선언시 초기값 설정하지 않으면 컴파일 오류 발생

#### 좋게 사용하는 법
* 가독성이 명확 할 떄 사용 
* 상수를 적극 활용 


```java
public class Foo {
	public static void main(String[] args) {
		final double PI = 3.14;
		double radius = 10.2;
		double circleArea = radius*radius*PI;

		System.out.print("반지름" + radius + ", ");
		System.out.println("원의 면적 = " + circleArea);
	}
}
```

### 타입 변환
* 특정 데이터 타입의 값을 다른 데이터 타입의 값으로 변환
#### 자동 타입 변환
* 컴파일러에 의해 큰 타입으로 자동 변환

#### 강제 타입 변환 
* 개발자의 의도적 타입 변환

### 자바의 키 입력
#### System.in
* 자바의 표준 입력 스트림
* 바이트로 리턴하는 저수준 스트림

#### Scanner 클래스
* 바이트를 문자, 정수, 실수, 문자열, 불린 등 다양한 타입으로 변환하여 리턴, java.util.Scanner
* 객체를 생성해서 사용
* System.in에게 키를 읽게 하고, 원하는 타입으로 변환하여 리턴
* 입력되는 키 값을 공백으로 구분되는 토큰 단위로 읽움

### 연산자 
#### 산술 연산자 
* 더하기 (+), 빼기 (-), 곱하기(*), 나누기(/), 나머지(%)
#### 증감 연산자
* 증가 혹은 감소 시키는 연사 : ++, --
#### 대입 연산
* 연산의 오른쪽 결과는 왼쪽 변수에 대입
#### 비교 연산, 논리 연산
* 비교연산자 : 두개의 갑을 비교 true / false 결과
* 논리연산자 : 두 개의 논리 값에 논리 연산, 논리 결과
#### 조건 연산 
* 3 개의 피연산자로 구성된 삼항 연산자
```java 
public class prog_1 {
    public static void main(String[] args) {
        int a = 3, b = 5;

        System.out.println("두 수의 차는 " + ((a > b) ? ( a - b ) : (b - a)));
    }
}
```
#### 비트 연산 
* 비트 논리 연산 : 비트끼리 AND, OR, XOR, NOT 연산
* 비트 시프트 연산 : 비트를 오른쪽이나 왼쪽으로 이동

#### 비트 연산이 사용되는 경우 
1. 성능 최적화, 연산 속도 향상 : 곱셈,나눗셈 보다 비트 연산이 빠름
2. 퀀한 및 플래그 설정 : 여러 개의 상태를 하나의 int 변수에 저장할 떄
3. 데이터 압축 및 최적화 : 여러 개의 작은 값을 하나의 정수에 저장
4. 해싱 및 암호화 : 함수 및 암호화 알고리즘을 최적화
5. 빠른 연산 : 짝수/홀수 판별




## 3월 20일 (3주차)
#### README 파일 편집
* 절차지향언어 : 프로그램의 흐름을 순차적으로 처리
* 객체지향언어 : 데이터와 그 데이터를 다루는 함수(메서드)를 하나의 객체로 묶어서 사용

* 소스 : 프로그래밍 언어로 작성된 텍스트 파일
* 컴파일 : 소스 파일을 컴퓨터가 이해 할 수 있는 기계어로 만드는 과정
* 자바 : .JAVA -> .class
* C : .c -> .obj -> .exe

* 플랫폼 = 하드웨어 플랫폼 + 운영체제 플랫폼

* 바이트 코드 (.class)
* 자바 JVM에서 실행 가능한 바이너리 코드
* 자바 JVM이 인터프리터 방식으로 바이트 코드 해석

* JVM
* 플랫폼에 맞는 JVM울 제공,JVM저체는 플랫폼에 종속적
* 자바의 실행은 JM에서 클래스 파일(.class)을 바이트 코드 실행하는 것.

* javac , javadoc , jar , jmod , jilink , job , javap

API : JDK에 포함된 클래스 라이브러리

### 자바의 특징 (1)
* 플랫폼 독립성 : 하드웨어 운영 체제에 종속 되지 않는 바이트 코드로 플랫폼 독집성
*
### 자바의 특징 (2)
* 한 개의 class 파일 또는 다수의 class 파일로 구성
* 여러 폴더에 걸쳐 다수의 클래스 파일로 구성된 경우 : jar 압축 파일로 배포

* 패키지 : 서로 관련 있는 여러 클래스를 패키지로 묶어 관라(폴더 개념)

* 자바는 운영체제의 도움 없이 자체적으로 멀티스레드 지원


## 3월 13일 (2주차)
#### README 파일 편집

# h1 tag
## h2
### h3
#### h4
##### h5
###### h6

---

* 가가가
- 나나나

1. asda
2. asdasd
7. asdasd

```java
int firstNumber = 10;
int secondNumber = 5;
char operator = '+';
```
