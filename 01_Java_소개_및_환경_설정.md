# 1. Java 소개 및 환경 설정

## 1.1. Java란 무엇인가? (Java의 특징 및 장점)

**Java**는 썬 마이크로시스템즈(현재 오라클)에서 개발한 **객체 지향 프로그래밍(Object-Oriented Programming, OOP) 언어**입니다. JavaScript와 이름은 비슷하지만, 문법적으로 C/C++에 기반을 두고 있어 구조적으로는 완전히 다른 언어입니다.

JavaScript가 주로 웹 브라우저(프론트엔드)나 Node.js(백엔드) 환경에서 동적으로 실행되는 **스크립트 언어**라면, Java는 운영체제(OS) 위에서 독립적으로 실행될 수 있는 강력하고 안정적인 **애플리케이션**을 만드는 데 사용됩니다.

JavaScript 개발자에게 Java의 주요 특징은 다음과 같이 요약할 수 있습니다.

### 주요 특징

1.  **객체 지향 프로그래밍 (OOP)**
    *   Java는 거의 모든 것이 '객체(Object)'로 이루어져 있습니다. 이는 코드를 재사용하고 유지보수하기 쉽게 만들어주는 프로그래밍 방식입니다.
    *   **JavaScript 비교**: JavaScript도 프로토타입 기반의 객체 지향 프로그래밍이 가능하지만, Java는 클래스(Class) 기반의 더 엄격하고 구조적인 객체 지향 모델을 따릅니다.

2.  **플랫폼 독립성 (Write Once, Run Anywhere)**
    *   Java는 **JVM(Java Virtual Machine)**이라는 가상 머신 위에서 동작합니다. 따라서 개발자는 운영체제에 상관없이 Java 코드 한 번만 작성하면, JVM이 설치된 어떤 환경(Windows, macOS, Linux 등)에서든 동일하게 실행할 수 있습니다.
    *   **JavaScript 비교**: JavaScript 코드는 브라우저의 JavaScript 엔진이나 Node.js 런타임 환경에 종속되어 실행됩니다.

3.  **정적 타입 (Statically-Typed) 언어**
    *   Java는 변수를 선언할 때 반드시 **타입(type)**을 명시해야 합니다. 예를 들어, `int number = 10;` 처럼 숫자 타입임을 알려줘야 합니다. 한번 정해진 타입은 바꿀 수 없습니다.
    *   **JavaScript 비교**: `let data = 10; data = "hello";` 처럼 변수의 타입이 동적으로 변할 수 있는 JavaScript와 가장 큰 차이점 중 하나입니다. Java의 정적 타입은 코드를 실행하기 전(컴파일 시)에 타입 관련 오류를 잡을 수 있어 코드의 안정성을 높여줍니다.

4.  **컴파일 언어 (Compiled Language)**
    *   Java 코드는 실행되기 전에 **컴파일(compile)** 과정을 거쳐 컴퓨터가 이해할 수 있는 **바이트코드(bytecode)** 파일(`.class`)로 변환됩니다. 이 과정에서 문법 오류 등을 미리 확인할 수 있습니다.
    *   **JavaScript 비교**: JavaScript는 별도의 컴파일 과정 없이 코드를 한 줄씩 읽어 바로 실행하는 **인터프리터(interpreter)** 언어입니다. (물론 내부적으로는 JIT 컴파일 등 복잡한 과정을 거칩니다.)

5.  **풍부한 표준 라이브러리 (API)**
    *   Java는 오랜 역사만큼이나 방대하고 검증된 표준 라이브러리를 제공합니다. 날짜 처리, 네트워크 통신, 데이터베이스 연결 등 거의 모든 기능이 공식적으로 지원되어 안정적인 개발이 가능합니다.

이러한 특징들 덕분에 Java는 대규모 엔터프라이즈 시스템, 안드로이드 앱 개발, 빅데이터 처리 등 높은 성능과 안정성이 요구되는 다양한 분야에서 널리 사용되고 있습니다.

---

## 1.2. Java와 JavaScript의 핵심 차이점

앞서 언급된 특징들을 바탕으로 두 언어의 핵심적인 차이점을 표로 정리하면 다음과 같습니다.

| 구분 | Java | JavaScript |
| :--- | :--- | :--- |
| **실행 환경** | JVM (Java Virtual Machine) | 브라우저 또는 Node.js |
| **타입 시스템** | **정적 타입 (Statically Typed)**<br>컴파일 시 타입 결정 | **동적 타입 (Dynamically Typed)**<br>런타임 시 타입 결정 |
| **언어 종류** | **컴파일 언어 (Compiled)**<br>소스 코드 -> 바이트코드 -> 실행 | **인터프리터 언어 (Interpreted)**<br>소스 코드를 바로 한 줄씩 실행 |
| **객체 지향** | **클래스 기반 (Class-based)** | **프로토타입 기반 (Prototype-based)** |
| **주요 용도** | 서버사이드, 안드로이드 앱, 데스크톱 앱 | 웹 프론트엔드, 서버사이드(Node.js) |

