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

|  |  |  | **println** |  |  |  |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|  |  | **second** | second | **second** |  |  |
|  | **first** | first | first | first | **first** |  |
| **main** | main | main | main | main | main | **main** |

```markdown
0. JVM에 의해 main 메서드가 호출되며 프로그램 시작
1. main 메서드를 위한 메모리 공간이 할당되며 main 메서드의 코드 수행
2. main 메서드에서 first 메서드 호출
3. main 메서드는 대기상태로 변경하고, first 메서드 메모리 공간 할당 및 코드 수행
4. frist 메서드에서 second 메서드 호출
5. first 메서드는 대기상태로 변경하고, second 메서드 메모리 공간 할당 및 코드 수행
6. second 메서드에서 println 메서드 호출
7. second 메서드는 대기상태로 변경하고, println 메서드 메모리 공간 할당 및 코드 수행
8. println 종료 시 second 메서드로 복귀
9. second 종료 시 first 메서드로 복귀
10. first 종료 시 main 메서드로 복귀
11. main 종료 시 프로그램 종료
```

## Basic and Reference Parameter

Java에서 메서드를 호출할 때 매개변수로 지정한 값을 메서드의 매개변수로 복사해서 넘겨준다. 이 때, 매개변수의 타입이 기본형 일 때는 기본형 값이 목사되겠지만 참조형 일 때는 인스턴스 주소가 복사된다. 즉 매개변수가 기본형이라면 단순히 지정된 값만 얻지만, 참조형이라면 값이 지정된 주소를 알 수 있기 때문에 값을 읽어오고 변경도 가능하다.

> **기본형 매개변수** : read only
  **참조형 매개변수** : read & write

### 기본형 매개변수

```Java
class Data
{
    int x;
}

class PrimitiveParameterEx
{
    public static void main(String[] args)
    {
        Data d = new Data(); // 클래스 Data의 x에 대한 주소를 d에 저장
        d.x = 10; // 클래스 Data의 x에 10을 저장
        System.out.println(d.x); // 10
        
        change(d.x); // 1000
        System.out.println(d.x); // 10
    }
    static void change (int x) // 기본형 매개변수
    {
        // 클래스 Data의 주소를 모르기 때문에 Data의 x가 아닌 change의 x를 만들어서 그 x에 값 저장
        x = 1000;
        System.out.println(x);
    }
}
```
```markdonw
0. 프로그램이 시작되면서 스텍에 main이 적재된다.
1. change 메서드가 호출되면서 스텍에 change를 적재하고, d.x가 change 메서드의 매개변수 x에 복사된다.
2. change 메서드에서 x 값을 1000으로 변경
3. change 메서드가 종료되면서 매개변수 x는 스텍에서 제거된다.
```

### 참조형 매개변수

```Java
class Data
{
    int x;
}

class ReferenceParameterEx
{
    public static void main(String[] args)
    {
        Data d = new Data(); // 클래스 Data의 x에 대한 주소를 d에 저장
        d.x = 10; // 클래스 Data의 x에 10을 저장
        System.out.println(d.x); // 10
        
        change(d); // 1000
        System.out.println(d.x); // 1000
    }
    static void change (Data d) // 참조형 매개변수
    {
        // 클래스 Data의 주소를 매개변수로 받으면서 Data의 x에 접근해서 값 변경 가능
        d.x = 1000; 
        System.out.println(d.x);
    }
}
```
```markdown
0. 프로그램이 시작되면서 스텍에 main이 적재된다.
1. change 메서드가 호출되면서 스텍에 change를 적재하고, 참조변수 d의 값(주소)이 매개변수 d에 복사된다.
2. change 메서드가 매개변수 d에 저장된 주소값으로 x에 접근 가능해진다.
3. change 메서드에서 매개변수 d로 x의 값을 1000으로 변경
4. chagne 메서드가 종료되면서 매개변수 d는 스텍에서 제거된다.
```

## Referential Conversion Type

매개변수 뿐만 아니라 반환 타입도 참조형이 될 수 있다. 반환 타입이 참조형이라는 것은 반환하는 값의 모든 타입이 참조형이 된다는 뜻이다.

```Java
class Data
{
    int x;
}

class ReferenceReturnEx
{
    public static void main(String[] args)
    {
        Data d = new Data();
        d1.x = 10;
        
        Data d2 = copy(d1);
        System.out.println(d1.x + ", " + d2.x); // 10, 10
    }
    static Data copy(Data d)
    {
        Data tmp = new Data()
        tmp.x = d.x;
        
        return tmp;
    }
}
```

