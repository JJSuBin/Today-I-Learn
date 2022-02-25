## 📘 JVM(Java Virtual Machine, 자바 가상 머신)

### 💡 JVM 등장 이유
 
    Linux에서 개발하고 Window에서 배포하려면 추가적인 작업이 필요한 것처럼 컴파일 플랫폼과 실행 플랫폼이 다른 경우 프로그램이 동작하지 
    않는 문제점이 있다. JAVA는 JVM을 사용해 이러한 문제를 해결한다.
    
    Javac(Java Comiler)가 컴파일하면 Java Bytecode(.class 파일)가 만들어지고, JVM이 설치된 플랫폼이라면 모두 Java Bytecode를 실행시킬 
    수 있다. 

### 💡 JVM 이란?

    Java Virtual Machine, 자바 가상 머신의 약자를 따서 줄여 부르는 용어, 스택 기반으로 동작하는 가상머신
    
    일반적인 프로그램은 OS 위에서 실행되지만 자바 프로그램은 OS 위의 JVM에서 실행된다. 즉, 자바 프로그램은 OS에 상관없이 실행시킬 수 있다는
    장점을 갖는다. 따라서 어떤 OS에서도 그에 맞는 JVM만 다운받는다면 자바 프로그램을 실행시킬 수 있게된다.
    
### 💡 JVM 역할

    1. 자바 애플리케이션을 클래스 로더로 읽어 들여 자바 API와 함께 실행
    2. Java와 OS 사이의 중개자 역할을 수행하여 Java가 OS에 구애받지 않고 재사용을 가능케 한다.
    3. JVM은 메모리 관리(C와는 달리 직접 메모리를 관리할 필요가 없음), Garbage Collection을 수행
</br>

### 💡 자바 프로그램 실행 과정
<p align="center"><img src="https://user-images.githubusercontent.com/45066381/155668918-773efe25-efd9-461f-b9db-d19fdfc31817.png" width="600" height="400"/></p>
    
    1. 프로그램이 실행되면 JVM은 OS로부터 프로그램이 필요로 하는 메모리를 할당 받음, JVM은 이 메모리를 용도에 따라 여러 영역으로 나눠 관리
    2. javac(자바 컴파일러)가 자바 소스코드(.java)를 읽어들여 자바 바이트코드(.class)로 변환
    3. Class Loader를 통해 class 파일들을 JVM으로 로딩
        -> 프로그램이 필요한 클래스들을 로딩하여 런타임 영역인 JVM 메모리로 로딩
        -> 인터프리터로 명령어를 하나씩 해석하고 수행
        -> JLT 방식은 캐시를 사용해 기존에 해석한 바이트 코드 전체를 기계어로 바꿔 수행하는 것, 인터프리터의 단점을 보완
    4. 로딩된 class 파일들은 Execution engine을 통해 해석됨
    5. 해석된 바이트 코드는 Runtime Data Areas에 배치되어 실질적인 수행이 이루어짐
       이때 JVM은 필요에 따라 Thread Synchronization, GC 와 같은 관리 작업을 수행한다.

### 💡 JVM 구성

    - Class Loader : JVM 내로 클래스(.class 파일)를 로드하고, 링크를 통해 배치하는 작업을 수행하는 모듈
      Runtime 시에 동적으로 클래스를 로드하며 jar 파일 내 저장된 클래스 들을 JVM 위에 탑재하고 사용하지 않는 클래스들은 메모리에서 삭제
    
    - Jaca Compiler : 자바 소스 코드(.java)를 바이트 코드(.class)로 변환하는 역할 수행
    
    - Execution Engine : Class Loader를 통해 JVM 내의 런타임 데이터 영역에 배치된 바이트 코드를 명령어 단위로 읽어 실행한다. 
      바이트 코드는 기계어가 아니기 때문에 바로 실행할 수 없어 Execution Engine이 바이트 코드를 JVM 내부에서 실행할 수 있는 형태로 변환
    
    - Interpreter : 바이트 코드 명령어를 하나씩 읽어 해석하고 실행 -> 속도가 느림
    
    - JLT(Just-In-Time) Compiler : 인터프리터의 단점을 보안하기 위해 도입
      인터프리터 방식으로 실행하다 적절한 시점에 바이트 코드 전체를 컴파일하여 네이티브 코드로 변환시킨다. 이후 해당 메서드를 더 이상 
      인터프리팅 하지 않고 캐시에 있는 네이티브 코드를 실행하므로서 빠르게 수행될 수 있다. 
   
    - Garbage Collector : GC를 수행하는 모듈(쓰레드)이 있음

