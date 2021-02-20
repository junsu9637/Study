[1. 상속](#inheritance)         
[1.1 상속의 정의와 장점](#definition-and-advantages-of-inheritance)                
[1.2 클래스 간의 관계](#relationships-between-classes)                
[1.3 클래스 간의 관계 결정](#determining-relationships-between-classes)                
[1.4 단일 상속](#single-inheritance)              
[1.5 Object 클래스](#object-class)             

[2. 오버라이딩](#overriding)            
[2.1 오버라이딩이란](#what-is-overriding)            
[2.2 오버라이딩의 조건](#conditions-for-overriding)            
[2.3 오버로딩 vs 오버라이딩](#overloading-vs-overriding)               
[2.4 super](#super)                
[2.5 super()](#super-function)           

[3. package와 import](#package-and-import)          
[3.1 package](#package)             
[3.2 package의 선언](#declaration-of-package)               
[3.3 import 문](#import)                          
[3.4 static import 문](#static-import)              

[4. 제어자](#modifier)              
[4.1 제어자란](#what-is-modifier)            
[4.2 static](#static)              
[4.3 final](#final)             
[4.4 abstract](#abstract)              
[4.5 접근 제어자](#access-modifier)               
[4.6 제어자의 조합](#combination-of-modifier)                     

[5. 다형성](#polymorphism)            
[5.1 다형성이란](#what-is-polymorphism)               
[5.2 참조변수의 형변환](#conversion-of-reference-variable)            
[5.3 instanceof 연산자](#instanceoof-operator)                     
[5.4 참조변수와 인스턴스의 연결](#association-of-reference-variables-and-instances)                            
[5.5 여러 종류의 객체를 배열로 다루기](#treat-multiple-types-of-objects-as-arrays)         

[6. 추상클래스](#abstract-class)            
[6.1 추상클래스란](#what-is-abstract-class)          
[6.2 추상메서드](#abstract-method)             
[6.3 추상클래스 작성](#create-of-abstract-class)              

[7. 인터페이스](#interface)             
[7.1 인터페이스란](#what-is-interface)            
[7.2 인터페이스의 작성](#create-of-interface)             
[7.3 인터페이스의 상속](#inheritance-of-interface)              
[7.4 인터페이스의 구현](#implementation-of-interface)                      
[7.5 인터페이스를 이용한 다형성](#polymorphism-with-interface)                  
[7.6 인터페이스의 장점](#advantage-of-interface)                            

[8. 내부 클래스](#inner-class)             
[8.1 내부 클래스란](#what-is-inner-class)            
[8.2 내부 클래스의 종류와 특징](#types-and-characteristics-of-inner-class)         
[8.3 내부 클래스의 선언](#declaration-of-inner-class)                                
[8.4 익명](#anonymous)                


# Inheritance

## Definition and Advantages of Inheritance

**상속**이란 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다. 상속을 통해 클래스를 작성하면 적은 양의 코드로 새로운 클래스를 작성할 수 있고, 코드를 공통적으로 관리할 수 있다. 즉 코드의 재사용성을 높이고 코드 중복을 제거하여 프로그램의 생산성과 유지보수에 크게 기여한다. 

상속을 구현하는 방법은 다음과 같이 새로 작성하고자 하는 클래스의 이름 뒤에 상속받고자 하는 클래스의 이름을 'extends'와 함께 작성한다.
```Java
class Child extends Parent {}
```

위의 두 클래스는 상속 관계에 있다고 하며, 상속해주는 클래스를 '조상 클래스', 상속받는 클래스를 '자손 클래스'라고 한다.

> **조상 클래스** : 부모(parent), 상위(super), 기반(base) 클래스           
  **자손 클래스** : 자식(child). 하위(sub), 파생된(derived) 클래스
  
다음과 같이 Parent 클래스에 age라는 정수형 변수를 맴버변수로 추가하면 Child 클래스에 상속되어 Child 클래스에 자동적으로 정수형 변수 age가 추가된다. 하지만 Child 클래스에 height라는 변수를 추가하더라도 Parent 클래스에는 영향을 줄 수 없다.
```Java
class Parent
{
  int age;
}

class Child extends Parent
{
  // int age;
  int height;
}
```

하나의 조상 클래스는 많은 수의 자손 클래스를 생성할 수 있다. 그리고 자손 클래스도 조상 클래스가 되어 새로운 자손 클래스를 생성할 수 있다.
```Java
class Parent {}
class Child extends Parent {}
class Child2 extends Parent {} // 하나의 조상 클래스가 다른 자손 클래스를 만든다
class GrandChild extends Child {} // 자손 클래스가 다른 자손 클래스의 조상 클래스가 될 수 있다
```

## Relationships between Classes

상속 관계에 있으면 클래스를 재사용할 수 있다고 언급했다. 상속 외에도 **포함 관계**를 통해 클래스를 재사용할 수 있다. 다음과 같이 클래스 간의 포함관계는 한 클래스의 맴버변수로 다른 클래스 타입의 참조변수를 선언하는 것으로 작성하면 된다. 

```Java
class Point
{
  int x;
  int y;
}

class Circle
{
  Point c = new Point(); // 포함관계 형성
  // int x;
  // int y;
  int radius;
}
```

이러한 방식을 통해 코드의 재사용성을 높이고, 간결한 코드를 작성할 수 있다.

## Determining Relationships between Classes

상속과 포함관계는 유사하지만 완전 동일하다고는 할 수 없다. 상속과 포함관계는 다음과 같은 상황을 통해 구분하여 사용한다.

> **상속관계** : ~은 ~이다.        
  **포함관계** : ~은 ~을 포함한다.
  
```markdown
원은 점이다.
원은 점을 가지고 있다.
```

## Single Inheritance

C++에서는 다중상속을 허용하지만 Java에서는 **단일 상속**만을 허용한다. 다중상속을 허용하면 복합적인 기능을 가진 클래스를 쉽게 작성할 수 있는 장점이 있다. 하지만 클래스 간의 관계가 복잡해지고, 다른 클래스로부터 상속받은 맴벼간의 이름이 같은 경우 구별할 수 있는 방법이 없는 단점이 있다.

## Object Class

**Object 클래스**는 모든 클래스 상속계층도의 최상위에 있는 조상 클래스다. 즉 프로그램의 모든 자손 클래스는 Object 클래스로부터 영향을 받는다. 

# Overriding

## What is Overriding

**오버라이딩**이란 다음과 같이 조상 클래스로부터 상속받은 메서드의 내용을 변경하는 것을 말한다. 

```Java
class Point
{
  int x;
  int y;
  String getLocation() { return x, y }
}

class Point3D extends Point
{
  int z;
  
  String getLocation() { return x, y, z } // 오버라이딩
}
```

## Conditions for Overriding

오버라이딩은 메서드의 내용만을 새로 작성하는 것이기 때문에 메서드의 선언부는 조상과 완전히 일치해야 한다. 그래서 오버라이딩이 성립하기 위해서는 다음과 같은 조건을 만족해야 한다.
```markdown
1. 자손 클래스의 이름이 조상 클래스와 같아야 한다.
2. 자손 클래스의 매개변수가 조상 클래스와 같아야 한다.
3. 자손 클래스의 반환타입이 조상 클래스와 같아야 한다. 
```

다만 다음과 같이 접근 제어자와 예외는 제한된 조건 하에서만 다르게 변경될 수 있다.
```markdown
1. 접근 제어자는 조상 클래스의 메서드보다 좁은 범위로 변경 할 수 없다.
2. 조상 클래스의 메서드보다 많은 수의 예외를 선언할 수 없다.
```

## Overloading vs Overriding

오버로딩과 오버라이딩을 혼동하기 쉬운데 둘은 다음과 같은 차이점이 있고, 다음과 같이 구분할 수 있다.
> **오버로딩** : 기존에 없는 새로운 메서드를 정의 (new)       
  **오버라이딩** : 상속받은 메서드의 내용을 변경 (change. modify)
  
```Java
class Parent void parentMethod() {}

class Child extends Parent
{
  void parentMethod() {} // 오버라이딩
  void parentMethod(int i) // 오버로딩
  
  void childMethod() {}
  void childMethod(int i) {} // 오버로딩
}
```

## Super

**Super**은 자손 클래스에서 조상 클래스로부터 상속받은 맴버를 참조하는데 사용하는 참조변수이다. 상속받은 맴버와 자신의 맴버가 이름이 같을 때 super을 붙여서 구별할 수 있다. 

조상 클래스로부터 상속받은 맴버도 자손 클래스 자신의 맴버이기 때문에 this를 사용할 수 있지만 두 클래스 간의 관계를 구별하기 위해서 super를 사용하는 것이 좋다. 

```Java
class Super
{
  public static void main(String args[])
  {
    Child c = new Child()
    c.method();
  }
} 

class Parent { int x=10; }

class Child extends Parent
{
  void method()
  {
    int x = 11;
    System.out.println(x); // 11
    System.out.println(this.x); // 11
    System.out.println(super.x); // 10
  }
}

```

## Super function

this()와 마찬가지로 super()도 생성자이다. this()는 같은 클래스의 다른 생성자를 호출하는데 사용하지만, super()은 조상 클래스의 생성자를 호출하는데 사용한다. 

```Java
class Point
{
  public static void main(String args[])
  {
    Point3D p3 = new Point3D();
    System.out.println(p3.x + ", " + p3.y + ", " + p3.z + ", ") // 100, 200, 300
  }
}

class Point
{
  int x=10;
  int y=20;
  
  Point(int x, int y)
  {
    this.x = x;
    this.y = y;
  }
}

class Point3D extends Point
{
  int z = 30;
  
  Point3D()
  {
    this(100, 200, 300); // Point3D(int x, int y, int z) 호출
  }
  
  Point3D(int x, int y, int z)
  {
    super(x, y); // Point(int x, int y) 호출
    this.z = z;
  }
}
```

```markdown
1. main 메서드 실행
2. Point3D 메서드 실행
3. Point3D() {this(100, 200, 300)} 실행
4. Point3D(int x, int y, int z) 호출
5. Point(int x, int y) 호출
6. object 클래스에서 x=100, y=200
7. Point3D(int x, int y, int z) 복귀
8. Point3D 클래스에서 z=300
9. main 메서드 복귀
```

# Package and Import

## Package

**패키지**는 클래스 집합이다. 패키지에는 클래스 또는 인터페이스를 포함시킬 수 있고, 서로 관련된 클래스들끼리 그룹 단위로 묶어 높음으로써 클래스를 효율적으로 관리할 수 있다. 

패키지는 일종의 디렉토리로 다양한 클래스 파일들이 .을 통해 계층구조를 이룬다. 예를 들어 String의 경우 실제 표현은 java.lang.String이 된다. 이는 java 디렉토리 안에 있는 lang 디렉토리 안에 String이라는 클래스를 의미한다. 

## Declaration of Package

패키지 선언은 다음과 같이 작성한다.
```Java
package PACKAGE_NAME;
```

## Import

코드를 작성할 때 다른 패키지의 클래스를 사용하려면 패키지 명이 포함된 클래스 이름을 사용해야 한다. 하지만 매번 패키지 명을 붙여서 작성하는 것은 효율적인 작업은 아니다. 따라서 **import 문**을 사용하여 사용하고자 하는 클래스의 패키지를 미리 명시하여 코드에서 사용할 때 패키지 명을 생략한다. 

```Java
package java.text.SimpleDataFormat

SimpleDataFormat date = new java.text.SimpleDataFormat()
```

```Java
import java.text.SimpleDataFormat

SimpleDataFormat date = new SimpleDataFormat()
```

## Static Import

**static import 문**을 사용하면 다음과 같이 static 맴버를 호출할 때 클래스 이름을 생략할 수 있다. 

```Java
import java.lang.System.out.println

system.out.println();
```

# Modifier

## What is Modifier

**제어자**는 클래스, 변수, 메서드의 선언부에 함께 사용되어 부가적인 의미를 부여한다. 제어자는 다음과 같이 접근 제어자와 그외 제어자로 나눈다.
> **접근 제어자** : public, protected, default, private           
  **그 외 제어자** : static, final, abstract, native, transient, synchronized, volatile, strictfp

접근 제어자는 한 번에 하나만 선택해서 사용해야 한다. 다양한 제어자가 있지만 그 중에서 가장 많이 사용하는 static, final, abstract, 접근 제어자에 대해 간단하게 알아보자.

## Static

static은 '클래스의', '공통적인'의 의미를 가지고 있다. 따라서 static이 붙은 맴버변수와 메서드, 초기화 블록은 인스턴스가 아닌 클래스에 관계된 것이기 때문에 인스턴스를 생성하지 않고도 사용 가능한 것이다. 

## Final

final은 '마지막의', '변경될 수 없는'의 의미를 가지고 있다. 따라서 거의 모든 대상에 사용할 수 있고, 변경 불가능한 상태로 만든다.

## Abstract

abstract는 '미완성'의 의미를 가지고 있다. 따라서 메서드 선언부에서 작성되어 아직 구현하지 않은 추상 메서드를 선언하는데 사용한다. 

## Access Modifier

**접근 제어자**는 맴버 또는 클래스에 사용되어 해당 맴버 또는 클래스를 외부에서 접근 불가능하도록 제한한다. 접근 제한을 위해서 4가지의 명령어를 사용한다. 이 명령어들은 다음과 같이 접근 범위를 제한한다.
| 제어자 | 같은 클래스 | 같은 패키지 | 자손 클래스 | 전체 |
|:-:|:-:|:-:|:-:|:-:|
| public | o | o | o | o |
| protected | o | o | o |  |
| default | o | o |  |  |
| private | o |  |  |  |

```Java
class Private {private int a;}

class test
{
    public static void main(String args[])
    {
        Private p = new Private();
        p.a = 1; // 클래스 Private의 a가 private 상태이기 때문에 에러 
    }
}
```

이 중 default는 생략 가능하다.

접근 제어자는 주로 **캡슐화**를 위해 사용한다. 캡슐화는 객체지향개념의 대표적인 기능으로 다음과 같은 기능을 위해 사용한다.
```markdown
1. 외부로부터 데이터를 보호
2. 외부에 내용을 숨김
```

## Combination of Modifier

제어자는 다양하게 존재하는 데 이런 제어자들을 조합해서 사용할 때는 다음과 같은 사항을 주의해야한다.
```
1. 메서드에 static과 abstract를 함께 사용할 수 없다.
2. 클래스에 abstract와 final을 동시에 사용할 수 없다.
3. abstract 메서드의 접근 제어자가 private일 수 없다.
4. 메서드에 private와 final을 같이 사용할 필요 없다.
```

# Polymorphism

## What is Polymorphism

**다형성**은 여러 가지 형태를 가질 수 있는 능력을 의미한다. Java에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함으로써 다형성을 프로그래밍적으로 구현한다. 이는 다음과 같이 조상 클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 코드를 작성한다.

```Java
class TV
{
    boolean power;
    int channel;
    
    void power(); { power = !power; }
    void channelUp(); { ++channel; }
    void channelDown(); { --channel; }
}

class CaptionTV extends TV
{
    String text;
    void caption() { ~~~ }
}
```

이런 방식으로 다형성을 구현하면 조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있다. 하지만 자손타입의 참조변수로는 조상타입의 인스턴스를 참조할 수 없다. 

## Conversion of Reference Variable

참조변수도 형변환이 가능하지만 서로 상속관계에 있는 클래스 사이에서만 가능하다. 따라서 다음과 같은 형변환만 가능하다.
```markdown
자손타입 -> 조상타입 : Up-casting 형변환 생략가능
조상타입 -> 자손타입 : Down-casting 형변화 생략불가
```

형변환은 참조변수의 타입을 변환하는 것이지 인스턴스를 변환하는 것은 아니기 때문에 참조변수 형변환은 인스턴스에 아무런 영향을 주지 않는다. 단지 참조변수의 형변환을 통해 참조하고 있는 인스턴스에 서 사용할 수 있는 맴버의 개수를 조절하는 것 뿐이다. 

```Java
class CastingEx
{
    public static void main(String args[])
    {
        Car car = null;
        FireEngine fe1 = new FireEngine();
        FireEngine fe2 = null;
        
        fe1.water();
        car = fe1; // car = (Car)fe1; 생략
        car.water(); // error Car 타입의 참조변수로는 water() 호출 불가능 
        fe2 = (FireEngine)car; // 조상타입 -> 자손타입
        fe2.water();
    }
}

class Car
{
    String color;
    int door;
    
    void drive() {}
    void stop() {}
}

class FireEngine extends Car
{
    void water() {}
}
```

## Instanceoof Operator

**instanceof 연산자**는 참조변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 사용한다. instanceof 왼쪽에는 참조변수를, 오른쪽에는 타입(클래스명)이 피연산자로 위치한다. 연산의 결과는 true, false로 반환된다. instanceof는 다음과 같이 주로 조건문에 사용한다. 

```Java
void Work(Car c)
{
    if(c instanceof FireEngine) {}
    else if(c instanceof Albulance) {}
}
```

instanceof 연산자가 true값이 출력되는 것은 참조변수가 검사한 타입으로 형변환이 가능하다는 것을 의미한다.

## Association of Reference Variables and Instances

**참조변수와 인스턴스를 연결할 때** 조상 클래스에 선언된 맴버변수와 같은 이름의 인스턴트 변수를 자손 클래스에 중복으로 정의된 경우, 다음과 같은 두 상황에서 다른 결과를 얻는다
```markdown
1. 조상타입 참조변수로 자손 인스턴스 참조
2. 자손타입 참조변수로 자손 인스턴스 참조
```

맴버변수가 조상 클래스와 자손 클래스에 중복으로 정의된 경우, 다음과 같이 작업이 진행된다.
```markdown
조상타입 참조변수를 사용 : 조상 클래스에 선언된 맴버변수 사용
자손타입 참조변수를 사용 : 자손 클래스에 선언된 맴버변수 사용
```

하지만 중복 정의가 아닌 경우, 조상타입의 참조변수를 사용했을 때와 자손타입의 참조변수를 사용했을 때의 차이가 없다. 

```Java
class Ex
{
    public static void main(String args[])
    {
        Parent p = new Child // Child 인스턴스를 참조하는 Parent 타입 참조변수 p
        Child c = new Child // Child 인스턴스를 참조하는 Child 타입 참조변수 c
        
        // 조상타입 참조변수를 사용하기 때문에 조상 클래스에서 선언된 맴버변수 사용
        System.out.println(p.x) // 100
        // 자손타입 참조변수를 사용하기 때문에 자손 클래스에서 선언된 맴버변수 사용
        System.out.println(c.x) // 200
        
        p.method(); // Child
        c.method(); // Child
    }
}

class Parent
{
    int x = 100;
    
    void method()
    {
        System.out.println("Parent")
    }

class Child
{
    int x = 200;
    
    void method()
    {
        System.out.println("Child")
    }
}
```

## Treat Multiple Types of Objects as Arrays

**Vector 클래스**는 내부적으로 Object 타입의 배열을 가지고 있다. 따라서 이 배열에 객체를 추가하거나 제거할 수 있게 작성되어 여러 종류의 객체를 배열로서 다룰 수 있게 된다. 그리고 배열의 크기를 알아서 관리해주기 때문에 저장할 인스턴스의 개수에 신경 쓰지 않아도 된다.

```Java
import java.util.*; // vector 클래스 사용을 위한 호출

Vector v = new Vector();
```

# Abstract class

## What is Astract Class

**추상 클래스**는 완성되지 못한 클래스를 뜻한다. 미완성 클래스는 클래스가 미완성 메서드를 포함한다는 뜻으로 맴버의 개수와는 관계 없다. 추상 클래스로는 인스턴스를 생성할 수 없고, 상속을 통해 자손클래스에서만 완성할 수 있다.

추상클래스 자체로는 클래스의 역할을 수행할 수 없다. 하지만 새로운 클래스를 작성하는 조상 클래스의 역할을 수행하면서 어느정도 새로운 클래스의 틀을 만들어주는 역할은 수행할 수 있다. 

다음과 같이 클래스 선언 앞에 abstract를 추가하면 추상 클래스가 된다. 
```Java
abstract class CLASS_NAME {}
```

## Abstract Method

**추상 메서드**는 선언부만 작성하고 구현부는 작성하지 않은 메서드를 의미한다. 추상 메서드를 사용하는 이유는 상속받는 클래스에 따라 메서드의 내용이 달라질 수 있기 때문에 사용한다. 이 때, 주석을 덧붙여 어떤 기능을 수행할 목적으로 작성되었는지 알려주고, 실제 내용은 상속받은 클래스에서 구현하면 된다. 

다음과 같이 메서드 선언 앞에 abstract를 추가하면 추상 메서드가 된다.
```Java
/* 주석을 통해 어떤 기능을 수행할 목적으로 작성하였는지 설명 */
abstract RETURN_TYPE METHOD_NAME();
```

## Create of Abstract Class

추상 클래스를 작성하는 법을 알아보기 전에 프로그램 개념에서 추상화와 구체화의 개념에 대해 이해해야한다. 이 두 개념은 다음과 같다.

> **추상화** : 클래스 간의 공통점을 찾아내 공통의 조상을 만드는 작업             
  **구체화** : 상속을 통해 클래스를 구현, 확장하는 작업
  
```Java
abstract class Player // 추상 클래스 Player 정의
{
    boolean pause;
    int currentPos;
    
    player() // 추상 클래스도 생성자가 있어야 한다.
    {
        pause = false;
        currentPos = 0;
    }
    
    /* 지정된 위치(pos)에서 재생을 시작하는 기능이 수행하도록 작성 */
    abstract void play (int pos); // 추상 메서드
    
    void play()
    {
        play(currentPos) // 추상 메서드 사용
    }
}
```

# Interface

## What is Interface

**인터페이스**는 일종의 추상 클래스로 추상클래스처럼 추상 메서드를 갖지만 추상클래스보다 추상화 정도가 높다. 따라서 추상클래스와 달리 일반 메서드나 맴버변수를 가질 수 없다. 즉 추상메서드와 상수만 맴버로 가질 수 있다. 

추상 클래스가 '미완성 설계도'라면 인터페이스는 '기본 설계도'라고 이해하면 된다. 인터페이스 자체로는 특별한 기능을 구현할 수 없지만 다른 클래스를 작성하는데 도움을 줄 수 있다. 

## Create of Interface

인터페이스를 작성할 때는 다음과 같은 제약이 있다.
```markdown
1. 모든 맴버변수는 public static final 이어야 하고, 이는 생략할 수 있다.
2. 모든 메서드는 public abstract 이어야 하고, 이를 생략할 수 있다.
```

인터페이스는 다음과 같이 작성된다.
```Java
interface INTERFACE_NAME
{
    public static final TYPE NAME = VALUE; // 상수
    // public static final int A = 1;
    // final int A = 1;
    // static int A = 1;
    // int A = 1;
    public abstract METHOD_NAME(); // 추상 메서드
    // public abstract String METHOD();
    // String METHOD();
}
```

## Inheritance of Interface

인터페이스 간의 상속이 가능하고, 클래스와 달리 다중상속이 가능하다. 
```Java
interface A {}
interface B {}
interface C {}

interface Child extends A, B, C {}
```

## Implementation of Interface

인터페이스는 추상 클래스와 같이 그 차제로는 사용할 수 없고, 자신에 정의된 추상메서드의 내용을 완성시켜주는 클래스를 작성해야 사용할 수 있다. 다만 추상 클래스는 상속을 위해 'extends'를 사용하지만 인터페이스는 'implements'를 사용한다. 

```Java
class CLASS_NAME implements INTERFACE_NAME
{
    // 인터페이스에 정의 된 추상메서드 구현
}

class Fighter implements Fightable
{
    public void move() {}
    public void attack() {}
}
```

## Polymorphism with Interface

앞서 다형성은 자손클래스의 인스턴스를 조상타입의 참조변수로 참조하는 것이 가능하다고 언급했다. 인터페이스를 이용해서 다형성을 구현할 수 있다. 인터페이스 Fightable을 클래스 Fighter가 구현했다고 가정하면 다음과 같이 Fighter 인스턴스를 Fightable 타입의 참조변수로 참조하는 것이 가능하다.
```Java
Fightable f = (Fightable)new Fighter();
```

따라서 인터페이스는 다음과 같이 메서드의 매개변수의 타입으로 사용될 수 있다.
```Java
void attack (Fightable f) {}
```

그리고 다음과 같이 메서드의 리턴타입으로 인터페이스 타입을 지정할 수 있다.
```Java
Fightable method()
{
    Fightable f = new Fighter;
    return f;
}
```

여기서 리턴타입이 인터페이스라는 것은 메서드가 해당 인터페이스를 구현한 클래스의 인터페이스를 반환한다는 것을 의미한다. 

## Advantage of Interface

인터페이스를 사용하면 다음과 같은 장점을 얻을 수 있다.
```markdown
1. 개발 시간 단축
2. 표준화
3. 관계없는 클래스들간 관계 형성
4. 독립적 프로그래밍
```

### 개발 시간 단축

인터페이스를 사용하면 메서드를 호출하는 쪽에서 메서드의 내용과 관계없이 선언부만 알면 되기 때문에 개발 시간이 단축된다. 그리고 인터페이스와 관련된 메서드를 2개 작성해야 하는 경우, 2명이 각각 동시에 개발이 가능해서 개발 시간이 단축된다.

### 표준화

프로젝트에 사용되는 기본 틀을 인터페이스로 작성한 후 개발자들이 프로그램을 작성한다면 개발자의 수가 많아져도 정량화된 프로그램이 개발된다.

### 관계없는 클래스들간 관계 형성

서로 상속관계에 있지 않고, 같은 조상클래스를 갖고 있지 않는 클래스들에게 하나의 인터페이스를 공통적으로 구현해주면 서로 관계를 만들어 줄 수 있다.

### 독립적 프로그래밍

인터페이스를 사용하면 클래스의 선언부와 구현부를 분리시킬 수 있기 때문에 실제 구현에서 독립적인 프로그램 작성이 가능하다. 즉 한 클래스의 변경이 관련된 다른 클래스에 영향을 미치지 않는 독립적인 프로그래밍이 가능하다. 

# Inner-class

## What is Inner Class

**내부 클래스**는 클래스 내에 선언된 클래스다. 클래스에 다른 클래스를 선언하는 이유는 다음과 같다.
```Java
1. 내부 클래스에서 외부 클래스의 맴버들을 쉽게 파악할 수 있다.
2. 코드의 복잡성을 줄일 수 있다(캡슐화).
```

## Types and Characteristics of Inner Class

내부 클래스의 종류와 특징은 다음과 같다.

| 내부 클래스 | 특징 |
|:-:|:-|
| 인스턴스 클래스 | 외부 클래스의 맴버변수 선언위치에 선언. 외부 클래스의 인스턴스 맴버처럼 다뤄진다. 주로 외부 클래스의 인스턴스 맴버들과 관련된 작업에 사용될 목적으로 선언된다.|
| static 클래스 | 외부 클래스의 맴버변수 선언위치에 선언. 외부 클래스의 static 맴버처럼 다뤄진다. 주로 외부 클래스의 static 맴버, static 메서드에서 사용될 목적으로 선언된다. |
| 지역 클래스 | 외부 클래스의 메서드나 추기화블록 안에 선언. 선언된 영역 내부에서만 사용될 수 있다. |
| anonymous 클래스 | 클래스의 선언과 객체의 생성을 동시에 하는 이름없는 클래스(일회용) |

## Declaration of Inner Class

내부 클래스는 다음과 같이 선언할 수 있다. 다음의 두 코드는 같은 코드로, 첫 번째 코드는 일반 코드이고, 두 번째 코드는 내부 클래스를 선언한 코드이다. 
```Java
class Outer
{
    int iv = 0;
    static int cv = 0;
    
    void Method()
    {
        int lv = 0;
    }
}
```
```Java
class Outer
{
    class InstaceInner {}
    static class StaticInner {}
    
    void Method()
    {
        class LocalInner {}
    }
}
```

## Anonymous

**익명 클래스**는 이름이 없는 클래스다. 클래스의 선언과 객체 생성을 동시에 하기 때문에 단 한번만 사용할 수 있고, 하나의 객체만 생성할 수 있다. 이름이 없기 때문에 생성자도 가질 수 없고, 단 하나의 클래스 상속이나 인터페이스 구현만 가능하다. 익명 클래스는 다음과 같이 작성된다.
```Java
new PARENT_CLASS_NAME() {} // 클래스 상속 익명 클래스
new INTERFACE_NAME() {} // 인터페이스 구현 익명 클래스
```
