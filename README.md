# 이동교 202230124
## 04월 18일 (8주차)
#### README 파일 편집

# static 메소드의 제약 조건 2
* static 메소드는 this 사용불가
* static 메소드는 객체 앖이도 사용 가능하므로, this 레퍼런스 사용할 수 없음

### final 필드
* final 필드 : 상수를 선언할 때 사용
* 상수는 필드 선언 시에 초기 값을 지정하여야한다

* final 클래스와 메소드
* final 클래스 - 더 이상 클래스 상속 불가능
* final 메소드 - 더 이상 오버라이딩 불가능

### 상속의 필요성
* 상속이 없는 경우 중복된 멤버를 가진 4개의 클래스

* 상속을 이용한 경우 중복이 제거되고 간결해진 클래스 구조 

### 클래스 상속과 객체
* 상속 선언 : exxtends 키워드 사용 
* 부모 클래스를 물려받아 자식 클래스를 확장한다는 의미
* 부모 클래스 -> 슈퍼 클래스
* 자식 클래스 -> 서브 클래스

### 클래스 상속
~~~~~java

import java.util.ResourceBundle.Control;

public class Ex51ColorPointEx {

    public static void main(String[] args) {
        Point p = new Point();
        p.set(1,2);
        p.showPoint();

        ControlPoint cp = new ColorPoint();
        cp.set(3,4);
        cp.setColor("red");
        cp.showColorPoint();

    }
}

class Point{
    private int x,y;
}
public void set(int x, int y) {
    this.x = x;
    this.y = y;
}


class ColorPoint extends Point {
    private String color;
}

public void setColor(String color) {
    this.color = color;
}

public void showColorPoint() {
    System.out.print(color);
    showPoint();
}
~~~~~

### 서브 클래스 객체의 모양
* 슈퍼 클래스 객체와 서브 클래스의 객체는 별개
* 서브 클래스 객체는 슈퍼 클래스 멤버 포함

### 자바 상속의 특징
* 클래스 다중 상속 불허 
* 하나의 클래스가 둘 이상의 부모 클래스를 동시에 상속받는 것을 말합니다.

* C++는 다중 상속 가능 
* C++는 다중 상속으로 멤버가 중복 생성되는 문제 있음
#### 부모 클래스 간에 계층적 관계가 있을 경우, 중복된 멤버가 생성될 수 있습니다.
#### 모호성 문제 : 두 부모 클래스에 동일한 이름의 멤버가 존재할 경우 어떤 부모의 멤버를 호출해야 할지 모호해집니다.

* 자바는 인터페이스의 다중 상속 허용
#### 다중 상속과 유사한 기능을 제공

* 모든 자바 클래스는 묵시적으로 object클래스 상속받음
* java.lang.Object는 클래스 모든 클래스의 슈퍼 클래스 

### 슈터 클래스의 멤버에 대한 서브 클래스의 접근
* 슈퍼 클래스의 private 멤버 : 서브 클래스에서 접근할 수 없음

* 슈퍼 클래스의 디폴트 멤버 : 서브 클래스가 동일한 패키지에 있을 떄 , 접근 가능

* 슈퍼 클래스의 public 멤버 : 서브 클래스는 항상 접근 가능 

* 슈퍼 클래스의 protected 멤버 : 같은 패키지 내의 모든 클래스 접근 허용 , 패키지 여부와 상관없이 서브 클래스는 접근 가능 

### protected 멤버 
* protected 멤버에 대한 접근 : 같은 패키지의 모든 클래스에게 허용 
* 상속되는 서브 클래스가 같은 패키지든 다른 패키지든 상관 없이 허용 

### 서브 클래스 / 슈퍼 클래스의 생성자 호출과 실행
* 서브 클래스의 객체가 생성될 때 : 슈퍼클래스 생성자와 서브 클래스 생성자 모두 실행
* 호출 순서 : 서브 클래스의 생성자 먼저 호출 -> 슈퍼 클래스 생성자 호출
* 실행 순서 : 슈퍼 클래스의 생성자가 먼저 실행 -> 서브 클래스의 생성자 실행

