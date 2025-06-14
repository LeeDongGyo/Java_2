# 이동교 202230124

## 06월 05일 (13주차) 
#### README 파일 편집
### 이벤트 리스너 작성 방법
#### 3가지 
#### 독립 클래스로 작성
* 이벤트 리스너를 완전한 클래스로 작성
* 이번트 리스너를 여러 곳에서 사용할 떄 적합 

#### 내부 클래스로 작성
* 클래스 안에 멤버처럼 클래스작성 
이번트 리스너를 특정 클래스에서만 사용할 떄 적합

#### 익명 클래스로 적합
* 클래스의 이름 없이 간단한 리스너 작성
* 클래스 조차 만들 필요 없이 리스너 코드가 간단한 경우에 적합 

### 예제 9-1 : 독립 클래스로 Action 이벤트 리스너 만들기 
~~~~java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class INdepClassListener extends JFrame {
    public IndepClassListener() {
        setTitle("Action 이벤트 리스너 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane();
        c.setLayout(new FlowLayout());
        JButton btn = new JButton("Action");
        btn.addActionListener(new Ex9MyActionListener());
        c.add(btn);
        setSize(250, 120);
        setVisible(true);
    }

    public static void main(String[] args) {
        new IndepClassListener();
    }
}

// 독립된 클래스로 이벤트 리스너를 작성한다.
class Ex9MyActionListener implements ActionListener {
    public void actionPerformed(ActionEvent e) {
        JButton b = (JButton)e.getSource();
        if(b.getText().equals("Action"))
            b.setText("액션");
        else
            b.setText("Action");
    }
}
~~~~

### INdepClassListener2
~~~~java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class INdepClassListener2 extends JFrame {
    public INdepClassListener2() {
        setTitle("Action 이벤트 리스너 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane();
        c.setLayout(new FlowLayout());
        JButton btn = new JButton("Action");
        btn.addActionListener(new Ex9MyActionListener());
        c.add(btn);
        setSize(250, 120);
        setVisible(true);
    }

    // 내부 클래스로 Action 리스너를 작성한다.
    private class Ex9MyActionListener implements ActionListener {
        public void actionPerformed(ActionEvent e) {
            JButton b = (JButton) e.getSource();
            if (b.getText().equals("Action"))
                b.setText("액션");
            else
                b.setText("Action");
            // InnerClassListener나 JFrame의 멤버 호출 가능
            // setTitle(b.getText()); // 프레임 타이틀에 버튼문자열 출력
        }
    }

    public static void main(String[] args) {
        new INdepClassListener2();
    }
}
~~~~

### 익명 클래스로 이벤트 리스너 작성
* 익명 클래스 : 이름 없는 클래스 (클래스 선언 + 인스턴스 생성)을 한번에 달성 

* 간단한 리스너의 경우 익명 클래스 사용 추천
* 메소드의 개수가 1,2개인 리스너에 대해 주로 사용


### 예제 9-4 : 마우스 이벤트 리스너 작성 - 마우스로 문자열 이동시키기 

~~~~java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class Ex9_4MouseListenerEx extends JFrame {
    private JLabel la = new JLabel("Hello");

    public Ex9_4MouseListenerEx() {
        setTitle("Mouse 이벤트 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane();
        c.setLayout(null);

        la.setSize(50, 20);
        la.setLocation(30, 30);
        c.add(la);

        c.addMouseListener(new MyMouseListener());

        setSize(200, 200);
        setVisible(true);
    }

    class MyMouseListener implements MouseListener {
        public void mousePressed(MouseEvent e) {
            int x = e.getX();
            int y = e.getY();
            la.setLocation(x, y);
        }
        public void mouseReleased(MouseEvent e) {

        }
        public void mouseClicked(MouseEvent e) {

        }
        public void mouseEntered(MouseEvent e) {

        }
        public void mouseExited(MouseEvent e) {

        }
    }

    public static void main(String[] args) {
        new Ex9_4MouseListenerEx();
    }
}
~~~~

### 어댑터 클래스
#### 이벤트 리스너 구현에 따른 부담
* 리스너의 추상 메서드를 모두 구현해야 하는 부담
* 예 마우스 리스너에서 마우스가 눌러지는 경우(mousePressed())만 처리하고자 하는 경우에도 나머지 4개의 메서드를 모두 구현해야 하는 부담
#### MouseAdapter 예
~~~~java 
class MouseAdapter implements MouseListener, MouseMotionListener, MouseWheelListener {
public void mousePressed(MouseEvent e) {}
public void mouseReleased(MouseEvent e) {}
public void mouseClicked(MouseEvent e) {}
public void mouseEntered(MouseEvent e) {}
public void mouseExited(MouseEvent e) {}
public void mouseMoved(MouseEvent e) {}
public void mouseDragged(MouseEvent e) {}
public void mouseWheelMoved(MouseWheelEvent e) {}
}
~~~~ 

### 어댑터 클래스(Adapter)
* 리스너의 모든 메서드를 단순 리턴하도록 만든 클래스(JDK에서 제공)

* 추상 메소드가 하나뿐인 리스너는 어댑터 없음
* ActionAdapter, ItemAdapter 클래스는 존재하지 않음


### Key 이벤트와 포커스
#### 키 입력시, 다음 세 경우 각각 Key 이벤트 발생
* 키를 누르는 순산 
* 누른 키를 떄는 순간
* 누른 키를 떼는 순간 

#### 카 아밴트를 받을 수 있는 조건
* 모든 컴포넌트
* 현재 포커스를 가진 컴포넌트가 키 이벤트 독점

#### 포커스 
* 컴포넌트나 응용프로그램이 키 이벤트를 독점하는 권한
* 컴포넌트에 포커스 설정 방법 : 다음 2 라인 코드 필요 
~~~~java
 componet.sertFousable(ture);
 componet.requestFousable();
~~~~
* 자바플랫폼마다 실행 환경의 초기화가 서로 다를 수 있기 떄문에 다음 코드가 필요하다 
~~~~java
componet.sertFousable(ture);
~~~~

### KeyListener 
* 응용프로그램에서 KeyListener를 상속받아 키 리스너 구현

#### KeyListener의 3개 메소드
* 키 리스너(KeyListener)
~~~~java
void keyPressed(KeyEvent e) { // 이벤트 처리 루틴 
}
void keyReleased(KeyEvent e) { // 이벤트 처리 루틴 
}
void keyTyped(KeyEvent e) { // 이벤트 처리 루틴 
}
~~~~

#### 컴포넌트에 키 이벤트 리스너 달기
~~~~java
component.addKeyListener(myKeyListener);
~~~~

### 유니코드(Unicode) 키
#### 유니코드 키의 특징
* 국제 산업 표준
* 전 세계의 문자를 컴퓨터에서 일관되게 표현하기 위한 코드 체계
* 문자들에 대해서만 키 코드 값 정의 : A-Z, a-z, 0-9, !, @, & 등

#### 문자가 아닌 키 경우에는 표준화된 키 코드 값 없음
* <Function> 키, <Home> 키, <Up> 키, <Delete> 키, <Control> 키, <Shift> 키, <Alt> 키, 등은 플랫폼에 따라 키 코드 값이 다를 수 있음

#### 유니코드 키가 입력되는 경우
* keyPressed(), keyTyped(), keyReleased() 가 순서대로 호출

#### 유니코드 키가 아닌 경우
* keyPressed(), keyReleased() 만 호출됨


### 가상 키와 입력된 키 판별
#### KeyEvent 객체
* 입력된 키 정보를 가진 이벤트 객체
* KeyEvent 객체의 메소드로 입력된 키 판별

#### KeyEvent 객체의 메소드로 입력된 키 판별
* char KeyEvent.getKeyChar()
* 키의 유니코드 문자 값 리턴
* Unicode 문자 키인 경우에만 의미 있음
* 입력된 키를 판별하기 위해 문자 값과 비교하면 됨
~~~~java
public void keyPressed(KeyEvent e) {
    if(e.getKeyChar() == 'q')
        System.exit(0);
}
~~~~
q 키가 누르면 프로그램 종료

#### int KeyEvent.getKeyCode()
* 유니코드 키 포함
* 모든 키에 대한 정수형 키 코드 리턴
* 입력된 키를 판별하기 위해 가상키(Virtual Key) 값과 비교해야 함
* 가상 키 값은 KeyEvent 클래스에 상수로 선언
~~~~java
public void keyPressed(KeyEvent e) {
    if(e.getKeyCode() == KeyEvent.VK_F5)
        System.exit(0);
}
~~~~ 
F5 키를 누르면 프로그램 종료


### 예제 9-6 : KeyListeneer 활용 - 입력된 문자 키 판별 
~~~~java
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class Ex9_6KeyCharEx extends JFrame {
    private JLabel la = new JLabel("<Enter>키로 배경색이 바뀝니다.");

    public Ex9_6KeyCharEx() {
        super("KeyListener의 문자 키 입력 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container c = getContentPane(); // 컨텐트 팬 알아내기
        c.setLayout(new FlowLayout());
        c.add(la);
        c.addKeyListener(new MyKeyListener()); // 키 리스너 달기
        setSize(250, 150);
        setVisible(true);

        c.setFocusable(true); // 컨텐트팬이 포커스를 받을 수 있도록 설정
        c.requestFocus();     // 컨텐트팬에 포커스 설정. 키 입력 가능해짐
    }

    class MyKeyListener extends KeyAdapter { // 키 리스너
        public void keyPressed(KeyEvent e) {
            int r = (int)(Math.random() * 256); // 0~255 사이의 임의의 red 색상
            int g = (int)(Math.random() * 256); // 0~255 사이의 임의의 green 색상
            int b = (int)(Math.random() * 256); // 0~255 사이의 임의의 blue 색상

            switch (e.getKeyChar()) { // 입력된 키 문자
                case '\n': // <Enter> 키 입력
                    la.setText("r=" + r + ", g=" + g + ", b=" + b);
                    getContentPane().setBackground(new Color(r, g, b)); // 컨텐트팬의 배경색 변경
                    break;
                case 'q': System.exit(0); // 프로그램 종료
            }
        }
    }

    public static void main(String[] args) {
        new Ex9_6KeyCharEx();
    }
}
~~~~


### 예제 9-7 : KeyListener 활용 - 상, 하, 좌, 우 키로 문자열 움직이기 
~~~~java 
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;

public class Ex9_7FlyingTextEx extends JFrame {
    private JPanel contentPane = new JPanel();
    private JLabel la = new JLabel("HELLO");

    public Ex9_7FlyingTextEx() {
        super("상,하,좌,우 키를 이용하여 텍스트 움직이기");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        Container c = getContentPane();
        c.setLayout(null);
        c.addKeyListener(new MyKeyListener());

        la.setLocation(50, 50);
        la.setSize(100, 20);
        c.add(la);

        setSize(200, 200);
        setVisible(true);

        c.setFocusable(true); // 컨텐트팬이 포커스를 받을 수 있도록 설정
        c.requestFocus();     // 포커스 지정
    }

    class MyKeyListener extends KeyAdapter {
        public void keyPressed(KeyEvent e) { // 입력된 키코드
            int keyCode = e.getKeyCode();
            switch (keyCode) {
                case KeyEvent.VK_UP:
                    la.setLocation(la.getX(), la.getY() - 10);
                    break;
                case KeyEvent.VK_DOWN:
                    la.setLocation(la.getX(), la.getY() + 10);
                    break;
                case KeyEvent.VK_LEFT:
                    la.setLocation(la.getX() - 10, la.getY());
                    break;
                case KeyEvent.VK_RIGHT:
                    la.setLocation(la.getX() + 10, la.getY());
                    break;
            }
        }
    }
}
~~~~

#### Mouse 이벤트와 MouseListener, MouseMotionListener
### Mouse 이벤트 : 사용자의 마우스 조작에 따라 발생하는 이벤트
* Mouse 이벤트가 발생하는 경우 리스너의 메소드	리스너
* 마우스가 컴포넌트 위에 올라갈 때
* 리스너의 메소드 void mouseEntered(MouseEvent e)	
* 리스너 MouseListener

* 마우스가 컴포넌트에서 내려올 때	
* 리스너의 메소드 void mouseExited(MouseEvent e)	
* 리스너 MouseListener

* 마우스 버튼이 눌러졌을 때	
* 리스너의 메소드 void mousePressed(MouseEvent e)	
* 리스너 MouseListener

* 눌러진 버튼이 떼어질 때	
* 리스너의 메소드 void mouseReleased(MouseEvent e)
* 리스너 MouseListener

* 마우스로 컴포넌트를 클릭하였을 때
* 리스너의 메소드 void mouseClicked(MouseEvent e)	
* 리스너 MouseListener

* 마우스가 드래그 되는 동안	
리스너의 메소드 void mouseDragged(MouseEvent e)	
* 리스너 MouseMotionListener

* 마우스가 움직이는 동안	
* 리스너의 메소드 void mouseMoved(MouseEvent e)	
* 리스너 MouseMotionListener

* mouseClicked() : 마우스가 눌려진 위치에서 그대로 떼어질 때 호출
* mouseReleased() : 마우스가 눌려진 위치에서 그대로, 떼어지는
아니든 항상 호출
* mouseDragged() : 마우스가 드래그되는 동안 계속 여러번 호출

#### 마우스가 눌려진 위치에서 떼어지는 경우 메소드 호출 순서
~~~~java
mousePressed(), mouseReleased(), mouseClicked()
~~~~
####  마우스가 드래그될 때 호출되는 메소드 호출 순서
~~~~java
mousePressed(), mouseDragged(), mouseDragged(), ..., mouseDragged(), mouseReleased()
~~~~


### 마우스 리스너 달기와 MouseEvent 객체 활용
#### 마우스 리스너 달기
* 마우스 리스너는 컴포넌트에 다음과 같이 등록
~~~~java
component.addMouseListener(myMouseListener);
~~~~ 

* 컴포넌트가 마우스 무브(mouseMoved())나 마우스 드래깅(mouseDragged())을 함께 처리하고자 하면, MouseMotion 리스너 따로 등록
~~~~java
component.addMouseMotionListener(myMouseMotionListener);
~~~~

#### MouseEvent 객체 활용
* 마우스 포인터의 위치, 컴포넌트 내 상대 위치 : int getX(), int getY()
~~~~java
public void mousePressed(MouseEvent e) {
    int x = e.getX();   // 마우스가 눌러진 x 좌표
    int y = e.getY();   // 마우스가 눌러진 y 좌표
}
~~~~
#### 마우스 클릭 횟수 : int getClickCount()
~~~~java
public void mouseClicked(MouseEvent e) {
    if(e.getClickCount() == 2) {
        // 더블클릭 처리 루틴
    }
}
~~~~


### 자바의 GUI 프로그래밍 방법
#### [ 자바의 GUI 프로그래밍 방법 2 종류 ]
#### 컴포넌트 기반 GUI 프로그래밍
* 스윙 컴포넌트를 이용하여 쉽게 GUI를 구축
* 자바에서 제공하는 컴포넌트의 한계를 벗어나지 못함

#### 그래픽을 이용하여 GUI 구축
* 그래픽 기반 GUI 프로그래밍
* 개발자가 직접 그래픽으로 화면을 구성하는 부담
* 독특한 GUI를 구성할 수 있는 장점
* GUI 처리의 실행 속도가 빨라, 게임 등에 주로 이용


### 스윙 컴포넌트의 공통 메소드, JComponent의 메소드
#### JComponent
* 스윙 컴포넌트의 멤버를 모두 상속받는 슈퍼 클래스, 추상 클래스
* 스윙 컴포넌트들이 상속받는 공통 메소드와 상수 구현
* JComponent의 주요 메소드 사례

#### 컴포넌트의 모양과 관련된 메소드
~~~~java
void setForeground(Color) : 전경색 설정
void setBackground(Color) : 배경색 설정
void setOpaque(boolean) : 불투명성 설정
void setFont(Font) : 폰트 설정
Font getFont() : 폰트 리턴
~~~~

#### 컴포넌트의 상태와 관련된 메소드
~~~~java
void setEnabled(boolean) : 컴포넌트 활성화/비활성화
void setVisible(boolean) : 컴포넌트 보이기/숨기기
boolean isVisible() : 컴포넌트의 보이는 상태 리턴
~~~~

#### 컴포넌트의 위치와 크기에 관련된 메소드
~~~~java
int getWidth() : 폭 리턴
int getHeight() : 높이 리턴
int getX() : x 좌표 리턴
int getY() : y 좌표 리턴
Point getLocationOnScreen() : 스크린 좌표상에서의 컴포넌트 좌표
void setLocation(int, int) : 위치 지정
void setSize(int, int) : 크기 지정
~~~~

#### 컨테이너를 위한 메소드
~~~~java
Component add(Component) : 자식 컴포넌트 추가
void remove(Component) : 자식 컴포넌트 제거
void removeAll() : 모든 자식 컴포넌트 제거
Component[] getComponents() : 자식 컴포넌트 배열 리턴
Container getParent() : 부모 컨테이너 리턴
Container getTopLevelAncestor() : 최상위 부모 컨테이너 리턴
~~~~


### 다른 컴포넌트의 메소드
#### 앞서 살펴본 바와 같이 JComponent의 메소드를 상속 받기 때문에 이 장에서 설명하는 컴포넌트의 사용법의 거의 동일합니다.

#### 다음 예를 비교해 보면 알 수 있듯이 JButton, JCheckBox, JRadioButton, JTextField, JTextArea, JList, JComboBox 모두 사용하는 메소드는 JLabel과 유사합니다.

#### 사용하고 싶은 컴포넌트를 골라 예제 10-1을 참고하여 코드를 작성하면 됩니다.
~~~~java
JLabel(이미지 레이블)
JLabel(Icon image) 이미지 레이블
JLabel(String text) 문자열 레이블
JLabel(String text, Icon image, int hAlign) 문자열과 이미지 모두 가진 레이블
hAlign: 수평 정렬값. SwingConstants.LEFT, SwingConstants.RIGHT, SwingConstants.CENTER 중 하나
~~~~
~~~~java
JButton(버튼)
JButton(Icon image) 이미지 버튼
JButton(String text) 문자열 버튼
JButton(String text, Icon image) 문자열과 이미지 모두 가진 버튼
~~~~ 
~~~~java
JCheckBox(체크박스)
JCheckBox() 빈 체크박스
JCheckBox(String text) 문자열 체크박스
JCheckBox(String text, boolean selected) 문자열 체크박스, 선택 여부 지정
JCheckBox(Icon image) 이미지 체크박스
JCheckBox(Icon image, boolean selected) 이미지 체크박스, 선택 여부 지정
JCheckBox(String text, Icon image) 문자열과 이미지 모두 가진 체크박스
JCheckBox(String text, Icon image, boolean selected) 문자열과 이미지 모두 가진 체크박스, 선택 여부 지정
~~~~

### 나머지 챕터의 내용 정리

#### 나머지 4개의 챕터의 내용은 다음과 같습니다. 필요에 따라서 선택적으로 학습하면 됩니다.

#### 11장 그래픽 : paintComponent() 활용하여 app에 직접 그림을 그리는 방법

#### 12장 자바 스레드 기초 : 멀티 태스킹과 스레드의 개념

#### 13장 입력과 스트림과 파일 입력 : 자바의 입력과 스트림, 텍스트와 바이너리 File 입출력

#### 14장 자바 소켓 프로그래밍 : 소켓 통신에 대한 이해. 인터넷 통신.

# 복습이 필요하다면 4장 클래스와 객체, 5장 상속, 8장 자바 GUI 스윙 기초, 9장 자바의 이벤트 처리를 다시 한번 학습하세요.




## 05월 29일 (12주차) 
#### README 파일 편집

### 컨테이너와 컴포넌트
#### 컨테이너
* 다른 컴포넌트를 포함 할 수 있는 GUI 컴포넌트 : java.awt.Container를 상속받음
* AWT 컨테이너 :  Panel, Frame, Applet, Dialog, JWindow
* Swing 컨테이너 : JPanel JFrame, JApplet, JDialog, JWindow 

#### 컴포넌트 
* 컨테이너에 포함되어야 화면에 출력될 수 있는 GUI 객체
* 다른 컴포넌트를 포함할 수 없는 순수 컴포넌트
* 모든 GUI 컴포넌트가 상속받는 클래스 : java.awt.Component
* 스윙 컴포넌트가 상속받는 클래스 : javax.swing.Jcomponent

#### 최상위 컨테이너 
* 다른 컨테이너에 포함되지 않고도 화면에 출력되며, 독립적으로 존재 가능한 컨테이너
* 스스로 화면에 자신을 출력하는 컨테이너 : JFrame, JApplet, JDialog

### Swing GUI 프로그램 만들기 
#### 스윙 GUI 프로스램 만드는 과정
1. 스윙 프레임 만들기
2. main() 메소드 작성
3. 스윙 프레임에 스윙 컴포넌트 붙이기 

### Swing 프레임 
#### 스윙 프레임: 모든 스윙 컴포넌트를 담는 최상위 컨테이너
* JFrame을 상속받아 구현
* 컴포넌트들은 화면에 보이려면 스윙 프레임에 부착되어야 함
* 프레임을 닫으면 프레임에 부착된 모든 컴포넌트가 보이지 않게 됨

#### 스윙 프레임(JFrame) 기본 구성
* 프레임: 스윙 프로그램의 기본 틀
* 메뉴바: 메뉴들이 부착되는 공간
* 컨텐트팬: GUI 컴포넌트들이 부착되는 공간

### 프레임 만들기, JFrame 클래스 상속
#### 스윙 프레임
* JFrame 클래스를 상속받은 클래스 작성
* 프레임의 크기 반드시 지정 : setSize() 호출
* 프레임을 화면에 출력하는 코드 반드시 필요 : setVisible(true) 호출

#### 300x300 크기의 스윙 프레임 만들기 
~~~~ java
import javax.swing.JFrame;

public class Ex81MyFrame extends JFrame {
    public Ex81MyFrame() {
        setTitle("300x300 스윙 프레임 만들기"); // 타이틀 설정
        setSize(300, 300); // 프레임 크기 300x300
        setVisible(true); // 프레임 출력
    }

    public static void main(String[] args) {
        Ex81MyFrame frame = new Ex81MyFrame();
    }
}
~~~~

### Swing 응용프로그램에서 main()의 기능과 위치
#### 스윙 응용프로그램에서 main()의 기능 최소화 바람직
* 스윙 응용프로그램이 실행되는 시작점으로서의 기능만
* 스윙 프레임을 생성하는 정도의 코드로 최소화
~~~~java
public static void main(String [] args) {
    MyFrame frame = new MyFrame(); // 스윙 프레임 생성
}
~~~~
* frame 객체를 생성하고 사용하지 않기 때문에 worrying이 발생합니다.
* 실무에서는 다음과 같이 코딩하는 것이 일반적입니다.

#### 프레임에 컴포넌트 붙이기
#### 타이틀 달기
* super()나 setTitle() 이용
~~~~java
MyFrame() { // 생성자
super("타이틀문자열");
}

MyFrame() { // 생성자
setTitle("타이틀문자열");
}
~~~~
#### 컨텐트팬에 컴포넌트 달기
* 컨텐트팬이란? 스윙 컴포넌트들이 부착되는 공간
* 컨텐트팬 알아내기 - 스윙 프레임에 붙은 디폴트 
* 컨텐트팬 알아내기
~~~~java
public class MyFrame extends JFrame {
MyFrame() {
// 프레임의 컨텐트팬을 알아낸다.
Container contentPane = getContentPane();
}
}
~~~~
* 컨텐트팬에 컴포넌트 붙이기
~~~~java
// 버튼 컴포넌트 생성
JButton button = new JButton("Click");
contentPane.add(button); // 컨텐트팬에 버튼 부착
~~~~
* 컨텐트팬 변경
~~~~java
class MyPanel extends JPanel {
// JPanel을 상속받은 패널을 구현한다.
}
// frame의 컨텐트팬을 MyPanel 객체로 변경
frame.setContentPane(new MyPanel());
~~~~

#### Tip. 컨텐트팬에 대한 JDK 1.5 이후의 추가 사항
#### JDK 1.5 이전
* 프레임의 컨텐트팬을 알아내어, 반드시 컨텐트팬에 컴포넌트 부착
~~~~java 
Container c = frame.getContentPane();
c.add(new JButton("Click")); // 컨텐트팬에 직접 컴포넌트 부착
~~~~
#### JDK 1.5 이후 추가된 사항
* 프레임에 컴포넌트를 부착하면 프레임이 대신 컨텐트팬에 부착
~~~~java
frame.add(new JButton("Click"));
// 프레임의 버튼 컴포넌트를 컨텐트팬에 대신 부착
~~~~
#### 저자의 결론
* JDK1.5이전처럼 직접 컨텐트팬에 컴포넌트를 부착하는 것이 바람직함
* 컨텐트팬 다루기 능력 필요하기 때문
* 컴포넌트를 부착할 경우 프레임이 아닌, 컨텐트팬임을 알고 명확히 사용할 필요

#### 1.5 이후 추가된 기능을 사용하는 것이 가독성이 좋으며, Content Pane을 다루는 능력이 반드시 필요한 것은 아닙니다.

#### 3개의 버튼 컴포넌트를 가진 스윙 프레임 만들기 
~~~~java
import javax.swing.*;
import java.awt.*;

public class Ex8_2ContentPaneEx extends JFrame {
    public Ex8_2ContentPaneEx() {
        setTitle("ContentPane과 JFrame"); // 프레임의 타이틀 바 설정
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);

        Container contentPane = getContentPane(); // 컨텐트팬 알아내기
        contentPane.setBackground(Color.ORANGE); // 오렌지색 배경 설정
        contentPane.setLayout(new FlowLayout()); // FlowLayout 배치관리자 설정

        contentPane.add(new JButton("OK"));      // OK 버튼 부착
        contentPane.add(new JButton("Cancel"));  // Cancel 버튼 부착
        contentPane.add(new JButton("Ignore"));  // Ignore 버튼 부착

        setSize(300, 150); // 프레임 크기 300x150 설정
        setVisible(true);  // 프레임을 화면에 출력
    }

    public static void main(String[] args) {
        new Ex8_2ContentPaneEx();
    }
}
~~~~

### Swing 응용프로그램의 종료
* 응용프로그램 내에서 스스로 종료하는 방법
* 언제 어디서나 무조건 종료
~~~~java
System.exit(0);
~~~~
#### 프레임의 오른쪽 상단의 종료버튼(X)이 클릭되면 어떤 일이 일어나는가?
* 프레임 종료, 프레임 윈도우를 닫음 : 프레임이 화면에서 보이지 않게 됨

#### 프레임이 보이지 않게 되지만 응용프로그램이 종료한 것 아님
* 키보드나 마우스 입력을 받지 못함
* 다시 setVisible(true)를 호출하면, 보이게 되고 이전 처럼 작동함

* 프레임 종료버튼이 클릭될 때, 프레임과 함께 프로그램을 종료 시키는 방법
~~~~java
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
~~~~

#### 컨테이너와 배치, 배치관리자 개념
* 컨테이너마다 하나의 배치관리자 존재
* 컨테이너에 부착되는 컴포넌트의 위치와 크기 결정
* 컨테이너의 크기가 변경되면, 컴포넌트의 위치와 크기 재결정


### 배치 관리자 대표 유형 4 가지
#### FlowLayout 배치관리자
* 컴포넌트가 삽입되는 순서대로 왼쪽에서 오른쪽으로 배치
* 배치할 공간이 없으면 아래로 내려와서 반복한다.

#### BorderLayout 배치관리자
* 컨테이너의 공간을 동(EAST), 서(WEST), 남(SOUTH), 북(NORTH), 중앙(CENTER)의 5개 영역으로 나눔
* 5개 영역 중 응용프로그램에서 지정한 영역에 컴포넌트 배치

#### GridLayout 배치관리자
* 컨테이너를 프로그램에서 설정한 동일한 크기의 2차원 격자로 나눔
* 컴포넌트는 삽입 순서대로 좌에서 우로, 다시 위에서 아래로 배치

#### CardLayout
* 컨테이너의 공간에 카드를 쌓아 놓은 듯이 컴포넌트를 포개어 배치


#### 컨테이너와 디폴트 배치관리자
* 컨테이너의 디폴트 배치관리자 : 컨테이너 생성시 자동으로 생성되는 배치관리자


### 컨테이너에 새로운 배치관리자 설정
#### 컨테이너에 새로운 배치관리자 설정
* setLayout(LayoutManager lm) 메소드 호출 : lm을 새로운 배치관리자로 설정

#### [사례]
* JPanel 컨테이너에 BorderLayout 배치관리자를 설정하는 예

~~~~java
JPanel p = new JPanel();
p.setLayout(new BorderLayout()); // JPanel에 BorderLayout 설정
~~~~
#### 컨텐트팬의 배치관리자를 FlowLayout 배치관리자로 설정
~~~~java
Container c = frame.getContentPane(); // 프레임의 컨텐트팬 알아내기
c.setLayout(new FlowLayout()); // 컨텐트팬에 FlowLayout 설정
~~~~
#### 오류
~~~~java
c.setLayout(FlowLayout); // 오류
~~~~

### FlowLayout 배치관리자
#### 배치방법 
* 컴포넌트를 컨테이너 내에 왼쪽에서 오른쪽으로 배치
* 다시 위에서 아래로 순서대로 배치
~~~~java
container.setLayout(new FlowLayout());
container.add(new JButton("add"));
container.add(new JButton("sub"));
container.add(new JButton("mul"));
container.add(new JButton("div"));
container.add(new JButton("Calculate"));
~~~~
### FlowLayout의 생성자
#### 생성자 :
* FlowLayout()
* FlowLayout(int align, int hGap, int vGap)

* align : 컴포넌트를 정렬하는 방법 지정. 왼쪽 정렬(FlowLayout.LEFT), 오른쪽 정렬(FlowLayout.RIGHT), 중앙 정렬(FlowLayout.CENTER(디폴트))

* hGap : 좌우 두 컴포넌트 사이의 수평 간격, 픽셀 단위. 디폴트는 5

* vGap : 상하 두 컴포넌트 사이의 수직 간격, 픽셀 단위. 디폴트는 5

~~~~java
import javax.swing.*;
import java.awt.*;

public class Ex83FlowLayoutEx extends JFrame {
    public Ex83FlowLayoutEx() {
        setTitle("FlowLayout 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container contentPane = getContentPane(); // 컨텐트팬 알아내기

        // 왼쪽 정렬, 수평 간격을 30, 수직 간격을 40 픽셀로 배치하는 FlowLayout 생성
        contentPane.setLayout(new FlowLayout(FlowLayout.LEFT, 30, 40));

        contentPane.add(new JButton("add"));
        contentPane.add(new JButton("sub"));
        contentPane.add(new JButton("mul"));
        contentPane.add(new JButton("div"));
        contentPane.add(new JButton("Calculate"));

        setSize(300, 200); // 프레임 크기 300x200 설정
        setVisible(true);  // 화면에 프레임 출력
    }

    public static void main(String[] args) {
        new Ex83FlowLayoutEx();
    }
}
~~~~

### BorderLayout 배치관리자
### 배치방법
* 컨테이너 공간을 5 구역으로 분할, 배치 : 동, 서, 남, 북, 중앙

#### 배치 방법
* add(Component comp, int index) : comp를 index의 공간에 배치
~~~~java
container.setLayout(new BorderLayout());
container.add(new JButton("div"), BorderLayout.WEST);
container.add(new JButton("Calculate"), BorderLayout.CENTER);
~~~~

#### BorderLayout 생성자와 add() 메소드
### 생성자
* BorderLayout()
* BorderLayout(int hGap, int vGap)

* hGap : 좌우 두 컴포넌트 사이의 수평 간격, 픽셀 단위(디폴트 : 0)

* vGap : 상하 두 컴포넌트 사이의 수직 간격, 픽셀 단위(디폴트 : 0)

#### add() 메소드
* void add(Component comp, int index)
* comp 컴포넌트를 index 위치에 삽입한다.
* index : 컴포넌트의 위치

* 동 : BorderLayout.EAST

* 서 : BorderLayout.WEST

* 남 : BorderLayout.SOUTH

* 북 : BorderLayout.NORTH

* 중앙 : BorderLayout.CENTER


#### GridLayout 배치관리자
### 배치방법
* 컨테이너 공간을 동일한 사각형 격자(그리드)로 분할하고 각 셀에 컴포넌트 하나씩 배치
* 생성자에 행수와 열수 지정
* 셀의 왼쪽에서 오른쪽으로, 다시 위에서 아래로 순서대로 배치

~~~~java
container.setLayout(new GridLayout(4,3,5,5)); // 4×3 분할로 컴포넌트 배치
container.add(new JButton("1"));   // 상단 왼쪽 첫 번째 셀에 버튼 배치
container.add(new JButton("2"));   // 그 옆 셀에 버튼 배치
~~~~ 

#### GridLayout 생성자
### 생성자
* GridLayout()
* GridLayout(int rows, int cols)
* GridLayout(int rows, int cols, int hGap, int vGap)

#### rows : 격자의 행수 (디폴트 : 1)

#### cols : 격자의 열수 (디폴트 : 1)

#### hGap : 좌우 두 컴포넌트 사이의 수평 간격, 픽셀 단위(디폴트 : 0)

#### vGap : 상하 두 컴포넌트 사이의 수직 간격, 픽셀 단위(디폴트 : 0)

#### rows x cols 만큼의 셀을 가진 격자로 컨테이너 공간을 분할, 배치

#### 배치관리자 없는 컨테이너
### 배치관리자가 없는 컨테이너가 필요한 경우
* 응용프로그램에서 직접 컴포넌트의 크기와 위치를 결정하고자 하는 경우
1. 컴포넌트의 크기나 위치를 개발자 임의로 결정하고자 하는 경우
2. 게임 프로그램과 같이 시간이나 마우스/키보드의 입력에 따라 컴포넌트들의 위치와 크기가 수시로 변하는 경우
3. 여러 컴포넌트들이 서로 겹쳐 출력하고자 하는 경우

#### 컨테이너의 배치 관리자 제거 방법
* container.setLayout(null);
~~~~java
JPanel p = new JPanel();
p.setLayout(null); // JPanel의 배치관리자 삭제
~~~~
* 컨테이너의 배치관리자가 없어진면, 컴포넌트에 대한 어떤 배치도 없음

* 추가된 컴포넌트의 크기가 0으로 설정, 위치는 예측할 수 없게 됨

~~~~java
// 패널 p에는 배치 관리자가 없는 패널에 컴포넌트를 여러 개 두면 버튼은 배치되지 않는다.
p.add(new JButton("me")); 
p.add(new JButton("me")); 
~~~~

### 컴포넌트의 절대 위치와 크기 설정
#### 배치관리자가 없는 컨테이너에 컴포넌트를 삽입할 때
* 프로그램에서 컴포넌트의 절대 크기와 위치 설정
* 컴포넌트들이 서로 겹치게 할 수 있음

#### 컴포넌트의 크기와 위치 설정 메소드
* void setSize(int width, int height) // 컴포넌트 크기 설정
* void setLocation(int x, int y) // 컴포넌트 위치 설정
* void setBounds(int x, int y, int width, int height) // 위치와 크기 동시 설정

#### 예 버튼을 100×40 크기로 하고, JPanel의 (50, 50) 위치에 배치
~~~~ java
JPanel p = new JPanel();
p.setLayout(null); // 패널의 배치관리자 제거

JButton clickButton = new JButton("Click");
clickButton.setSize(100, 40); // 버튼 크기를 100×40으로 지정
clickButton.setLocation(50, 50); // 버튼 위치를 (50, 50)으로 지정
p.add(clickButton); // 패널 내 (50, 50)에 100×40 크기의 버튼 출력
~~~~

#### 예제 8-6 : 배치관리자 없는 컨테이너에 컴포넌트를 절대 위치와 절대 크기로 지정
~~~~java
import javax.swing.*;
import java.awt.*;

public class Ex86NullContainerEx extends JFrame {
    public Ex86NullContainerEx() {
        setTitle("배치관리자 없이 절대 위치에 배치하는 예제");
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        Container contentPane = getContentPane();
        contentPane.setLayout(null); // 컨텐트팬에 배치관리자 제거

        JLabel la = new JLabel("Hello, Press Buttons!");
        la.setLocation(130, 50); // la를 (130, 50)에 위치시킴
        la.setSize(200, 20); // 크기를 200x20으로 지정
        contentPane.add(la);

        for(int i = 1; i <= 9; i++) {
            JButton b = new JButton(Integer.toString(i)); // 버튼 생성
            b.setLocation(i*15, i*15); // 버튼 위치 지정
            b.setSize(50, 20); // 버튼 크기 50x20
            contentPane.add(b);
        }

        setSize(300, 200);
        setVisible(true);
    }

    public static void main(String[] args) {
        new Ex86NullContainerEx();
    }
}
~~~~

## 09장 자바의 이벤트 처리 

### 이벤트 기반 프로그래밍
#### 이벤트 기반 프로그래밍(Event Driven Programming)
* 이벤트의 발생에 의해 프로그램 흐름이 결정되는 방식
* 이벤트가 발생하면 이벤트를 처리하는 루틴(이벤트 리스너) 실행
* 실행될 코드는 이벤트의 발생에 의해 전적으로 결정

#### 반대되는 개념 : 배치 실행(batch programming)
* 프로그램 개발자가 프로그램의 흐름을 결정하는 방식

#### 이벤트 종류
* 사용자의 입력 : 마우스 드래그, 마우스 클릭, 키보드 누름 등
* 센서로부터의 입력, 네트워크로부터 데이터 송수신
* 다른 응용프로그램이나 다른 스레드로부터의 메시지

#### 이벤트 기반 응용 프로그램의 구조
* 각 이벤트마다 처리하는 리스너 코드 보유

#### GUI 응용프로그램은 이벤트 기반 프로그래밍으로 작성됨
* GUI 라이브러리 종류 : C++의 MFC, C# GUI, Visual Basic, X Window, Android 등
* 자바의 AWT와 Swing

#### 자바 스윙 프로그램에서 이벤트 처리 과정
1. 이벤트 발생
* 예 : 마우스의 움직임 혹은 키보드입력
2. 이벤트 객체 생성
* 현재 발생한 이벤트에 대한 정보를 가진 객체
3. 응용프로그램에 작성된 이벤트 리스너 찾기
4. 이벤트 리스너 실행
* 리스너에 이벤트 객체 전달
* 리스너 코드 실행

### 이벤트 객체
#### 이벤트 객체
* 발생한 이벤트에 관한 정보를 가진 객체
* 이벤트 리스너에 전달됨 : 이벤트 리스너 코드가
발생한 이벤트에 대한 상황을 파악할 수 있게 함

#### 이벤트 객체가 포함하는 정보
* 이벤트 종류와 이벤트 소스
* 이벤트가 발생한 화면 좌표 및 컴포넌트 내 좌표
* 이벤트가 발생한 버튼이나 메뉴 아이템의 문자열
* 클릭된 마우스 버튼 번호 및 마우스의 클릭 횟수
* 키의 코드 값과 문자 값
* 체크박스, 라디오버튼 등과 같은 컴포넌트에
이벤트가 발생하였다면 체크 상태

#### 이벤트 소스를 알아 내는 메소드 : Object getSource()
* 발생한 이벤트의 소스 컴포넌트 리턴
* Object 타입으로 리턴하므로 캐스팅하여 사용
* 모든 이벤트 객체에 대해 적용

### 리스너 인터페이스
* 이벤트 리스너 : 이벤트를 처리하는 자바 프로그램 코드, 클래스로 작성
* 자바는 다양한 리스너 인터페이스 제공

#### 예 ActionListener 인터페이스 – 버튼 클릭 이벤트를 처리하기 위한 인터페이스
~~~~java
interface ActionListener { // 아래 메소드를 개발자가 구현해야 함
    public void actionPerformed(ActionEvent o); // Action 이벤트 발생시 호출됨
}
~~~~
#### 예 MouseListener 인터페이스 – 마우스 조작에 따른 이벤트를 처리하기 위한 인터페이스
~~~~java
interface MouseListener { // 아래의 5개 메소드를 개발자가 구현해야 함
    public void mousePressed(MouseEvent e); // 마우스 버튼이 눌러지는 순간 호출
    public void mouseReleased(MouseEvent e); // 눌러졌던 마우스 버튼이 떼어지는 순간 호출
    public void mouseClicked(MouseEvent e); // 마우스 버튼이 눌렸다가 떼어지는 순간 호출
    public void mouseEntered(MouseEvent e); // 마우스가 컴포넌트 위에 올라가는 순간 호출
    public void mouseExited(MouseEvent e); // 마우스가 컴포넌트 위에서 나가는 순간 호출
}
~~~~
#### 사용자의 이벤트 리스너 작성
* 자바의 리스너 인터페이스(interface)를 상속받아 구현
* 리스너 인터페이스의 모든 추상 메소드 구현


### 이벤트 리스너 작성 과정 사례
1. 이벤트와 이벤트 리스너 선택
* 버튼 클릭을 처리하고자 하는 경우
* ㆍ이벤트 : Action 이벤트, 이벤트 리스너 : ActionListener
2. 이벤트 리스너 클래스 작성 : ActionListener 인터페이스 구현
~~~~java
class MyActionListener implements ActionListener {
    public void actionPerformed(ActionEvent e) { // 버튼이 클릭될 때 호출되는 메소드
        JButton b = (JButton)e.getSource();     // 사용자가 클릭한 버튼 알아내기
        if(b.getText().equals("Action"))        // 버튼의 문자열이 "Action"인지 비교
            b.setText("액션");                  // JButton의 setText() 호출, 문자열 변경
        else
            b.setText("Action");                // JButton의 setText() 호출, 문자열 변경
    }
}
~~~~
3. 이벤트 리스너 등록
* 이벤트를 받아 처리하고자 하는 컴포넌트에 이벤트 리스너 등록
* component.addXXXListener(listener)
* ㆍxxx : 이벤트 명, listener : 이벤트 리스너 객체
~~~~java
MyActionListener listener = new MyActionListener(); // 리스너 인스턴스 생성
btn.addActionListener(listener);                    // 리스너 등록
~~~~

### 이벤트 리스너 작성 방법
#### [ 3 가지 방법 ]

#### 독립 클래스로 작성
* 이벤트 리스너를 완전한 클래스로 작성
* 이벤트 리스너를 여러 곳에서 사용할 때 적합

#### 내부 클래스(inner class)로 작성
* 클래스 안에 멤버처럼 클래스 작성
* 이벤트 리스너를 특정 클래스에서만 사용할 때 적합

#### 익명 클래스(anonymous class)로 작성
* 클래스의 이름 없이 간단히 리스너 작성
* 클래스 조차 만들 필요 없이 리스너 코드가 간단한 경우에 적합



## 05월 22일 (11주차) 
#### README 파일 편집

### StringBuffer 클래스가
#### 기변 스트링을 다루는 클래스가 
* StringBuffer 객체 생성
~~~~java
StringBuffer sb = new StringBuffer("java");
~~~~

* String 쿨래스와 달리 문자열 변경 가능
* 가변 크기의 버퍼를 가고 있어 문자열 수정이 가능
* 문자열의 수정이 많은 작업에 적합 

### 스트링 조작 사례
~~~~~java
StringBuffer sb = new StringBuffer("java");

sb.append("is pencil");
sb.insert(7, "my");
sb.replace(8, 10, "your");
~~~~~

### StringTokenizer 클래스
* 구분 문자를 기준으로 문자열을 분리하는 클래스
* 구분 문자 : 문자열을 구분할 떄 사용되는 문자
* 토큰 : 구분 문자로 분리된 문자열


### Math 클래스
* 기분 산술 연산 메소드를 제공하는 클래스 
* 보든 메소드는 staric으로 선언 
* 클래스 이름으로 호출 가능

* Math.random 메소드로 난수 발생
* random() 0보다 크거나 같고 1.0보다 작은 실수 난수 발생 

### Math 클래스 활용
~~~~java
public class Ex68MathEx {
    public static void main(String[] args) {
        System.out.println(Math.abs(3.12));
        System.out.println(Math.sqrt(9.0));
        System.out.println(Math.exp(2));
        System.out.println(Math.round(3.14));

        System.out.println("이번주 행운 번호는 ");
        for (int i = 0; i < 5 ; i++)
            System.out.print((int)(Math.random()*45 + 1)+ " ");
        
    }
}
~~~~

### 컬렉션의 개념 
* 요소라고 불리는 가변 개수의 객체들의 저장소
* 객체들의 컨테이너라고도 불림
* 요소의 개수에 따라 크기 자동 조절
* 요소의 삽입, 삭제에 따른 요소의 위치 자동 이동
* 고정 크기의 배열을 다루는 어려움 해소 
* 다양한 객체들의 삽입, 삭제, 검색 등의 관리 용이 

### 컬렉션의 특징 
* 컬렉션은 제네릭 기법으로 구현 
#### 제네릭 
* 특정 타입만 다루지 않고, 여러 종류의 타입으로 변신할 수 있도록 클래스나 메소드를 일반화 시키는 기법
* 클래스나 인터페이스 이룸에 <E>, <k>, <v>등 타입 매개변수 포함

#### 제네릭 커렉션 사례 : 벡터 Vector<E>
* <E>에서 E에 구체적인 타입을 주어 구체적인 타입만 다루는 벡터로 활용 
* 점수만 다루는 컬렉션 벡터 Vecotr<Integer>
* 문자만 다루는 컬렉션 벡터 Vecotr<String>
### 컬렉션의 요소는 객체만 가능 
* int, char, doble 등의 기본 타입으로 구체화 불가

### 제네익은 형판과 같은 개년
* 제네릭은 클래스나 메소드를 현판에서 찍어내듯이 생산랑 수 있도록 일반화된 형판을 만드는 기법 

### 제네릭의 기본 개념
#### 제네릭 
* JDK 1.5부터 도입 
* 모든 종루의 데이터 타입을 다룰 수 있도록 일반화된 매개 변수로 클래스나 메소드를 작성하는 기법 
* C++의 탬플릿과 동일 

### Vector<E>의 특징 
* <E>에 사용할 요소의 특징 타입으로 구세화
* 배열을 기변크기로 다를 수 있게 하는 컨테이너 
* 벼열의 같이 제한 극복
* 요소의 개수가 넘치면 자동으로 길이 조절

* 요소 객체들의 삽입, 삭제, 검색하는 컨테이너
* -삽입, 삭제에 따라 자동으로 요소의 위치 조정

#### Vector에 삽입 가능한 것 
* 객체, null
* 기본 타입 값은 Wrapper 객체로 만들어 저장 

#### Vector에 삽입
* 벡터의 맨 뒤, 중간에 객체 삽입 가능

#### Vector에서 객체 삭제
* 임의의 위치에 있는 객체 삭제 가능 

### ArrayList<E>
* 기변 크기 배열을 수현한 클래스
* <E>에 요소로 사용할 득점 타입으로 구체화

* 백터와 거의 동일
* 요소 삽입, 삭제, 검색 등 백터 기능과 거의 동일
* 백터와 달리 스레드 동기화 기능 없음
* 다수 스레드가 동시에 ArrayList에 접근할 때 동기화되지 않음 
* 개발자가 스레드 동기화 코드 작성

### ArrayList와 Vector의 차이
* ArrayList와 Vector는 모두 동적으로 크기가 늘어나는 배열 기반의 리스트 클래스입니다.
* 요즘은 ArrayList가 기본 선택지입니다.
* Vector는 이제 거의 사용하지 않고, 멀티스레드가 필요하면 다른 방법을 씁니다

#### 컬렉션의 순차 검색을 위한 Itertor 
* Itertor<E> 인터페이스
* 리스트 구조의 컬렉션에서 요소의 순차 검색을 위한 인터페이스
* Vextor<E>, ArrayList<E> LinkedList<E> 상속 받는 인터페이스

#### Itertor 객체 얻어내기
* 컬렉션의 itertor() 메소드 호출 : 해당 컬렉션을 순차 검색할 수 있는 Itertor 객체 리턴 

### HashMap<K,V>
* 키와 값의 쌍으로 구성되는 요소를 다루는 컬렉션
* K : 키로 사용할 요소의 타입
* V : 값으로 사용할 요소의 타입
* 키와 값이 한 쌍으로 삽입 
* 값을 검색하기 위해서는 반드시 '키' 이용

#### 삽입 및 검색어 빠른 특징
* 요소 삽입 : put() 메소드
* 요소 검색 : get() 메소드

### 자바의 GUI
* GUI : 사용자가 편리하게 입출력 할 수 있도록 그래픽으로 화면을 구성하고, 마우스나 키보드로 입력 받을 수 있도록 지원하는 사용자 인터페이스 
* 자바 언어에서 GUI 응용프로그램 작성 : AWT와 Swing 패키지에 강력한 GUI 컴포넌트 제공 

### AWT 패키지
* 자바가 처음 나왔을 때 부터 배포된 GUI 패키지
* AWT 컴포넘트는 중량 컴포넌트
* AWT 컴포넌트의 그리기는 운영펮제에 의해 이루어지며, 운영체제의 자원을 많이 소모하고 부담을 줌
* 운영체제가 직접 그리기 때문에 속도는 빠름

### Swing 패키지
* AWT 기술을 기반으로 작성된 자바 라이브러리
* 모든 AWT 기능 + 추가된 풍부하고 화려한 고급 컴포넌트
* AWT 컴포넌트를 모두 스윙으로 재작성
* AWT 컴포넌트 이름 앞에 J자를 덧붙림
* 순수 자바 언어로 구현
* 스윙 컴포넌트는 경량 컴포넌트
* 스윙 컴포넌트는 운영체제의 도움을 받지 않고, 직접 그리기 떄문에 운영체제에 부담주지 않음
* 현재 자바의 GUI 표준으로 사용됨




## 05월 015일 (10주차) -> 여기서부터 기말
#### README 파일 편집

### 모듈 개념
* JVA 9에서 도입된 개념
* 패키지와 이미지등의 리소스를 담은 컨테이너
* 모듈 파일(.jmod)로 저장 

### 자바 플랫폼의 모듈화
#### 자바 플랫폼 자바의 개발 환경(JDK)과 자바의 실행 환경(JRE)을 지칭. JAVA SE(자바 API)포함.
* 자바 API의 모든 클래스가 여러 개의 모듈로 재구성됨
* 모듈 파일은 JDK의 jmods 디렉터링 저장하여 배포

### 자바 모듈화의 목적 
* 자바 컴포넌트들을 필요에 따라 조립하여 사용하기 위함
* 컴퓨터 시스템의 불필여한 부담 감소
* 세밀한 모듈화를 통해 필요 업는 모듈이 로드되지 않게 함 
* 소형 IoT 장치에도 자바 응용프로그램이 실행되고 성능을 유지하게 함

### JDK의 주요 패키지
* java.lang 
* 스트링, 수학 함수, 입출력 등 자바 프로그래밍에 필요한 기본적인 클래스와 인터페이스
* 자동으로 import 문 필요 없음
 
* java.util
* 날짜, 시간, 백터, 해시맵 등과 같은 다양한 유틸리티 클래스와 인터페이스 제공

* java.Io
* 키보드, 모니터, 프린트, 디스크 등에 입출력을 할 수 있는 클래스와 인터페이스 제공

* java.awt 
* GUI 프로그램을 작성하기 위한 AWT 패키지

* javas.swing 
* GUI 프로그래밍 작성하기 위한 스윙 패키지

### Object 클래스
* 모든 자바 클래스는 반드시 Object를 상속받도록 자동 컴파일
* 모든 클래스의 수퍼 클래스
* 모든 클래스가 상속받는 공통 메소드 포함 

### 객체 속성 
* Object 클래스는 객체의 속성을 나타내는 메소드 제공

* hashCode() 메소드 
* 객체의 해시코드 값을 리턴하며, 객체마다 다름

#### getClass() 메소드
* 객체의 클래스 정보를 담은 Class 객체 리턴
* Class 객체의 getName() 메소드는 객체의 클래스 이름 리턴

#### toString() 메소드
* 객체를 문자열로 리턴


### Object 클래스로 객체 속성 알아내기
~~~~java
class Point {
    private int x, y;
    public Point(int x, int y){
        this.x = x; this.y = y;
    }
}

public class Ex610bectPropertyEx {

    public static void main(String[] args) {
        Point p = new Point(2, 3);
        System.out.println(p.getClass().getName());
        System.out.println(p.hashCode());
        System.out.println(p.toString());
    }
}
~~~~

### otString() 메소드, 객체를 문자열로 변환
* 각 클래스는 toString()을 오버라이딩하여 자신만의 문자열 리턴 가능 
* 객체를 문자열로 반환
* 원형 : public toString();

### 컴파일에 의한 toString() 자동 변환
* 객체 + 문자열 -> 객체.toString + 문자열로자동 변환
* 객체를 단독으로 사용 하는 경우 -> 객체toString() 으로 자동 변환

~~~~java
class Point2 {
    private int x,y;
    public Point2 (int x , int y ){
        this.x = x; this.y = y;
    }
      
    public String toString(){
        return "Point("+ x + "," + y +")";
    }
}


public class Ex62ToStringEx {
    
    public static void main(String[] args) {
        Point2 a = new Point2(2,3);
        System.out.println(a.toString());  
        System.out.println(a);  
    }
}
~~~~

### 객체 비교(==)와 equals() 메소드
* == 연산자 : 객체 래퍼런스 비교

boolean equals(object obj)
* 두객체의 내용물 비교
* 객체의 내용물을 비교하기 위해 클래그의 멤버로 작성

~~~~java
class Point {
     int x, y;
    public Point3(int x, int y){
        this.x = x; this.y = y;
    }
}

public bloolean equls(Object ob){
    point3 p = (Point3ob)
    if (o =.x && y p.y)return
    else return false;
}
public class Ex63EqulsEx {

    public static void main(String[] args) {
        Point3 a = new Point3(2, 3);
        Point3 b = new Point3(2, 3);
        Point3 c = new Point3(3, 4);
        if( a == b) System.out.println("a == b")
        if(a.equls(b)) System.out.println("a is equls to b")
        if(a.equls(c)) System.out.println("a is equls to c")
    }
}
~~~~

### Wrapper 클래스
* Wrapper 클래스 : 자바의 기본 타입을 클래스화 한 8개 클래스 통칭
* 용도 : 객체만 사용할 수 있는 컬렉션 등에 기본 타입의 값을 사용하기 위해 Wrapper 객체로 만들어 사용 

### 박싱과 언박싱
* 박싱 : 기본 타입의 값을 Wrapper 객체 변환하는 것
* 언박싱 : Wrapper 객체에 들어 있는 기본 타입의 값을 뺴내는 것. 박싱의 반대.

* 자동 박싱과 자동 언박싱 : JDK 1.5부터 박싱과 언박싱은 자동으로 이루어지도록 컴파일됨 

### String의 생성과 특징
* String 클래스는 문자열을 나타냄
* 스트링 리터럴(문자열 리터럴)은 String 객체로 처리됨
* 스트링 객제의 생성 사례
~~~~java
String str1 = "abcd";

char data[] = {'a','b','c','d'};
String2 = new String(data);
String3 = new String("abcd");
~~~~

### 스트링 리터럴과 new Sting()
#### 스트링 리터럴 
* 자바 가상 기계 내부에서 리터럴 테이블에 저장되고 관리됨
* 응용프로그램에서 공유됨
* 스트링 리터럴 사례 : Strig s = "Hello";

#### new String()으로 생성된 스트링
* 스트링 객체는 힙에 생성
* 스트링은 공유되지 않음 

### 스트링 객체의 주요 특징
#### 스트링 객체는 수정 불가능 
* 리터럴 스트링이든 new String()을 생성했든 객체의 문자열 수정 불가능 

* 스트링 비교 : 두 스트링을 비교할 떄 반드시 equals()를 사용하여야 함 -> equals()는 내용을 비교하기 떄문 

### String 활용
#### 스트링 비교,equals와 compareTo()
* 스트링 비교에 == 연산자 절대 사용 금지
* equals() : 스트링이 같으면 true, 아니면 false 리턴
~~~~java
String java = "Java";
if(java.equals("Java"))
~~~~
#### int compareTo(String anotherString)
* 문자열이 같으면 0 리턴
* 이 문자열이 anotherString 보다 먼저 나오면 음수 리턴
* 이 문자열이 anotherString 보다 나중에 나오면 양수 리턴

### String 활용
* 공백 제거, String trim()
* 키보드나 파일로부터 스트링을 입력 시, 스트링 앞 뒤 공백이 끼는 경우가 많다 
* trim()을 이용하면 스트링 앞 뒤에 있는 공백 제거


## 05월 08일 (9주차) -> 여기서부터 기말
#### README 파일 편집

### 추상 메소드 
* abstract로 선언된 메소드, 메소드의 코드는 없고 원형만 선언

### 추상 클래스
* 추상 메소드를 가지며, abstract로 선언된 클래스
* 추상 메소드 없이, abstract로 선언된 클래스

### 추상 클래스의 인스턴스 생성 불가능
* 추상 클래스는 온전한 클래스가 아니기 떄문에 인스턴스를 생성 할 수 없음

### 추상 클래스의 상속과 구현 
* 추상 클래스 상속 
* - 추상 클래스를 상속 받으면 추상 클래스가 됨
* - 서브 클래스도 abstract로 선언해야 함

#### 추상 클래스 구현
* - 서브 클래스에서 슈퍼 클래스의 추상 메소드 구현(오버라이딩)
* - 추상 클래스를 구현한 서브 클래스는 추상 클래스 아님

### 추상 클래스의 목적
* 상속을 위한 슈퍼 클래스로 활용하는 것 
* 서브 클래스에서 추상 메소드 구현
* 다형성 실현 

### 추상 클래스의 구현 
~~~~java
abstract class Calulator {
    public abstract int add(int a, int b);

    public abstract int subtract(int a, int b);

    public abstract int average(int a, int b);
}
~~~~

#### 자바의 인터페이스 
* 소프트웨어를 규격화된 모듈로 만들고, 인터페이스가 맞는 모듈을 조립하긋이 응용프로그햄을 작성 하기위해서 사용

#### 자바의 인터페이스 
* 클래스가 구현해야 할 메소드들이 선언되는 추상형
* 인터페이스 선언 : interface 키워드 선언

#### 자바 인터페이스에 대한 변화 
* JAVA 7까지 : 인터페이스는 상수와 푸상 메소드로만 구성 

### 인터페이스의 구성 요소들의 특징
* 상수 : public만 허용, public static final 생략

* 추상 메소드 : public abstract 생략 가능 

* default 메소드: 
* 인터페이스에 코드가 작성된 메소드
* 인터페이스를 구현하는 클래스에 자동 상속
* public 접근 지정만 허용. 생략 가능 

* private 메소드 :
* 인터페이스 내에 메소드 코드가 작성되어야 함
* 인터페이스 내에 있는 다른 메소드에 의해서만 호출 가능

* static 메소드 : public,private 모두 지정 가능, 생략하면 public

### 자바 인터페이스 특징 
* 인터페이스의 객체 생성 불가
* 인터페이스 탑입의 레퍼런스 변수 선언 가능

### 인터페이스 상속 
* 인터페이스 간에 상속 가능 :  인터페이스를 상속하여 확장된 인터페이스 작성 
* 인터페이스 다중 상속 허용 (일반 상속에서는 허용하지 않음)

### 인터페이스 구현
* 인터페이스의 추상 메소드를 모두 구현한 클래스 작성
* implements 키워드 사용 
* 여러 개의 인터페이스 동시 구현 가능 

#### 인터페이스 구현 사례
* PhoneInterface 인터페이스를 구현한 SamsungPhone 클래스 
~~~~java 
class SamsungPhone implements PhoneInterface {
    public void sendCall() {System.out.println "띠리리리리링);}

    public void receiveCall() { System.out.println ("전화가 왔습니다");}
}
~~~~

### 패키지 개념과 필요성 
* 3명이 분담하여 자바 응용프로그램을 개발하는 경우, 동일한 이름의 클래스가 존재할 가능성 있음. -> 합칠 떄 오류 발생 가능성
* 개발자가 서로 다른 디렉터리로 코드 관리하여 해결 

### 자바의 패키지와 모듈이란? 
#### 패키지 
* 서로 관련된 클래스와 인터페이스를 컴파일한 클래스 파일들을 묶어 놓은 디렉터리
* 하나의 응용프로그램은 한 개 이상의 패키지로 작성 
* 패키지는 jar 파일로 압축할 수 있음

### 모듈
* 여러 패키지와 이미지 등의 자원을 모아 놓은 컨테이너
* 하나의 모듈을 하나의 .jmod 파일에 저장 

Java 9부터 모듈화 도입 
* 플랫폼의 모듈화 : Java9부터 자바 API의 모든 클래스를 (자바 실행 환경) 패키지 기반에서 모듈들로 완전히 재구성 
* 응용프로그램의 모듈화 : 클래스들은 패키지로 만들고, 다시 패키지를 모듈로 만듦. 모듈 프로그래밍은 어렵고 복잡

### 자바의 모듈화의 목적
#### 모듈화의 목적 
* Java 9부터 자바 API를 여러 모듈로 분할 : Java 8까지는 rt.jar의 한 파일에 모든 API 저장. # 현재 70개로 정리됨.
* 응용프로그램이 실헹할 때 꼭 필요란 모듈들로만 실행 환경 구축 : 메모리 자원이 열락한 작은 소형 기기에 꼭 필요한 모듈로 구성된 작은 크기의 실행 이미지를 만들기 위함

#### 모듈의 현실
* 모듈화 작업은 매우 중요한 개념이며, 소규모 프로젝트로 부터 적용해야 대형 프로젝트 쉽게 도입, 활용할 수 있다.

### 패키지 사용하기, import문 
#### 다른 패키지에 작성된 클레스 사용
* import를 이용하지 않는 경우 
* 소스에 클래스 이름의 완전 경로명 사용

#### 필요한 클래스만 import
* 소스 시작 부분에 클래스의 경로명 import
* import 패키지.클래스
* 소스에는 클래스 명만 명시하면 됨

#### 패키지 전체를 import 
* 소스 시작 부분에 패키지의 경로명. * import
* import 패키지.* 
* 소스에는 클래스 명만 명시하면 됨

### 패키지 만들기 
#### 클래스 파일이 저장되는 위치는?
* 클래스나 인터페이스가 컴파일 되면 클래스 파일 생성
* 클래스 파일은 패키지로 선언된 디렉터리에 저장 

#### 패키지 선언 
* 소스 파일에 맨 앞에 컴파일 후 저장될 패키지 지정 -> package 패키지명;

### 디폴트 패키지 
### package 선언문이 없는 자바 소스 파일의 경우
* 컴파일러는 클래스나 인터페이스를 디폴트 패키지에 소속시킴 
* 디폴트 패키지 -> 현재 디렉터리

### package의 운영 방법
* 패키지 이름은 도메인 기반으로 시작 형식 : com.회사이름.프로젝트명.기능명
* 기능/역할별로 하위 패키지 구분 : utils, controller, service 등
* 디렉터리 구조와 package 선언을 정확히 일치해야 합니다.
* import는 필요한 만큼만, * 전체 import는 피하는 것이 좋습니다.

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