```markdown
1. copy 매개변수를 호출하면서 참조변수 d의 값이 매개변수 d에 복사된다.
2. 새로운 객체를 생성한 다음 d.x에 저장된 값을 tmp.x에 복사한다.
3. copy 메서드가 종료되면서 반환한 tmp의 값은 참조변수 d2에 저장된다.
4. copy 메서드가 종료되어 tmp는 사라졌지만 d2로 새로운 객체를 다룰 수 있다. 
```

## Recursive Call

메서드를 내분에서 자신을 다시 호출하는 것을 **재귀호출**이라고 한다.
```Java
void method
{
    method();
}
```

재귀 호출을 사용하면 논리적 간결함을 얻을 수 있다. 몇 겹의 반복문과 조건문으로 구성된 코드 보다는 재귀 호출로 구성된 코드가 보다 단순한 구조가 된다. 다음과 같이 펙토리얼을 구하는 코드를 통해 살펴보자. 펙토리얼을 구하는 수학적 공식은 `f(n) = n * f(n-1), 단 f(1) = 1`

```Java
class Factorial
{
    public static void main(String[] args)
    {
        int result = factorial(4);
        
        System.out.println(result); // 24
    }
    static int factorial (int n)
    {
        int result = 0;
        
        if (n == 1);
        {
            result = 1;
        }
        else
        {
            result = n * factorial(n-1); // 재귀호출
        }
        return resilt;
    }
}
```

```markdown
1. factorial(4)를 호출하면 매개변수 n에 4가 복사된다.
2. 메서드 factorial이 필요에 의해 factorial(3)을 호출한다.
3. 메서드 factorial이 필요에 의해 factorial(2)을 호출한다.
4. 메서드 factorial이 필요에 의해 factorial(1)을 호출한다.
```

## Class Method and Instance Method

변수와 같이 메서드 앞에 static을 붙이면 **클래스 메서드**가 된다. 반대로 static을 붙이지 않으면 **인스턴스 메서드**가 된다.

인스턴스 메서드는 인스턴스 변수와 관련된 작업을 하는 메서드이다. 즉 메서드의 작업을 수행하는데 인스턴스 변수를 필요로 하는 메서드이다. 

클래스 메서드는 인스턴스 변수나 인스턴스 메서드를 사용하지 않는 메서드이다. 

보편적으로 인스턴스 메서드와 클래스 메서드 중 결정하는 방법은 상황들을 고려하면서 결정한다.

```markdown
1. 클래스를 생성할 때, 맴버변수 중 모든 인스턴스에 공통으로 사용하는 것에 static을 붙인다. 
2. 작성한 메서드 중에서 인스턴스 변수나 인스턴스 메서드를 사용하지 않는 메서드라도 호출시간이 짧아야 하거나 높은 성능이 요구되는 메서드에 static을 붙인다. 
```

## Reference and Call between Class Member and Instance Member

같은 클래스에 속한 맴버들 간에는 별도의 인스턴스 생성 없이도 서로 참조와 호출이 가능하다. 단, **클래스 맴버는 존재하지만 인스턴스 맴버는 존재하지 않을 수 있기 때문에 클래스 맴버가 인스턴스 맴버를 참조나 호출하기 위해서는 인스턴스를 생성해야 한다.** 하지만 인스턴스 메서드가 실행된다는 것은 이미 인스턴스 변수가 생성되었다는 것을 의미하기 때문에 인스턴스 맴버 간의 호출에는 아무 문제가 발생하지 않는다. 

```Java
class Ex
{
    void instancemethod() {} // 인스턴스 메서드
    static void staticmethod // 클래스 메서드
    
    void instancemethod_Ex()
    {
        instancemethod(); // 인스턴스 메서드 호출
        staticmethod(); // 클래스 메서드 호출
    }
    
    static void staticmethod_Ex()
    {
        instancemethod(); // 인스턴스 메서드 호출 에러
        staticmethod(); // 클래스 메서드 호출
        
        Ex e = new Ex(); // 인스턴스 생성
        e.instancemethod(); // 인스턴스 생성으로 인해 인스턴스 메서드 호출 성공
    }
}
```

# Overloading

## What is Overloading

메서드도 변수와 마찬가지로 같은 클래스 내에서 서로 구별될 수 있어야 하기 때문에 각자 다른 이름을 가져야한다. **오버로딩**은 한 클래스 내에 같은 이름의 메서드를 여러 개 정의하는 것을 말한다. 즉, 보통 하나의 메서드 이름에 하나의 기능만을 구현해야 하는데 하나의 메서드 이름으로 여러 기능을 구현한다.

