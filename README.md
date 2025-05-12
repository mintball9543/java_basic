* **상속**을 통해 기존 클래스(슈퍼 클래스)의 필드와 메서드를 하위 클래스에서 물려받아 코드 중복을 줄일 수 있습니다.
* **다형성**은 하나의 메서드 호출이 실제 객체 타입에 따라 서로 다른 구현을 실행하도록 해 주며, **업캐스팅**과 **오버라이딩**이 주요 메커니즘입니다.
* **추상 클래스**는 일부 구현을 강제하거나 공통 인터페이스를 정의할 때 사용하며, 직접 인스턴스화할 수 없고 서브클래스에서 구체화를 제공합니다.

---

## 1. 상속 (Inheritance)

### 1.1 정의 및 목적

* **상속**이란 한 클래스가 다른 클래스의 속성과 동작을 물려받는 것을 말합니다.(부모클래스+자식클래스)
* 이를 통해 **코드 재사용**이 가능하고, 클래스 계층 구조를 설계하여 유지보수성을 높입니다.

### 1.2 문법과 예제

```java
// 슈퍼 클래스
class Vehicle {
    String model;
    void drive() {
        System.out.println("Vehicle is driving");
    }
}

// 서브 클래스
class Car extends Vehicle {
    int seatCount;
    @Override
    void drive() {
        System.out.println("Car is driving with " + seatCount + " seats");
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();
        car.model = "Sedan";
        car.seatCount = 5;
        car.drive();  // Car is driving with 5 seats
    }
}
```

### 1.3 메서드 오버라이딩(Method Overriding)

* 서브 클래스에서 슈퍼 클래스의 메서드를 **같은 시그니처**로 재정의할 수 있습니다.
* `@Override` 어노테이션을 권장하며, 런타임에 올바른 메서드가 호출되도록 합니다.

---

## 2. 다형성 (Polymorphism)

### 2.1 개념

* **다형성**은 같은 인터페이스(슈퍼 타입)로 여러 구체 타입의 객체를 다룰 수 있는 성질입니다.
* 대표적으로 **업캐스팅(upcasting)**, **다운캐스팅(downcasting)**, **메서드 오버라이딩**을 통해 구현됩니다.

### 2.2 업캐스팅 예제

```java
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal animal = new Dog();  // 업캐스팅
        animal.sound();             // Dog barks
    }
}
```
### 2.3 활용

* 컬렉션 프레임워크에서 서로 다른 객체를 하나의 타입으로 관리할 때 유용합니다.
* 예: `List<Shape>`에 `Circle`, `Rectangle` 객체를 담고 공통 메서드 `draw()`를 호출하면 실제 타입별 구현이 실행됩니다.

---

## 3. 추상 클래스 (Abstract Class)

### 3.1 정의

* 추상 클래스는 `abstract` 키워드로 선언하며, 인스턴스화 불가하지만 서브 클래스에서 확장할 수 있습니다.
* 추상 메서드를 포함할 수 있으며, 이러한 메서드를 하나라도 가지면 클래스는 반드시 `abstract`여야 합니다.

### 3.2 문법과 예제

```java
abstract class Shape {
    // 추상 메서드
    abstract double area();
    
    // 일반 메서드
    void info() {
        System.out.println("This is a shape.");
    }
}

class Circle extends Shape {
    double radius;
    Circle(double r) { radius = r; }
    
    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}

public class Main {
    public static void main(String[] args) {
        Shape shape = new Circle(5.0);
        System.out.println("Area: " + shape.area());
        shape.info();  // This is a shape.
    }
}
```

### 3.3 추상 클래스 vs 인터페이스

* **추상 클래스**: 상태(필드) 가질 수 있고, 생성자 정의 가능.
* **인터페이스**: JDK 8 이후로 디폴트 메서드와 정적 메서드 허용, 다중 상속 가능.
* 설계 시 “is-a” 관계로 **공통 구현 일부**를 제공할 필요가 있으면 추상 클래스를, **완전 추상** 형태로만 기능 규격을 정의하려면 인터페이스를 사용합니다.