### 💡 Runtime Data Area
<p align="center"><img src="https://user-images.githubusercontent.com/45066381/155683982-7712d91e-43ef-43f5-a1e4-10886f3b9a43.png" width="600" height="350"/></p>

    프로그램을 수행하기 위해 OS에서 할당받은 메모리 공간을 의미, Class Loader에서 준비한 데이터들을 보관하는 저장소
   
    - PC Register : 쓰레드가 시작될 때 생성되며, 쓰레드마다 하나씩 존재한다. 쓰레드가 어떤 부분을 어떤 명령어로 실행해야 할 지에 
      대한 정보 등 JVM 명령의 주소를 기록하는 부분
   
    - JVM 스택 영역 : 프로그램 실행 과정에서 임시로 할당 되었다가 메소드를 빠져나가면 바로 소멸되는 특성의 데이터를 저장하기 위한 영역
      메소드 호출 시마다 각각의 스택 프레임이 생성되고, 메서드 수행이 끝나면 프레임 별로 삭제한다. 기본 타입 변수는 스택 영역에 직접 
      값을 가지고, 참조 타입 변수는 힙 영역이나 메소드 영역의 객체 주소를 가진다.
   
    - Native Method Stack : 자바 프로그램이 컴파일 되어 생성되는 바이트 코드가 아닌 실제 실행할 수 있는 기계어로 작성된 프로그램
      (자바 외 언어)을 실행시키는 영역, Java Native Interface를 통해 바이트 코드로 전환하여 저장하게 됨
   
    - Method Area(=Class/Static Area) : 클래스 정보를 처음 메모리 공간에 올릴 때 초기화 되는 대상을 저장하기 위한 메모리 공간, 
      클래스와 멤버 변수, 클래스 변수(static), 메소드 이름, 리턴 타입 등의 정보가 올라가고, 상수 자료형을 저장하여 참조하고 중복을 
      막는 Runtime Constant Pool 관리 영역 존재
      Method Area는 클래스 데이터를 위한 공간이라면 Heap 영역은 객체를 위한 공간 -> 두 공간 모드 GC 관리 대상
    
    - Heap Area : 객체를 저장하는 가상 메모리 공간, new 연산자로 생성된 객체와 배열을 저장한다.  
       -> Permanent Generation : 생성된 객체들의 주소 값이 저장된 공간, Class Loader에 의해 로드되는 클래스, 메서드 등에 대한 메타 
          정보가 저장되는 영역으로 JVM에 의해 사용된다.
       -> New/Young Area : 객체들이 최초로 생성되는 공간 Eden, Eden에서 참조되는 개체들이 저장되는 공간인 Survivor 0/1로 구성
       -> Old Area : New Area에서 일정 시간 참조되고 있는(살아남은) 객체들이 저장되는 공간, Eden 영역에 객체가 가득차게 되면 첫 번째 
          GC가 발생, Eden 영역에 있는 값들을 Survivor 1 영역에 복사하고 이 영역을 제외한 나머지 영역의 객체를 삭제한다.
    
    OS 위에 존재하는 JVM 위에서 실행되기 때문에 운영체제에 독립적으로 실행이 가능하다. 
    하지만 JVM을 사용하기 때문에 많은 메모리를 사용하고 실행 속도가 느리다는 단점이 존재한다.
   
### 💡 자바 PermGen / Metaspace