## Condition for Overloading

같은 이름의 메서드를 정의한다고 해서 무조건 오버로딩이 되는 것은 아니다. 오버로딩이 성립하기 위해서는 다음과 같은 조건을 만족해야한다.
```markdown
1. 메서드 이름이 같아야 한다.
2. 매개변수의 개수 또는 타입이 달라야한다. 
```

비록 메서드의 이름이 같더라도, 매개변수가 다르면 서로 구별되어 오버로딩이 가능하다. 위의 조건을 만족하지 않는다면 컴파일 시 에러가 발생하낟. 그리고 오버로딩된 메서드들은 매개변수에 의해서만 구별 될 수 있기 때문에 **반환 타입은 오버로딩을 구현하는데 아무런 영향을 주지 못한다.**

## Example of Overloading

Java에서 제공하는 메서드 중 println은 대표적인 오버로딩의 예시가 된다. 사용자가 println을 사용할 때는 어떤 입력값을 주어도 화면에 출력하는데 어려움이 없었다. 하지만 실제로는 println 메서드를 호출할 때 매개변수로 지정하는 값의 타입에 따라서 호출되는 println 메서드가 달라진다. println이 포함되어있는 PrintStream 클래스는 다음과 같이 구성되어 있다.
```Java
class PrintStream
{
    void println()
    void println(boolean x)
    void println(char x)
    void println(char[] x)
    void println(double x)
    void println(float x)
    void println(int x)
    void println(long x)
    void println(Object x)
    void println(String x)
}
```

PrintStream에 있는 println들은 모두 이름은 같지만 매개변수의 타입이 모두 다르기 때문에 오버로딩이 해당한다.

```Java
class math
{
    int add(int a, int b) {return a+b;}
    int add(int x, int y) {return x+y;}
}
```

하지만 위와 같이 메서드의 이름이 같지만 매개변수의 타입도 같다면 이는 오버로딩에 해당하지 않아 에러가 발생한다. 즉 매개변수의 이름은 오버로딩에 영향을 주지 않는다. 다음과 같이 매개변수의 수나 타입을 다르게 만들어야 에러가 발생하지 않는다.

```Java
class math
{
    int add(int a, int b) {return a+b;}
    int add(int a, int b, int c) {return a+b+c;}
    long add(long a, long b) {return a+b;}
}
```

## Advantage of Overloading

이러한 오버로딩을 사용하면 다음과 같은 이점을 얻을 수 있다.
```markdown
1. 기능에 비해 외워야하는 명령어 이름이 줄어든다.
2. 매서드의 이름을 짓는 고민을 줄일 수 있다. 
3. 이름의 종류가 줄어들어 하나의 이름으로 그 명령어의 작업 종류를 예측할 수 있다.
```

## Variable Factor and Overloading

기존 Java에서는 매개변수의 개수를 고정적으로 사용해야 했다. 하지만 JDK1.5 이후로부터는 동적으로 매개변수를 설정할 수 있는 **가변인자**가 추가되었다. 가변인자는 다음과 같이 `타입...변수명`으로 지정한다.

```Java
class Ex
{
    public static void main(String[] args)
    {
        System.out.printf(Overloading("a")) // a
        System.out.printf(Overloading("a", "b")) // ab
        System.out.printf(Overloading("a", "b", "c")) // abc
    }
    
    static String Overloading(String...str)
    {
        return Overloading("", str);
    }
}
```

# Generator

## What is Generator

**생성자**는 인스턴스가 생성될 때 호출되는 '인스턴스 초기화 매서드'이다. 즉 인스턴스 변수의 초기화 작업에 주로 사용된다. 생성자도 메서드처럼 클래스 내에 선언되고, 구조도 return이 없는 메서드와 동일하다. 생성자의 조건은 다음과 같다.
```markdown
1. 생성자의 이름은 클래스의 이름과 같아야 한다.
2. 생성자는 리턴 값이 없어야 한다.
```

생성자는 다음과 같이 정의하낟. 생성자도 오버로딩이 가능하기 때문에 하나의 클래서의 여러 생성자가 존재할 수 있다. 
```Java
class CLASS_NAME
{
    CLASS_NAME() // 매개변수가 있다면 매개변수를 포함한다.
    {
        // 인스턴스 생성 시 수행할 코드
        // 인스턴스 변수 초기화 코드
    }
}
```

