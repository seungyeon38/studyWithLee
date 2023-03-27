# JAVA의 상속 
- [1. extends](#1-extends)
- [2. implements](#2-implements)
- [3. abstract](#3-abstract)
- [4. 상속 관계에서 객체 생성 방법](#4-상속-관계에서-객체-생성-방법)

### 1. extends
   - 부모의 메소드를 그대로 사용할 수 있으며 오버라이딩 할 필요없이 부모에 구현되어있는 것을 직접 사용 가능 
   - 다중상속 지원X
   - 일반 class와 abstract 클래스 상속에 사용됨. 

```java
class Vehicle {
    protected int speed = 3;
    
    public int getSpeed(){
    	return speed;
    }
    
    public void setSpeed(int speed){
    	this.speed = speed;
    }
}

class Car extends Vehicle{
    public void printspd(){
    	System.out.println(speed);
    }
}

public class ExtendsSample {
    public static main(String[] args) {
    	Car A = new Car();
        System.out.println(A.getSpeed());
        A.Printspd();
    }
}
```

<br/>

### 2. implements
   - 부모의 메소드를 반드시 오버라이딩(재정의)해야 한다. 
   - 다중상속 지원O (자바는 class의 다중상속을 지원하지 않음. Interface는 class가 아니다)
   - interface 상속에 사용됨. 

```java
interface TestInterface {
    public static int num = 8;
    public void fun1();
    public void fun2();
}

class InterfaceExam implements TestInterface {
    @Override
    public void fun1(){
    	System.out.println(num);
    }
    
    @Override
    public void fun2(){
    	...
    }
}

public class InterfaceSample {
    public static void main(String args[]) {
    	InterfaceExam exam = new InterfaceExam();
        exam.fun1();
    }
}
```

<br/>

### 3. abstract
   - 추상메서드를 포함하는 클래스 
   - 추상메서드는 본체가 없는 메서드 
   - 일반 클래스에 필요한 어떤 제약을 줄 때 사용한다. 
   - 객체 생성 불가능 
   - extends와 implements의 혼합으로, extends하되 몇 개는 추상 메서드로 구현되어있다. 

```java
public abstract class SmartPhone {
    // 공통적인 기능
    String call = "전화";
    String sns = "SNS";
    String search = "인터넷 검색";
    String game = "게임";

    // 각각의 기계(단말기)들의 특성
    String company, name, color, size, weight, price;

    void purpose() {
	System.out.println("사용목적 : "+call+" / "+sns+" / "+search+" / "+game);
    }

    // 각각의 단말기(기계)들의 spec
    abstract void spec();    // 추상메서드
}
   
public class Galaxy extends SmartPhone {
    @Override
    void spec() {
    	company = "삼성"; 
	name = "Galaxy Note 20";
	color = "화이트";
	size = "20cm";
	weight = "350g";
	price = "150만원";
		
	System.out.println(company+" / "+name+" / "+color+" / "+size+" / "+weight+" / "+price);
    }
}

public class IPhone extends SmartPhone {
    @Override
    void spec() {
	company = "애플"; 
	name = "IPhone 11"; 
	color = "화이트";
	size = "15cm"; 
	weight = "200g"; 
	price = "150만원";
		
	System.out.println(company+" / "+name+" / "+color+" / "+size+" / "+weight+" / "+price);
		
    }
}

public class Ex03_SmartPhone {
    public static void main(String[] args) {
	Galaxy galaxy = new Galaxy();
	galaxy.purpose();
	galaxy.spec();    // 추상메서드 재정의한 메서드를 호출
	System.out.println();
		
	IPhone iPhone = new IPhone();
	iPhone.purpose();
	iPhone.spec();    // 추상메서드 재정의한 메서드를 호출
    }
}
```

<br/>

### 4. 상속 관계에서 객체 생성 방법
```java
// 모든 클래스는 상속을 받지 않으면 기본적으로 루트 클래스인 Object 클래스(최상위 클래스)를 상속받음
public class Animal extends Object {
    public void eat() {
    	System.out.println("?"); // 포괄적, 추상적
    }
	
    public Animal() {
    	super(); // new Object();
    }
}
```

```java
public class Dog extends Animal {
    // 이름, 나이, 종 등 : 상태정보 존재.
	
    // 재정의(override)
    public void eat() { 
	System.out.println("멍멍이 처럼 먹는다."); 
    }	
	
    public Dog() {
	super();	// new Animal();
    }
}
```

```java
public class Cat extends Animal {
    // 이름, 나이, 종 등 : 상태정보 존재.

    @Override
    public void eat() { 
    	System.out.println("고양이 처럼 먹는다."); 
    }

    public void night() {
	System.out.println("고양이는 밤에 눈에서 빛이 난다.");
    }
	
    public Cat() {
	super();	// new Animal();
    }
}
```

```java
public class Main {
    public static void main(String[] args) {
	// 재정의(오버라이드) 유무에 따라 하위(자식)클래스의 메서드 구동 가능 여부가 결정됨.
	// 1. 직접 이용 (자기 자신 클래스 이용)
	Dog dog = new Dog();
	dog.eat();
		
	Cat cat = new Cat();
	cat.eat();
	cat.night();
		
	// 2. 간접 이용	: 상속관계가 선행되어야 사용 가능. (클래스 형변환하여 객체 생성)
	Animal d = new Dog();	// UpCasting (자동 형 변환/ 자식->부모)
	d.eat(); // 자식 메서드 실행 
		
	Animal c = new Cat();
	c.eat();
        c.night(); // 오류 
	((Cat)c).night();	// DownCasting (강제 형 변환/ 부모->자식)

        Dog dog = new Animal(); // 오류  
    }
}
```
