# 3. 객체 지향 프로그래밍 (OOP) - 핵심 개념

객체 지향 프로그래밍(OOP)은 Java의 근간을 이루는 가장 중요한 패러다임입니다. JavaScript 역시 프로토타입 기반의 객체 지향 언어이지만, Java는 **클래스(Class)** 기반의 보다 엄격하고 구조적인 OOP 모델을 따릅니다.

---

## 3.1. 클래스(Class)와 객체(Object)

-   **클래스 (Class)**: 객체를 만들어내기 위한 **설계도** 또는 **틀(template)**입니다. 클래스에는 객체가 가지게 될 속성(데이터)과 기능(동작)이 정의되어 있습니다.
-   **객체 (Object)**: 클래스라는 설계도를 바탕으로 메모리에 **실체화된 존재**입니다. 클래스의 **인스턴스(instance)**라고도 부릅니다.

붕어빵 틀이 '클래스'라면, 그 틀로 찍어낸 각각의 붕어빵이 '객체'라고 비유할 수 있습니다.

**JavaScript (ES6 Class 문법)**
ES6부터 `class` 키워드가 도입되어 Java와 유사해 보이지만, 내부적으로는 여전히 프로토타입 기반으로 동작하는 'syntactic sugar'입니다.
```javascript
class Car {
  constructor(name, speed) {
    this.name = name;
    this.speed = speed;
  }

  honk() {
    console.log(`${this.name}이(가) 경적을 울립니다.`);
  }
}

// 객체(인스턴스) 생성
const myCar = new Car('소나타', 60);
myCar.honk();
```

**Java (클래스 기반)**
Java의 클래스는 객체를 만들기 위한 완전한 설계도입니다.
```java
// Car.java 파일
public class Car {
    // 1. 속성 (필드)
    String name;
    int speed;

    // 2. 기능 (메서드)
    public void honk() {
        System.out.println(name + "이(가) 경적을 울립니다.");
    }
}

// Main.java 파일
public class Main {
    public static void main(String[] args) {
        // 객체(인스턴스) 생성
        Car myCar = new Car();

        // 객체의 속성 값 할당
        myCar.name = "소나타";
        myCar.speed = 60;

        // 객체의 메서드 호출
        myCar.honk();
    }
}
```

---

## 3.2. 필드(Fields)와 메서드(Methods)

-   **필드 (Fields)**: 클래스에 포함된 **변수**로, 객체의 **상태나 속성**을 나타냅니다. (예: `Car` 클래스의 `name`, `speed`)
-   **메서드 (Methods)**: 클래스에 포함된 **함수**로, 객체의 **동작이나 기능**을 나타냅니다. (예: `Car` 클래스의 `honk()`)

---

## 3.3. 생성자 (Constructors)

**생성자**는 `new` 키워드로 객체를 생성할 때 **가장 먼저 호출되는 특별한 메서드**입니다. 주로 객체의 필드를 초기화하는 역할을 합니다.

-   생성자의 이름은 **클래스 이름과 반드시 동일**해야 합니다.
-   생성자는 **반환 타입(return type)을 명시하지 않습니다.**

**Java 생성자 예시**
```java
// Car.java
public class Car {
    String name;
    int speed;

    // 생성자: 객체가 생성될 때 이름과 속도를 초기화
    public Car(String initialName, int initialSpeed) {
        System.out.println("Car 객체가 생성됩니다.");
        name = initialName;
        speed = initialSpeed;
    }

    public void honk() {
        System.out.println(name + "이(가) 경적을 울립니다.");
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        // new Car(...)를 호출하는 순간 생성자가 실행됨
        Car myCar = new Car("그랜저", 80);

        System.out.println("차 이름: " + myCar.name); // 차 이름: 그랜저
        System.out.println("현재 속도: " + myCar.speed); // 현재 속도: 80
        myCar.honk();
    }
}
```
JavaScript의 `constructor` 함수와 거의 동일한 역할을 수행합니다.

---

## 3.4. 상속 (Inheritance)

**상속**은 기존 클래스(부모 클래스)의 필드와 메서드를 새로운 클래스(자식 클래스)가 물려받아 사용할 수 있게 하는 기능입니다. 코드의 재사용성을 높이고 클래스 간의 관계를 구조화할 수 있습니다.