그동안 인스턴스를 생성하기 위해 `name n = new name()`의 코드를 사용했다. 여기서 name()이 생성자이다.  `name n = new name()`코드를 통해 name 클래스의 인스턴스를 생성하는 과정을 단계별로 나누어 보면 다음과 같다.
```markdown
1. 연산자 new에 의해 heap 메모리에 name 클래스의 인스턴스가 생성된다.
2. 생성자 name()이 호출되어 수행된다.
3. 연산자 new의 결과로 생성된 name 인스턴스의 주소가 반환되어 참조변수 n에 저장된다.
```

즉 모든 클래스에는 반드시 하나 이상의 생성자가 정의되어 있어야한다. 

## Default Constructor

지금까지 코드를 구성할 때 클래스 내에 생성자를 정의하지 않았지만 코드는 정상적으로 작동되었다. 이는 컴파일러가 제공하는 **기본 생성자** 덕분이다. 컴파일 할 때, 클래스에 생성자가 하나도 정의되지 않은 경우 컴파일러는 자동적으로 기본 생성자를 추가하여 컴파일한다. 

컴파일러가 추가해주는 기본 생성자는 매개변수와 내용이 없는 아주 간단한 구조로 되어있다. 따라서 특별한 초기화 작업이 필요하지 않는 코드의 경우 생성자를 정의하지 않고, 기본 생성자를 사용해도 된다.

## Generator with Parameter

생성자도 메서드처럼 매개변수를 선언하고, 호출 시 값을 넘겨받아서 인스턴스의 초기화 작업에 사용할 수 있다. 다음과 같이 Car 인스턴스와 Car() 생성자를 정의해 보자.
```Java
class Car
{
    String color;
    String gearType;
    int door;
    
    Car() {} // 생성자
    Car(String c, String g, int d) // 생성자
    {
        color = c;
        gearType = g;
        door = d;
    }
}
```

Car 인스턴스를 생성할 때, 생성자 `Car()`을 사용하면 인스턴스를 생성한 다음에 인스턴스 변수들을 따로 초기화해야 한다. 하지만 생성자 `Car(String c, String g, int d)`을 사용하면 인스턴스를 생성하는 동시에 원하는 값으로 초기화할 수 있다. 

## Call Another Constructor from Constructor

다음의 조건을 만족시키면 생성자 간에도 서로 호출이 가능하다.
```markdown
1. 생성자 내에 자신을 사용할 때는 생성자의 이름으로 this를 사용한다.
2. 한 생성자에서 다른 생성자를 호출할 때는 반드시 첫 줄에서만 호출이 가능하다.
```

```Java
class Ex()
{
    Ex() {}
    Example()
    {
        Ex(); // 다른 생성자를 호출할 때는 첫 번째 줄에 호출한다.
        this(); // 자신을 호출할 때는 이름 대신 this를 사용한다.
    }
}
```

this를 통해 다음과 같이 생성자를 간단하게 표기할 수 있다.
```Java
Car()
{
   color = "white";
   gearType = "auto";
   door = 4;
}
```
```Java
Car()
{
   this("white", "auto", 4);
}
```

this를 통해 다음과 같이 매개변수와 인스턴스 변수간의 이름 구별을 통해 가독성을 높일 수 있다.
```Java
Car(String c, String g, int d)
{
    color = c;
    gearType = g;
    door = d;
}
```

```Java
Car(String color, String gearType, int door)
{
    this.color = color;
    this.gearType = gearType;
    this.door = door;
}
```


## Copy Instance Using the Constructor

생성자를 사용해서 현재 사용하고 있는 인스턴스와 같은 상태(인스턴스의 모든 인스턴스 변수가 동일한 값을 갖는 상태)를 갖는 인스턴스를 하나 더 생성할 수 있다. 생성자를 통한 복제는 다음과 같이 진행된다. 

```Java
class Car
{
    String color;
    String gearType;
    door = door;
    
    Car() // 인스턴스 초기화를 위한 생성자
    {
        this("white", "auto", 4);
    }
    
    Car(Car c) // 인스턴스 복제를 위한 생성자
    {
        this(c.color, c.gearType, c.door);
    }
    
    Car(String color, String gearType, int door) // 매개변수를 통한 초기화를 위한 생성자
    {
        this.color = color;
        this.gearType = gearType;
        this.door = door;
    }
    
class Ex
{
    public static void main (String[] args)
    {
        Car c1 = new Car();
        Car c2 = new Car(c1); // c1의 복사본 c2를 생성한다
        
        System.out.println(c1.color + ", " + c1.gearType + ", " + c1.door); // white, auto, 4
        System.out.println(c2.color + ", " + c2.gearType + ", " + c2.door); // white, auto, 4
        
        c1.door = 100;
        
        System.out.println(c1.color + "," + c1.gearType + "," + c1.door); // white, auto, 100
        System.out.println(c2.color + "," + c2.gearType + "," + c2.door); // white, auto, 4
    }
}
}
```