### 서브 클래스와 슈퍼 클래스의 생성자 선택
* 슈퍼 클래스와 서브 클래스 : 각각 여러 개의 생성자 작성 가능
* 서브 클래스의 객체가 생성될 때 : 슈퍼 클래스 생성자 1개와 서브 클래스 생성자 1개가 실행
*서브 클래스의 생성자와 슈퍼 클래스의 생성자가 결정되는 방식
1. 개발자의 명시적 선택 
* 서브 클래스 개발자가 슈퍼 클래스의 생성자 명시적 선택
* super() 키워드를 이용하여 선택
2. 컴파일러가 기본 생성자 선택
* 서브 클래스 개발자가 슈퍼 클래스의 생성자를 선택하지 않는 경우
* 컴파일러가 자동으로 슈퍼 클래스의 기본 생성자 선택

### super() 슈퍼 클래스의 생정자 명시적 선택
* super() : 서브 클래스에서 명시적으로 슈퍼 클래스의 생성자 선택 호출 
* 반드시 서브 클래스 생성자 코드의 제일 첫 라인에 와야 함

### super()를 활용한 ColorPoint 작성 
~~~~java
class Point1 {
    private int x, y;
    public Point1(){
        this.x = this.y = 0;
    }
    public Point1(int x, int y){
        this.x = x; this.y = y;
    }
    public void showPoint() {
        System.out.println("(" + x + ", "+ y +")");
    }
}

class ColorPoint1 extends Point1 {
    private String color;
    public ColorPoint1(int x, int y, String color){
        super(x,y);
        this.color = color;
    }
    public void showColorPoint() {
        System.out.print(color);
        showPoint();
    }
}
public class Ex525SuperEx {

    public static void main(String[] args) {
        ColorPoint1 cp = new ColorPoint1(5, 6, "blue");
        cp.showColorPoint();
    }
}
~~~~

### 업캐스팅 개념 
* 하위 클래스의 레퍼런스는 상위 클래스를 가리킬 수 없지만, 상위 클래스의 레퍼런스는 하위 클래스를 가리킬 수 있다는 설명

### 업캐스팅 
* 생물이 들어가는 박스에 사람이나 코끼리를 넣어도 무방, 모두 생물을 상속 받았기 때문
#### 업캐스팅 이란? 
* 서브  클래스의 래퍼런스를 슈퍼 클래스 레퍼런스에 대입
* 슈퍼 클래스 레퍼런스로 서브 클래스 객체를 가리키게 되는 현상
### 다운캐스팅 
* 슈퍼 클래스 레퍼런스 서브 클래스 레퍼런스에 대입
* 업캐스팅 된 것을 다시 원래대로 되돌리는 것
* 반드시 명시적 타입 변환 지정  

### 업캐스팅 레퍼헌스로 객체 구별
* 업캐스팅된 레퍼런스로는 객체의 실제 타입을 구분하기 어려움
* 슈퍼 클래스는 여러 서브 클래스에 상속되기 떄문

### instanceof 연산자 사용 
* 레퍼전스가 가리키는 객체의 타입 시별 : 연산의 결과는 true/false의 불린 값으로 반환 

### 메소드 오버라이딩의 개념 
*서브 클래스에서 슈퍼 클래스의 메소드 중복 작성
* 슈퍼 클래스의 메소드 무력화, 항상 서브 클래스에 오버라이딩한 메소드가 실행되도록 보장됨 
* '메소드 무시하기'로 번역되기도 함 
#### 오버라이딩 조건
* 슈퍼 클래스 메소드의 원형 동일하게 작성

### 오버라이딩의 목적, 다형성 실현
* 오버라이딩으로 다형성 실현
* 하나의 인터페이스에 서로 다른 구현 
* 슈퍼 클래스의 메소드를 서브 클래스에서 각각 목적에 맞게 다르게 구현 

