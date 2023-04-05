# SOLID 원칙 
> 객체 지향 프로그래밍 및 설계의 5가지 기본 원칙 <br/>
> **높은 응집도**와 **낮은 결합도**가 목표 

1. [SRP(Single Responsibility Principle)](#1-srpsingle-responsibility-principle) : 단일 책임 원칙
2. [OCP(Open/Closed Principle)](#2-ocpopenclosed-principle) : 개방/폐쇄 원칙 
3. [LSP(Liskov Substitution Principle)](#3-lspliskov-substitution-principle) : 리스코프 치환 원칙
4. [ISP(Interface Segregation Principle)](#4-ispinterface-segregation-principle) : 인터페이스 분리 원칙
5. [DIP(Dependency Inversion Principle)](#5-dipdependency-inversion-principle) : 의존관계 역전 원칙 

<br/>

## 1. SRP(Single Responsibility Principle)
> 단일 책임 원칙 <br/>
> 어떤 클래스던지 단 하나의 기능만을 책임을 갖는다. 

```java
class Person {
    void cook();    // 요리사 역할 
    void plate();   // 요리사 역할 
    void order();   // 손님 역할 
    void pickup();  // 손님 역할
    void eat();     // 손님 역할
}   
```
Person 클래스는 요리사의 역할과 손님의 역할을 모두 가진 클래스로, 하나의 책임만 가지고 있지 않다. 

<br/>

따라서, Person 클래스는 요리사의 역할과 관련된 기능이 추가될 때마다 코드의 변경을 해줘야 한다. 

```java
class Cook {
    void cook();
    void plate();
} 

class Customer {
    void order();
    void pickup();
    void eat();
}
```
Person 클래스를 단 하나의 책임만 갖도록 Cook 클래스와 Customer 클래스로 구분해주었다. <br/>

이렇게 단일 책임 원칙에 맞게 클래스를 수정하면, 요리사의 역할과 관련된 기능이 추가될 때 Customer 클래스가 변경되지 않아도 된다. <br/>

즉, 클래스 변경으로 인한 다른 클래스에게 영향을 줄일 수 있기 때문에 **응집도가 높아지고 결합도가 낮아진다.**

<br/>

## 2. OCP(Open/Closed Principle)
> 개방/폐쇄 원칙 <br/>
> 기존의 코드를 변경하지 않으면서, 기능을 추가할 수 있도록 설계가 되어야 한다. <br/>
> 확장에 대해서는 개방적(open)이고, 수정에 대해서는 폐쇄적(closed)이어야 한다. <br/>
> 확장에 개방적 : 새로운 타입(클래스, 모듈, 함수)을 추가함으로써 기능을 확장 <br/>
> 수정에 폐쇄적 : 확장이 발생했을 때 해당 코드를 호출하는 쪽에서는 변경이 발생하지 않는 것 <br/>
> '추상화', '다형성'을 이용하여 가능하다.

[적용 전]
```java
class Truck{
    public void drive() {
	System.out.println("Truck Drive");
    }
}

class Bus{
    public void drive() {
	System.out.println("Bus Drive");
    }	
}

public class Driver {
    public static void main(String[] args) {
	// 트럭 운전 인스턴스 생성
	Truck driver1 = new Truck();
	driver1.drive();
		
	//버스 운전 인스턴스 생성
	Bus driver2 = new Bus();
	driver2.drive();
    }
}
```

<br/>

[적용 후]
```java
interface Car {
    void drive();
    void accel();
    void brake();
}

class Bus implements Car {
    void drive() {
        System.out.println("Bus Drive");
    };
    void accel() { //속도 10 증가 };
    void brake() { //속도 5 감소 };
}

class Truck implements Car {
    void drive() {
        System.out.println("Truck Drive");
    };
    void accel() { //속도 5 증가 };
    void brake() { //속도 3 감소 };
}

public class Driver {
    public static void main(String[] args) {
    	// 트럭 운전 인스턴스 생성
	Car driver1 = new Truck();
	driver1.drive();
		
	//버스 운전 인스턴스 생성
	Car driver2 = new Bus();
	driver2.drive();
    }
}
```

위에서 클라이언트(운전자)는 자동차가 변경되더라도 운전하는 것에 대해 영향을 받지 않는다. 이는 클라이언트가 변경에는 닫혀있는 것을 의미한다. <br/>

반대로, 자동차는 Bus나 Truck 이외에도 다른 자동차 종류로 클래스를 인터페이스를 통해 확장할 수 있고, 클라이언트(운전자)의 역할에는 영향을 끼치지 않는다. 이는 확장에는 열려있는 것을 의미한다.

<br/>

또 다른 예시, Java 애플리케이션에서의 JDBC 매니저 

<img width="400" alt="image" src="https://user-images.githubusercontent.com/29995318/229976372-34e24e0a-3413-4946-a3a3-128a616931ff.png">

JDBC 매니저를 상속받는 PostgreSQL, Oracle, Sybase는 모두 변경에는 확장적이지만, 자바 어플리케이션은 수정에 폐쇄적이다. <br/>

더 쉽게 말하자면, Oracle DB의 변화가 발생하여도 자바 어플리케이션에서 수정할 코드는 없다

<br/>

## 3. LSP(Liskov Substitution Principle)
> 리스코프 치환 원칙
> 하위 타입이 상위 타입이 지정한 제약조건들을 지키고, 상위 타입에서 하위 타입으로의 변동이 일어나도 상위타입의 역할을 문제없이 제공해야한다. 

```java
class Car {
    int speed;
    void drive() { 
    	this.speed += 10;
    }
}

class Bus extends Car {
    int speed;
    int km;
	
    @Override 
    void drive() {
    	// 부모 기능 그대로 수행
	this.speed += 10;
	// 하위 타입 기능 추가
	this.km += 1;
    }
}
```
Bus 클래스는 Car 클래스가 제공하는 drive 메소드의 speed += 10기능을 그대로 수행하고 있고, 하위 타입에서 추가적으로 구현한 km += 1을 수행한다. <br/>

이는 상위 타입인 Car클래스가 제공하던 speed += 10 기능을 하위타입에서 제대로 수행할 수 있기 때문에 해당 원칙을 잘 지킨 것이다. <br/>

리스코프 치환 원칙을 지키기 위해서는 하위 타입에서 상위 타입은 상속을 하지만 무분별한 메소드 오버라이딩을 줄이는 것이다. 메소드 오버라이딩을 하더라도 상위 타입이 구현한 기능을 변경없이 구현 후 추가적인 기능을 구현하는 것이 바람직하다.

<br/>

## 4. ISP(Interface Segregation Principle)
> 인터페이스 분리 원칙
> 인터페이스를 최대한 변경을 하지 않도록 구체적으로 구분해야 한다. 

```java
interface Person {
    void cook();
    void plate();
    void order();
    void pickup();
    void eat();
}
```
위와 같이 Person 인터페이스를 요리사 인터페이스의 기능과 손님 인터페이스를 모두 구현할 수 있다.


```java
interface Cook {
    void cook();
    void plate();
}

interface Customer {
    void order();
    void pickup();
    void eat();
}
```
따라서, Cook 인터페이스와 Customer 인터페이스로 구분해 만들어 준다면, Cook 인터페이스에서는 Customer 인터페이스의 기능을, Customer 인터페이스에서는 Cook 인터페이스의 기능을 구현하지 않아도 된다.

<br/>

## 5. DIP(Dependency Inversion Principle)
> 의존관계 역전 원칙 <br/>
> 객체는 구체적인 객체가 아닌 추상화에 의존해야 한다. <br/>
> 자신보다 변화하기 쉬운 것에 의존하지 말아라. 

```java
public class Kid {
    private Robot toy;

    public void setToy(Robot toy) {
        this.toy = toy;
    }

    public void play() {
        System.out.println(toy.toString());
    }
}
```
```java
public class Main {
    public static void main(String[] args) {
        Robot robot = new Robot();
        Kid k = new Kid();
        k.setToy(robot);
        k.play();
    }
}
```
위 상황에서, Kid는 robot이라는 구체적인 객체에 의존하고 있다. <br/>
이런 경우 아이가 가지고 노는 장난감의 종류가 변경될 때, 다음과 같이 Kid 클래스를 수정해야 한다. 

```java
public class Kid {
    private Robot toy;
    private Lego toy; //레고 추가
    
    // 아이가 가지고 노는 장난감의 종류만큼 Kid 클래스 내에 메서드가 존재해야함.
    public void setToy(Robot toy) {
        this.toy = toy;
    }
    public void setToy(Lego toy) {
        this.toy = toy;
    }

    public void play() {
        System.out.println(toy.toString());
    }
}
```
이렇게 아이라는 고수준 모듈이, 변하기 쉬운 장난감이라는 저수준 모듈에게 의존하면 영향에 직접적으로 노출된다. 장난감을 하나 더 추가하기 위해서는 Kid 클래스에 수정까지 해야 한다.

<img width="600" alt="image" src="https://user-images.githubusercontent.com/29995318/229972680-77f0c511-7d54-4cca-9e1d-078b4878f55a.png">

DIP 의존 관계를 맺을 때 자신보다 변화하기 쉬운 것을 의존해서는 안 되고, 거의 변화가 없는 개념에 의존해야 한다는 원칙. <br/>

이제는 아이가 구체적인 객체들(로봇, 레고, 모형 자동차 등)을 직접 의존하지 않고 장난감이라는 추상 클래스와 의존 관계를 맺도록 설계하여, 로봇, 레고, 모형 자동차 같은 구체적인 객체들도 상위 개념인 장난감 클래스에 의존하고 있다. <br/>

이런 설계에서는 장난감의 종류가 아무리 추가되고 변경되어도 아이 객체에 영향을 미치지 않는다. <br/>

```java
public class Kid {
    private Toy toy;

    public void setToy(Toy toy) {
        this.toy = toy;
    }

    public void play() {
        System.out.println(toy.toString());
    }
}
```
더이상 Kid 클래스 내에서 구체적인 장난감 객체들을 생성하지 않고, 장난감이라는 큰 개념의 클래스를 의존하고 있다. <br/>
setToy() 메서드로 가지고 노는 장난감을 바꿀 수 있다.

로봇을 가지고 놀고 싶다면, Toy라는 추상 클래스를 상속 받아 다음과 같이 Robot 객체를 구현한다.

```java
public class Main{
    public static void main(String[] args) {
        Toy robot = new Robot();
        Kid k = new Kid();
        k.setToy(robot);
        k.play();
    }
}
```

레고를 가지고 놀고 싶다면, Toy라는 추상 클래스를 상속 받는 Lego 객체를 구현해주면 된다. 
```java
public class Lego extends Toy {
    public String toString() {
        return "Lego";
    }
}
```

```java
public class Main{
    public static void main(String[] args) {        
        // Toy robot = new Robot();
        Toy lego = new Lego();
        Kid k = new Kid();
        k.setToy(robot);
        k.play();
    }
}
```

새로운 장난감을 추가했지만 Kid 클래스의 코드에는 어떠한 변화도 일어나지 않고, 어떠한 영향도 미치지 않는다. DIP를 만족했기 때문에 변화에 유연한 시스템이 됨.