# Initialize Variable

## Initialize Variables

변수를 선언하고 처음으로 값을 저장하는 것을 **변수 초기화**라고 한다. 맴버변수는 초기화를 진행하지 않아도 자동적으로 적절한 기본값으로 초기화가 이루어지기 때문에 변수 초기화를 진행하지 않아도 된다. 하지만 지역 변수는 사용하기 전에 반드시 초기화를 진행해야한다. 각 타입의 기본값은 다음과 같다.

| 자료형 | 기본값 | 
|:-:|:-:|
| boolean | false |
| char | '\u0000' |
| byte, short, int | 0 |
| long | 0L |
| float | 0.0f |
| double | 0.0d |
| 참조 변수 | null |

지역 변수 초기화는 위와 같은 기본값이나 사용자가 원하는 값으로 진행하면 된다. 하지만 맴버 변수의 초기화는 다음과 같은 명시적 초기화, 생성자, 초기화 블록을 사용해야 한다.

## Explicit Initialization

변수를 선언과 동시에 초기화하는 방법을 명시적 초기화라고 한다. 다장 기본적이면서도 간단한 초기화 방법으로 다음과 같이 진행한다.
```Java
class Car
{
    int door = 4; // 기본형 변수의 초기화
    Engine e = new Engine(); // 참조현 변수의 초기화
}
```

간단한 초기화는 명시적 초기화로도 가능하지만 복잡한 초기화는 초기화 블록을 사용해야한다.

## Initialization Block

**초기화 블록**에는 클래스 초기화 블록과 인스턴스 초기화 블록이 있다.
> **클래스 초기화 블록** : 클래스변수의 복잡한 초기화의 사용      
  **인스턴스 초기화 블록** : 인스턴스 변수의 복잡한 초기화에 사용
  
초기화 블록은 다음과 같이 작성한다.
```Java
class InitBlock
{
    static { // 클래스 초기화 블록 }
    
    { //인스턴스 초기화 블록 }
}
```

위와 같이 초기화 블록은 클래스 내에 만들고 {}안에 코드를 작성하면 된다. 인스턴스 초기화 블록은 그냥 작성하고, 클래스 초기화 블록은 static을 앞에 작성한다. 초기화 블록 내에는 조건문, 반복문, 예외처리구문 등을 사용할 수 있어서 복잡한 초기화도 가능해 진다. 

## Initialization of Member Variable

지금까지 알아본 맴버변수를 초기화하는 방법은 다음과 같은 시기에 사용되고, 다음과 같은 순서로 진행된다.

### 클래스 변수
**초기화 시점** : 클래스가 처음 로딩될 때 단 한번 초기화
**초기화 순서** : 기본값 -> 명시적 초기화 -> 클래스 초기화 블록

### 인스턴스 변수
**초기화 시점** : 인스턴스가 생성될 때마다 각 인스턴스별로 초기화
**초기화 순서** : 기본값 -> 명시적 초기화 -> 인스턴스 초기화 블록 -> 생성자

다음 코드를 통해 초기화 과정을 살펴본다.
```Java
class InitEx
{
    // 명시적 초기화
    static int cv = 1; 
    int iv = 1;
    
    static { cv = 2; } // 클래스 초기화 블록
    { iv = 2; } // 인스턴스 초기화 블록
    
    InitEx() { iv = 3; } // 생성자
}

```
|  | 기본값 | 명시적 초기화 | 클래스 초기화 블록 | 기본값 | 명시적 초기화 | 인스턴스 초기화 블록 | 생성자 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| cv | 0 | 1 | 2 | 2 | 2 | 2 | 2 |
| iv |  |  |  | 0 | 1 | 2 | 3 |

```markdown
1. cv가 메모리의 메서드 영역에 생성되고, cv는 int형 기본값 0으로 초기화
2. 명시적 초기화에 의해 cv=1
3. 클래스 초기화 블록에 의해 cv=2
4. InitEx 클래스의 인스턴스가 생성되며 iv가 메모리의 힙 영역에 생성하고, itn형 기본값 0으로 초기화
5. 명시적 초기화에 의해 iv=1
6. 인스턴스 초기화 블록에 의해 iv=2
7. 생성자에 의해 iv=3
```