### 메소드 오버라이딩으로 다형성 실현 
~~~~java
class Shape {
    public void draw() {
        System.out.println(("Shape"));
    }
}

class Line extends Shape {
    public void draw() {
        System.out.println("Line");
    }
}

class Rect extends Shape {
    public void draw() {
        System.out.println("Rect");
    }
}

class Circle extends Shape {
    public void draw() {
        System.out.println("Circle");
    }
}

public class Ex54MethodOverridingEx {
    static void paint(Shape p){
        p.draw();
    }

    public static void main(String[] args) {
        Line line = new Line();
        paint(line);

        paint(new Shape());
        paint(new Line());
        paint(new Rect());
        paint(new Circle());
    }
}
~~~~

### 동적 바인딩 - 오버라이딩된 메소드 호출
* SuperObject 하나만 있는 응용프로그램의 경우 혹은 상속받은 경우 모두 동적 바인딩을 한다.
* 오버라이딩 메소드가 항상 호출된다.
* SuperObject는 키워드가 아니다.

### super 키워드로 슈퍼 클래스의 멤버 접근 
* 슈퍼 클래스의 멤버를 접근할 때 사용되는 레퍼런스 super.슈퍼클래스의 멤버
* 서브 클래스에서만 사용
* 슈퍼클래스의 필드 접근 
* 슈퍼 클래스의 메소드 호풀 시 super로 이루어지는 메소드 호출 : 정적 바인딩 



## 04월 17일 (7주차)
#### README 파일 편집

### 기본 생성자 : 매개 변수 없고, 아무 작업 없이 단순 리턴하는 생성자
~~~~java
class Circle {
    public Circle() { } //기본생성자
}
~~~~
### 기본 생성자가 자동 생성되는 경우
* 클래스에 생성자가 하나도 선언되어 있지 않을 때
* 컴파일러에 의해 기본 생성자 자동 생성 

### 생성자의 종류
* 기본 생성자가 자동 생성되지 않는 경우
* 클래스에 생성자가 선언되어 있는 경우
* 컴파일러는 기본 생성자를 자동 생성해 주지 않는다

### this 래퍼런스
* 객체 자신에 대한 레퍼런스
* 컴파일러에 의해 자동 관리, 개발자는 사용하기만 하면 됨
* this.멤버 형태로 멤버를 접근할 떄 사용

### this()로 다른 생성자 호출
* 같은 클래스의 다른 생성자 호출
* 생성자 내에서만 사용 사능
* 셍성자 코드의 제일 앞에 있어야 함
* this() 사용 실패 사례

### 객체 배열 
* 객체에 대한 레퍼런스 배열
* 자바의 객체 배열 만들기 3 단계
1. 배열 레퍼런스 변수 선언
2. 레퍼런스 배열 생성
3. 배열의 각 원소 객체 생성

### Circle 배열 만들기
~~~~java
class Circle {
    int radius;


    public Circle(int radius){
        this.radius = radius;
    }
    public double getArea() {
        return 3.14 * radius * radius;
    }

}

public class Ex46CircleArray {
    public static void main(String[] args) {
        Circle[] c;
        c = new Circle[5];

        for (int i = 0; i < c.length; i++)
        c[i] = new Circle(i);

        for (int i = 0; i < c.length; i++)
            System.out.print((int) (c[i].getArea()) + " ");
    }



}
~~~~

~~~~java
import java.util.Scanner;

class Book {
    String title,author;
    public Book(String title, String author){
        this.title = title;
        this.author = author;
    }
}

public class Ex47BookArray {
    public static void main(String[] args) {
        Book [] book = new Book[2]; // Book 배열 선언

        Scanner scanner = new Scanner(System.in);
        for(int i = 0; i < book.length; i++) {
            System.out.println("제목>>");
            String title = scanner.nextLine();
            System.out.println("저자>>");
            String author = scanner.nextLine();
            book[i] = new Book(title, author); //배열 원소 객체 생성
        }
            for(int i = 0; i < book.length; i++)
                System.out.print("(" + book[i].title + ", " + book[i].author + ")");
            scanner.close();
    }
 }
