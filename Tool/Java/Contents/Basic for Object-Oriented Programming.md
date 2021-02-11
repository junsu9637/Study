[1. 객체지향언어](#object-oriented-programming)            
[1.1 객체지향언어의 역사](#history-of-object-oriented-programming)            
[1.2 객체지향언어](#object-oriented-programming)                   

[2. 클래스와 객체](#class-and-object)                   
[2.1 클래스와 객체의 정의와 용도](#definition-and-purpose-of-class-and-object)                
[2.2 객체와 인스턴스](#object-and-instance)               
[2.3 객체의 구성요소](#components-of-object)            
[2.4 인스턴스의 생성과 사용](#creating-and-using-instance)            
[2.5 객체 배열](#object-array)              
[2.6 클래스의 다른 정의](#different-definition-of-class)                

[3. 변수와 메서드](#variable-and-method)             
[3.1 선언위치에 다른 변수의 종류](#type-of-other-variable-in-declaration-location)             
[3.2 클래스 변수와 인스턴스 변수](#class-variable-and-instance-variable)            
[3.3 메서드](#method)           
[3.4 메서드의 선언과 구현](#creating-and-using-method)           
[3.5 메서드의 호출](#call-of-method)            
[3.6 return 문](#return)             
[3.7 JVM의 메모리구조](#memory-structure-of-JVM)              
[3.8 기본형 매개변수와 참조형 매개변수](#basic-and-reference-parameter)              
[3.9 참조형 변환타입](#referential-conversion-type)            
[3.10 재귀호출](#recursive-call)            
[3.11 클래스 메서드와 인스턴스 메서드](#class-method-and-instance-method)                
[3.12 클래스 맴버와 인스턴스 맴버간의 참조와 호출](#reference-and-call-between-class-member-and-instance-member)           

[4. 오버로딩](#overloading)        
[4.1 오버로딩이란](#what-is-overloading)           
[4.2 오버로딩의 조건](#condition-for-overloading)           
[4.3 오버로딩의 예](#example-of-overloading)            
[4.4 오버로딩의 장점](#advantage-of-overloading)             
[4.5 가변인자와 오버로딩](#variable-factor-and-overloading)                 

[5. 생성자](#generator)        
[5.1 생성자란](#what-is-generator)            
[5.2 기본 생성자](#default-constructor)         
[5.3 매개변수가 있는 생성자](#generator-with-parameter)                
[5.4 생성자에서 다른 생성자 호출](#call-another-constructor-from-constructor)              
[5.5 생성자를 이용한 인스턴스 복사](#copy-instance-using-the-constructor)                 

[6. 변수의 초기화](#initialize-variable)             
[6.1 변수의 초기화](#initialize-variables)            
[6.2 명시적 초기화](#explicit-initialization)            
[6.3 초기화 블록](#initialization-block)               
[6.4 맴버변수의 초기화 시기와 순서](#initialization-of-member-variable)           

# Basic for Object-Oriented Programming

## History of Object Oriented Programming

컴퓨터는 주로 모의실험을 목적으로 사용되어 왔다. 연구원들은 모의실험을 위해 실제 세계와 유사한 가상세계를 컴퓨터 속에 구현하고자 **객체지향이론**을 만들었다. 객체지향이론은 `실제 세계는 객체로 이루어져 있으며, 발생하는 모든 사건들은 사물간의 상호작용이다.` 라는 기본 개념을 바탕으로 발전되어 왔다. 

1960년대 중반에 Simula라는 상속, 캡슐화, 추상화 개념이 포함된 최초의 객체지향언어가 개발되었다. 

## Object Oriented Programming

객체지향언어는 다음과 같은 특징을 갖는다.
```markdown
1. 코드의 재사용성이 높다
2. 코드의 관리가 용이하다
3. 신뢰성이 높은 프로그래밍이 가능하다
```

객체지향개념을 살펴볼 때, 재사용성, 유지보수성, 중복된 코드 제거의 3가지 관점에서 살펴보아야 한다.

객체지향 프로그래밍은 프로그래머에게 거시적 관점에서 설계할 수 있는 능력을 요구한다. 따라서 프로그래머는 너무 객체지향개념에 얽메여서 고민하기 보다는 프로그램을 완성한 다음 보다 객체지향적으로 코드를 개선하는 방향으로 수정하는 방법을 사용해야한다.

# Class and Object

## Definition and Purpose of Class and Object

**클래스**는 '객체를 정의해 높은 것', '객체의 설계도'라고 정의할 수 있다.
```markdown
정의 : 객체를 정의해 놓은 것
용도 : 객체를 생성
```

**객체**는 '실제로 존재하는 것'으로 정의할 수 있다. 객체지향이론에서는 유형적인 것(사물) 뿐만 아니라 무형적인 것(개념, 논리)도 객체로 간주한다.
```markdown
정의 : 실제로 존재하는 것
용도 : 객체가 가지고 있는 기능과 속성에 따라 다름
```

클래스를 정의하고 클래스를 통해 객체를 생성하는 이유는 설계도를 통해 제품을 만드는 것과 같다. 하나의 설계도만 잘 만들면 제품을 생성하는 것은 쉬운 것과 같은 맥락이다.

## Object and Instance

클래스로부터 객체를 만드는 과정을 클래스의 **인스턴스화**라고 하며, 클래스로부터 만들어진 객체를 그 클래스의 **인스턴스**라고 한다.

`클래스 -(인스턴스화)-> 인스턴스(객체)`

## Components of Object

객체는 **속성**과 **기능**의 구성요소로 이루어져 있다. 객체가 가지고 있는 속성과 기능을 그 객체의 **맴버**라고 한다.

클래스는 다음과 같은 객체의 모든 속성과 기능을 정의한다. 

```markdown
속성 : 맴버변수, 특성, 필드, 상태
기능 : 메서드, 함수, 행위
```

보통 '속성'보다는 '맴버변수'를, '기능'보다는 '메서드'를 주로 사용한다.

```Java
class TV
{
    // 속성(변수)
    String color;
    boolean power;
    int channel;
    
    // 기능(메서드)
    void power() { power = !=power; }
    void channelUp() { channel++; }
    void channelDown() { channel--; }
}
```

## Creating and Using Instance

클래스로부터 인스턴스를 생성하는 방법은 다음과 같다.
```Java
Class_Name Variable_Name; // 클래스의 객체를 참조하기 위한 참조변수 선언
Variable_Name = new Class_Name(); // 클래스의 객체를 생성 후, 객체의 주소를 참조변수에 저장
```

```Java
class TV
{
    // 속성(변수)
    String color;
    boolean power;
    int channel;
    
    // 기능(메서드)
    void power() { power = !=power; }
    void channelUp() { channel++; }
    void channelDown() { channel--; }
}

class TVTest
{
    public static void main(String[] args)
    {
        TV t; // TV 인스턴스를 참조하기 위한 변수 t 선언
        t = new TV() // TV 인스턴스를 생성
        
        t.channel = 7;
        t.channelDown(); 
        Systme.out.printf(t.channel) // 6
    }
}
```

인스턴스는 참조변수를 통해서만 다룰 수 있으며, 참조변수의 타입은 인스턴스 타입과 일치해야한다.


## Object Array

**객체 배열**은 참조변수들을 하나로 묶은 참조 변수 배열이다. 즉, 객체 배열 안에 객체가 저장되는 것이 아니라 객체의 주소가 저장된다. 객체 배열은 다음과 같이 생성한다.

`TV[] tvArray = new TV[3];`

객체 배열의 요소별 저장은 일반 배열과 같은 방식으로 이루어진다.

## Different Definition of Class

앞서 객체지향이론의 관점에서 클래스를 '객체를 생성하기 위한 틀'이라고 정의했다. 이번에는 프로그래밍적 관점에서 클래스의 정의와 의미를 살펴본다.

### 클래스 : 데이터와 함수의 결합

프로그래밍 언어에서 데이터 처리를 위한 데이터 저장형태의 발전과정은 다음과 같다.

`변수 -> 배열 -> 구조체 -> 클래스`

```markdown
변수 : 하나의 데이터 저장 공간
배열 : 같은 종류의 여러 데이터 저장 공간
구조체 : 다른 종류의 여러 데이터 저장 공간
클래스 : 데이터와 함수의 결합(구조체 + 함수)
```

객체지향언어에서는 데이터와 함수를 클래스에 정의하여 서로 관련된 변수와 함수들을 함께 다룰 수 있게 했다. 

### 클래스 : 사용자정의 타입

프로그래밍언어에서 제공하는 자료형 외에 프로그래머가 서로 관련된 변수들을 묶어서 만든 새로운 타입을 **사용자정의 타입**이라고 한다. 

# Variable and Method

## Type of Other Variable in Declaration Location

변수는 **클래스 변수(공유 변수)**, **인스턴스 변수**, **지역 변수**로 나뉘어진다. 이렇게 변수의 종류를 결정짓는 요소는 '변수가 선언된 위치'다. 

| 변수의 종류 | 선언 위치 | 생성 시기 |
|:-:|:-:|:-:|
| 클래스 변수 | 클래스 영역 | 클래스가 메모리에 적재될 때 |
| 인스턴스 변수 | 클래스 영역 | 인스턴스가 생성될 때 |
| 지역 변수 | 클래스 영역 이외의 영역 | 변수 선언문이 수행될 때 |

맴버 변수를 제외한 모든 변수는 지역 변수에 해당하고, 맴버 변수 중 static이 붙는다면 클래스 변수, 없으면 인스턴트 변수에 해당한다.
```Java
class Variables
{
    int iv; // 인스턴스 변수
    static int cv; // 클래스 변수
    
    void method()
    {
        int lv; // 지역 변수
    }
}
```

### 인스턴스 변수

클래스 영역에서 선언되어 클래스의 인스턴스를 생성할 때 생성된다. 따라서 인스턴스 변수의 값을 읽거나 저장하기 위해서는 먼저 인스턴스를 생성해야 한다. 

인스턴스는 독립적인 저장공간을 가지므로 서로 다른 값을 가질 수 있다. 따라서 인스턴스마다 고유한 상태를 유지해야하는 속성을 인스턴스 변수로 선언한다. 

### 클래스 변수

클래스 변수는 인스턴스가 공통된 저장공간(변수)을 공유하게 된다. 즉 인스턴스마다 독립적인 공간을 갖는 인스턴스 변수와는 달리 한 클래스의 모든 인스턴스 들의 공통적인 값을 유지해야하는 속성을 클래스 변수로 선언한다.

클래스 변수는 언제든지 사용할 수 있고, `Class_Name.Class_Variable`위 형식으로 사용한다. 

클래스가 메모리에 적재될 때 생성되어 프로그램이 종료될 때 까지 유지된다. 그리고 앞에 public을 붙이면 같은 프로그램 내에서 어디서나 접근 가능한 **전역 변수**의 성격을 갖는다.

### 지역 변수

메서드 내에 선언되어 메서드 내에서만 사용 가능하다. 메서드가 종료되면 소멸되어 사용할 수 없게 된다. 

## Class Variable and Instance Variable

클래스 변수와 인스턴스 변수의 차이를 이해하기 위해 다음의 예제를 보자
```Java
class Card
{
    String kind;
    int number;
    static int width = 100;
    static int height = 250;
}

class CardTest
{
    public static void main(String[] args)
    {
        System.out.println("Card.width = " + Card.width);
        System.out.println("Card.height = " + Card.height);
        
        Card c1 = new Card();
        c1.kind = "Spade";
        c1.number = 1;
        
        Card c2 = new Card()'
        c2.kind = "Heart"
        c2.number = 2;
        
        System.out.println(c1.kind + ", " + c1.number + c1.width + ", " + c1.height); // Spade, 1, 100, 250
        System.out.println(c2.kind + ", " + c2.number + c2.width + ", " + c2.height); // Heart, 2, 100, 250
        
        c1.width = 50;
        c1.height = 100;
        
        System.out.println(c1.kind + ", " + c1.number + c1.width + ", " + c1.height); // Spade, 1, 50, 100
        System.out.println(c2.kind + ", " + c2.number + c2.width + ", " + c2.height); // Heart, 2, 50, 100
        
    }
}
```

Card 인스턴스는 자신만의 형태(kind)와 숫자(number)를 유지하고 있어야 하기 때문에 이들을 **인스턴스 변수**로 선언했고, 카드의 폭(width)과 높이(height)는 모든 인스턴스가 공통적으로 같은 값을 유지해야하기 때문에 **클래스 변수**로 선언했다.

## Method

**메서드**는 특정 작업을 수행하는 일련의 문장들을 하나로 묶은 것이다. 메서드는 다음과 같은 3가지 이점으로 인해 사용한다.

### 높은 재사용성

메서드는 한 번 만들면 다른 프로그램에서도 사용이 가능하다. 우리가 사용하는 System.out.printf와 같은 것들이 메서드에 해당한다.

### 중복된 코드 제거

프로그램을 작성하다 보면 같은 내용의 문장이 여러 곳에 반복되는 경우가 존재한다. 이렇게 반복되는 문장을 메서드로 작성하면 반복되는 문장들을 메서드 호출로 대신할 수 있다. 이를 통해 코드의 길이를 줄일 수 있다. 

### 프로그램의 구조화

메서드를 통해 한줄 한줄 작성되는 프로그램을 구조화할 수 있다. 짧은 프로그램의 경우 구조화가 필요하지 않지만 운영체제와 같이 100만 줄이 넘어가는 대규모 프로그램에서는 문장들을 작업단위로 나눠서 여러 개의 메서드에 담아 프로그을 구조화 하는 작업이 필수적이다.

## Creating and Using Method

메서드는 다음과 같이 **선언부**와 **구현부**로 이루어져있다.
```Java
Type Method_Name (Type Variable_Name ...) // 선언부
{
    // 
}
```
```Java
int add(int a, int b)
{
    int result = a + b;
    return result;
    // 위의 두 줄을 return a + b로 간단히 표현할 수 있다.
}
```

## Call of Method

메서드를 호출하는 방법은 다음과 같다.
```
Method_Name(value1, value2, ...)
```

메서드를 호출할 때 ()안에 지정해준 값들을 **인자**라고 한다. 인자의 개수와 순서는 호출된 매서드에 선언된 매개변수와 일치해야한다. 
```Java
class Math
{
    int add(int a, int b) { return a+b; }
    int subtract(int a, int b) { return a-b; }
    int multiply(int a, int b) { return a*b; }
    float divide(float a, float b) { return a/b; }
}

class Ex
{
    public static void main(String[] args)
    {
        Math m = new Math();
        int value = m.add(1, 2);
    }
}
```

위 프로그램을 실행하면 다음과 같은 순서로 작업이 진행된다. 
```markdown
1. 메서드 add를 호출한다.
2. add를 호출할 때 지정된 1과 2를 메서드 add의 매개변수 a, b에 복사한다.
3. 메서드 add의 {}안에 있는 문장을 수행한다.
4. 메서으 add의 모든 문장을 수행하거나 return 문을 만나면 원래 메서드로 돌아간다.
```

## Return

**return 문**은 현재 실행중인 메서드를 종료하고 호출한 메서드로 되돌아가는 명령어다. 모든 메서드에는 반환값이 없더라도 return 문이 있어야 한다. 하지만 반환타입이 void인 경우 컴파일러가 자동적으로 return 문을 추가해주기 때문에 없어도 에러가 되지 않는다. 

## Memory Structure of JVM

응용 프로그램이 실행되면 JVM은 시스템으로부터 프로그램을 수행하는데 필요한 메모리를 할당받고, 할당받을 메모리를 용도에 따라 여러 영역으로 나누어 관리한다. 이 영역은 다음과 같이 **메서드 영역**, **힙 영역**, **호출 스텍 영역**으로 나눈다. 

### 메서드 영역

프로그램 실행 중 클래스가 사용되면 JVM은 해당 클래스의 클래스 파일(.class)을 읽어 클래스에 대한 정보를 메서드 영역에 저장한다. 이 때, 클래스 변수도 이 영역에 함께 생성된다.

### 힙

힙은 인스턴스가 생성되는 공간이다. 프로그램 실행 중 생성되는 모든 인스턴스는 이곳에 생성된다. 

### 호출 스텍

호출 스텍은 메서드의 작업에 필요한 메모리 공간을 제공한다. 메서드가 호출되면 호출 스텍에 호출된 메서드를 위한 메모리가 할당된다. 이 메모리는 메서드가 작업을 수행하는 동안 지역변수들과 연산의 중간 결과 등을 저장한다. 그리고 메서드가 작업을 마치면 할당되었던 메모리 공간은 반환되어 비워진다. 

각 메서드를 위한 메모리상의 작업공간은 서로 구분된다. 각 작업공간은 스텍과 같이 저장되며 가장 위에 위치한 메서드가 실행된다. 호출 스텍은 다음과 같이 구성되고 굵게 표현된 메서드가 현재 실행중인 메서드다.


|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|  |  |  | **println** |  |  |  |
|  |  | **second** | second | **second** |  |  |
|  | **first** | first | first | first | **first** |  |
| **main** | main | main | main | main | main | **main** |



3.8 기본형 매개변수와 참조형 매개변수(## Basic and Reference Parameter
3.9 참조형 변환타입(## Referential Conversion Type
3.10 재귀호출(## Recursive Call
3.11 클래스 메서드와 인스턴스 메서드(## Class Method and Instance Method
3.12 클래스 맴버와 인스턴스 맴버간의 참조와 호출(## Reference and Call between Class Member and Instance Member

4. 오버로딩(# Overloading
4.1 오버로딩이란(## What is Overloading
4.2 오버로딩의 조건(## Condition for Overloading
4.3 오버로딩의 예(## Example of Overloading
4.4 오버로딩의 장점(## Advantage of Overloading
4.5 가변인자와 오버로딩(## Variable Factor and Overloading

5. 생성자(# Generator
5.1 생성자란(## What is Generator
5.2 기본 생성자(## Default Constructor
5.3 매개변수가 있는 생성자(## Generator with Parameter
5.4 생성자에서 다른 생성자 호출(## Call Another Constructor from Constructor
5.5 생성자를 이용한 인스턴스 복사(## Copy Instance Using the Constructor

6. 변수의 초기화(# Initialize Variable
6.1 변수의 초기화(## Initialize Variables
6.2 명시적 초기화(## Explicit Initialization
6.3 초기화 블록(## Initialization Block
6.4 맴버변수의 초기화 시기와 순서(## Initialization of Member Variable