-   **부모 클래스 (Superclass)**: 속성과 기능을 물려주는 클래스
-   **자식 클래스 (Subclass)**: 속성과 기능을 물려받는 클래스
-   Java에서는 `extends` 키워드를 사용하며, **단일 상속만 지원**합니다. (하나의 부모만 가질 수 있음)

```java
// 부모 클래스
public class Vehicle {
    int speed;

    public void start() {
        System.out.println("차량이 출발합니다.");
    }
}

// 자식 클래스 (Vehicle을 상속)
public class Truck extends Vehicle {
    int capacity; // 트럭만의 고유한 속성

    public void load() {
        System.out.println("짐을 싣습니다.");
    }
}

// 실행
public class Main {
    public static void main(String[] args) {
        Truck myTruck = new Truck();
        myTruck.speed = 50;   // 부모(Vehicle)의 필드 사용
        myTruck.start();      // 부모(Vehicle)의 메서드 사용
        myTruck.capacity = 1000;
        myTruck.load();       // 자신(Truck)의 메서드 사용
    }
}
```

---

## 3.5. 다형성 (Polymorphism)

**다형성**은 '여러 가지 형태를 가질 수 있는 능력'을 의미하며, OOP의 핵심적인 특징 중 하나입니다. Java에서는 주로 **하나의 참조 변수로 여러 타입의 객체를 참조**하는 방식으로 나타납니다.

-   **부모 클래스 타입의 참조 변수로 자식 클래스의 객체를 가리킬 수 있습니다.**

```java
public class Main {
    public static void main(String[] args) {
        // 부모 타입 변수로 자식 객체를 참조
        Vehicle myVehicle = new Truck();

        myVehicle.speed = 60;
        myVehicle.start();

        // myVehicle.load(); // 컴파일 에러!
        // Vehicle 타입에는 load() 메서드가 정의되어 있지 않기 때문
    }
}
```
다형성은 코드를 더 유연하고 확장성 있게 만들어주며, 특히 메서드 오버라이딩(Overriding)과 결합될 때 강력한 힘을 발휘합니다.

---

## 3.6. 캡슐화 (Encapsulation)와 접근 제어자

**캡슐화**는 객체의 데이터(필드)와 기능(메서드)을 하나로 묶고, 외부의 직접적인 접근으로부터 데이터를 보호하는 개념입니다.

**접근 제어자(Access Modifiers)**를 사용하여 외부의 접근 수준을 제어합니다.

-   `public`: 어떤 클래스에서든 접근 가능 (완전 공개)
-   `protected`: 같은 패키지 또는 상속받은 자식 클래스에서 접근 가능
-   `default` (아무것도 안 씀): 같은 패키지 내에서만 접근 가능
-   `private`: **해당 클래스 내부에서만 접근 가능 (가장 높은 수준의 보호)**

일반적으로 필드는 `private`으로 선언하여 외부의 직접적인 수정을 막고, 해당 필드에 접근할 수 있는 `public` 메서드(Getter/Setter)를 제공하는 것이 좋은 설계입니다.

```java
public class Person {
    // 필드는 private으로 보호
    private String name;
    private int age;

    // name 필드에 접근할 수 있는 public 메서드 (Getter)
    public String getName() {
        return name;
    }

    // name 필드의 값을 설정할 수 있는 public 메서드 (Setter)
    public void setName(String newName) {
        this.name = newName;
    }

    // age 필드에 대한 Getter/Setter
    public int getAge() {
        return age;
    }

    public void setAge(int newAge) {
        if (newAge > 0) { // 유효성 검사 로직 추가 가능
            this.age = newAge;
        }
    }
}

// 실행
public class Main {
    public static void main(String[] args) {
        Person p = new Person();
        // p.name = "홍길동"; // 컴파일 에러! private 필드에 직접 접근 불가
        p.setName("홍길동"); // Setter를 통해 안전하게 값 설정
        p.setAge(30);

        System.out.println("이름: " + p.getName()); // Getter를 통해 값 조회
    }
}
```
이러한 방식을 통해 객체의 데이터 무결성을 보장하고, 내부 구현을 숨길 수 있습니다.