~~~~


### 메소드 
* 메소드는 C/C++의 함수와 동일 
* 자바의 모든 메소드는 반드시 클래스 안에 있어야 함(캡슐화 원칙)
* 메소드 형식

#### 접근 지정자 : 다른 클래스에서 메소드를 접근할 수 있는지 여부 선언
* public , private, pritected, 디폴트(접근 지정자 생략)
#### 리턴 타입 : 메소드가 리턴하는 값의 데이터 타입

### 인자 전달 - 기본 타입의 값이 전달되는 경우
* 매개 변수가 byte, int, double 등 기본 타입으로 선언되었을 때 
* -> 호춯자가 건네는 값이 매개 변수에 복사되어 전달. 실 인자 값은 변경되지 않음

### 인자 전달 - 객체가 전달되는 경우
* 객체의 래퍼런스만 전달 : 매개 변수가 실 인자 객체 공유 

### 인자 전달 - 배열이 전달되는 경우
* 배열 레퍼런스만 매게 변수에 전달 : 배열 통째로 전달되지 않음
* 객체가 전달되는 경우 동일 : 매개 변수가 실인자의 배열 공유



### 메소드 오버로딩 
* 한 클래스 내에서 두 개 이상의 이름이 같은 메소드 작성
* 메소드 이름이 동일해야 함
* 매개 변수의 개수 혹은 타입이 달라야 함
* 리턴 타입은 오버로딩과 관련 없음

### 오버로딩 살패 사례
* 매개 변수의 개수와 타입이 같기 때문에 오버로딩 실패

### 인자로 배열이 전달되는 얘
~~~~java
public class Ex48Arrayparameter {
    static void replaceSpace(char a[]) {
        for (int i = 0; i < a.length; i++)
        if (a[i] == ' ')
            a[i] = ',';
    }

    static void printCharArray(char a[]){
        for (int i = 0; i < a.length; i++)
            System.out.print(a[i]);
        System.out.println();
    }   

    public static void main(String[] args) {
        char c[] = {'T','h','i','s',' ','i','s',' '
                        ,'a',' ','p','e','n','c','i','l','.'};
        printCharArray(c);
        replaceSpace(c);
        printCharArray(c);                
    }
}
~~~~


### 객체 치환 시 주의할 점
* 객체 치환은 객체 복사가 아니며, 래퍼런스의 복사이다.

### 객체 소멸
* new로 할당 받은 객체와 메모리를 JVM으로 되돌려 주는 행위
* 자바는 객체 소멸 연산자 없음
* 객체 소멸은 JVM의 고유한 역할

* C/C++에서는 할당 받은 객체를 개발자가 프로그램 내에서 삭제해야 함
* C/C++의 프로그램 작성을 어렵게 만드는 요인
* 자바에서는 사용하지 않는 객체나 배열을 돌려주는 코딩 책임으로부터 개발자 해방

### 기비지 
* 가리키는 래퍼런스가 하나도 없는 객체
* 더 이상 접근할 수 업어 사용할 수 없게 된 메모리
* 가비지 컬렉션 : 자바 가상 기계의 가비지 컬렉터가 자동으로 가비지 수집, 반환

### 가비지의 발생 
~~~~java 
public class Ex49GarbageEx {
    public static void main(String[] args) {
        String a = new String("Good");
        String b = new String("Bad");
        String c = new String("Normal");
        String d,e;
        a= null;
        d = c;
        c = null;
    }
}
~~~~

### 가비지 컬렉션
* JVM이 가비지 자동 회수
* 가용 메모리 공간이 일정 이하로 부족해질 떄
* 가비지를 수거하여 가용 메모리 공간으로 확보
* 가비지 컬렉터에 의해 자동 수행