---

## 1.3. 개발 도구: JDK와 IntelliJ IDEA



Java로 개발하려면 **JDK(Java Development Kit)**가 필요합니다. JDK는 Java 코드를 컴퓨터가 이해하는 언어로 번역(컴파일)하고 실행시켜주는 도구들의 모음입니다.



과거에는 JDK를 직접 설치하고 복잡한 환경 설정을 해야 했지만, 최근에는 **IntelliJ IDEA**와 같은 똑똑한 통합 개발 환경(IDE)이 이 모든 과정을 대신 처리해줍니다.



이번 강의에서는 별도로 JDK를 설치하지 않고, IntelliJ IDEA를 설치하는 과정에서 필요한 JDK를 함께 설치하여 개발 환경을 쉽고 빠르게 구성하는 방법을 사용합니다.



---



## 1.4. IntelliJ IDEA 설치 및 프로젝트 생성



IDE(Integrated Development Environment)는 코딩, 디버깅, 실행 등 개발의 모든 과정을 하나의 프로그램에서 할 수 있게 도와주는 강력한 도구입니다. Java 개발에는 IDE 사용이 거의 필수적입니다.



**IntelliJ IDEA Community Edition**을 가장 추천합니다. 무료이면서 Java 개발에 필요한 모든 강력한 기능을 제공합니다.



1.  **IntelliJ 다운로드**: [JetBrains IntelliJ IDEA 다운로드 페이지](https://www.jetbrains.com/idea/download/)에서 **Community** 버전을 다운로드하여 설치합니다.



2.  **새 프로젝트 생성**:

    -   IntelliJ를 실행하고 `New Project`를 클릭합니다.

    -   프로젝트 이름(Name)을 입력하고, 언어(Language)는 `Java`, 빌드 시스템(Build system)은 `IntelliJ`를 선택합니다.

    -   **JDK 설정**: JDK 항목을 클릭했을 때, 설치된 JDK가 없다면 **`Download JDK`**를 선택하세요. 최신 LTS(Long-Term Support) 버전 (예: 21)을 선택하고 `Download` 버튼을 누르면 IntelliJ가 자동으로 JDK를 다운로드하고 설정해줍니다.

    -   `Create` 버튼을 눌러 프로젝트를 생성합니다.



---



## 1.5. 첫 Java 프로그램 작성 및 실행: "Hello, World!"



이제 IntelliJ를 사용하여 첫 Java 프로그램을 만들어 보겠습니다.



1.  **클래스 생성**:

    -   프로젝트 탐색기(왼쪽 패널)에서 `src` 폴더를 마우스 오른쪽 버튼으로 클릭합니다.

    -   `New` -> `Java Class`를 선택합니다.

    -   클래스 이름으로 `HelloWorld`를 입력하고 Enter 키를 누릅니다.



2.  **코드 작성**: 생성된 `HelloWorld.java` 파일에 다음 코드를 입력합니다.



    ```java

    public class HelloWorld {

        public static void main(String[] args) {

            // System.out.println()은 콘솔에 문자열을 출력하는 명령어입니다.

            // JavaScript의 console.log()와 비슷한 역할을 합니다.

            System.out.println("Hello, World!");

        }

    }

    ```



### 코드 분석



-   `public class HelloWorld`: `HelloWorld`라는 이름의 공개 클래스를 정의합니다. **Java에서는 파일 이름과 public 클래스 이름이 반드시 일치해야 합니다.**

-   `public static void main(String[] args)`: **main 메서드**라고 불리며, Java 프로그램의 **시작점(entry point)**입니다. JVM은 이 메서드를 가장 먼저 찾아 실행합니다.

    -   `public`: 어디서든 접근 가능하다는 의미입니다.

    -   `static`: 객체를 생성하지 않고도 클래스 이름을 통해 바로 실행할 수 있다는 의미입니다.

    -   `void`: 이 메서드는 아무것도 반환하지 않는다는 의미입니다.

    -   `String[] args`: 프로그램을 실행할 때 외부에서 전달하는 인자(arguments)를 받을 수 있는 문자열 배열입니다.

-   `System.out.println("Hello, World!");`: 콘솔에 "Hello, World!" 문자열을 출력하고 줄을 바꿉니다. JavaScript의 `console.log()`와 기능적으로 유사합니다.



### 실행 방법



-   **IntelliJ에서 실행**: 코드 편집기의 `main` 메서드 옆에 있는 **녹색 재생(▶) 버튼**을 클릭하고 `Run 'HelloWorld.main()'`을 선택하면 됩니다. 하단 콘솔 창에 "Hello, World!"가 출력되는 것을 확인할 수 있습니다. IntelliJ가 코드를 컴파일하고 실행하는 모든 과정을 자동으로 처리해줍니다.
