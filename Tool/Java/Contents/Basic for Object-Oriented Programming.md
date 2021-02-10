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
3.1 선언위치에 다른 변수의 종류(## Type of Other Variable in Declaration Location
3.2 클래스 변수와 인스턴스 변수(## Class Variable and Instance Variable
3.3 메서드(## Method
3.4 메서드의 선언과 구현(## Creating and Using Method
3.5 메서드의 호출(## Call of Method
3.6 return 문(## Return
3.7 JVM의 메모리구조(## Memory Structure of JVM
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