* 강제 가비지 컬렉션 강제 수행 : System 또는 Runtime 객체의 gc() 메소드 호출
~~~~java
System.gs(); // 가비지 컬렉션 작동 요청
~~~~
* 이 코드는 JVM에 강역한 가비지 컬렉션 요청
* 그러나 JVM이 가비지 컬렉션 시점을 전적으로 판단

자바의 패키지 개념
#### 패키지
* 상호 관련 있는 클래스 파일(컴파일된 .class)을 저장하여 관리하는 디렉터리 
* 자바 응용프로그램은 하나 이상의 패키지로 구성 

### 접근 지정자
* 자바의 접근 지정자 4가지 : private, protected, public, 디폴트(접근 지정자 생략)
* 접근 지정자 목격
* 클래스나 일부 멤버를 공개하여 다른 클래스에서 접근하도록 허용
* 객체 지향 언어의 캡슐화 정책은 멤버를 보호하는 것
* -> 접근 지정은 캡슐화 묶인 보호를 일부 해제할 목적으로 사용
* 접근 지정자에 따른 클래스나 멤버의 공개 범위


### 클래스 접근 지정
* 다른 클래스에서 사용하도록 허용할 지 지정
* public 클래스 : 다른 모든 클래스에게 접근 허용
* 디폴트 클래스(접근 지정자 생략) : 같은 패키지의 클래스에만 접근 허용

### 맴버 접근 지정
* public 멤버 : 패키지에 관곙 없이 모든 클래스에게 접근 허용
* private 멤버 : 동일 클래스 내에만 접근 허용 . 상속 받는 서브 클래스에서 접근 불가.
* portected 멤버 : 
* 같은 패키지 내의 다른 모든 클래스에게 접근 허용
* 상속 받은 서브 클래스는 다른 패카자에 있어도 접근 가능 
* 디폴트 멤버 : 같은 패키지 내의 다른 클래스에게 접근 허용 

### static 멤버 
#### static 멤버 선언 
~~~~java
class StaticSample {
    int n;          //  non-static 필드
    void g() {...}  //  non-static 메소드
    static int m;   //  static 필드
    static void f() {...} // static 메소드 
}
~~~~
#### 겍체 생성과 non-static 멤버의 생성 
* non-static 멤버는 객체가 생성될 때,객체마다 생긴다.

* 객체마다 n,g()의 non-static 맴버들이 생긴다.
* # non-static 모든 객체에 멤버 생성, static은 멤버 공유!

### static 멤버의 생성
* static 멤버는 클래스당 하나만 생성
* 객체 등에 의해 공유됨

### static 멤버 사용 
#### 클래스 이름으로 접근 가능 
~~~~java
StaticSample.m = 3;
StaticSample.f = f();
~~~~
#### 객체의 멤버로 접근 가능 
~~~~java
StaticSample b1 = new StaticSample();
b1.m = 3;
b1.f();
~~~~
#### non-static 멤버는 클래스 이름으로 접근 안 됨
~~~~java
StaticSample.n = 5;
StaticSample.g();
~~~~

### static 활용
* 전역 변수와 전역 함수를 만들 떄 활용
* 공유 멤버를 만들 때 : static으로 선언한 멤버는 클래스의 객체들 사이에 공유

### static 멤버를 가진 Calc 클래스 작성
~~~~java
class Calc {
    public static int abs(int a) {return a> 0?a: -a;}
    public static int max(int a, int b) {return (a>b)?a:b;}
    public static int min(int a, int b) {return (a>b)? b:a;}
}



public class Ex411CalcEx {
    public static void main(String[] args) {
        System.out.println(Calc.abs(-5));
        System.out.println(Calc.max(10, 8));
        System.out.println(Calc.min(-3, -8));
    }
}
~~~~

### static 메소드의 제약 조건1
* static 메소드는 오직 static 멤버만 접근 가능
* 객체가 생성되지 않은 상황에서도 static 메소드는 실행될 수 있기 때문에, non-static 멤버 활용 불가
*  non-static 메소드는 static 멤버 사용 가능


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
