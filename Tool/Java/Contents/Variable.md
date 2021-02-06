[1. 변수와 상수](#variables-and-constants)               
[1.1 변수란](#what-is-variables)          
[1.2 변수의 선언과 초기화](#declaration-and-initialization-of-variables)        
[1.3 변수의 명명규칙](#naming-rules-for-variables)

[2. 변수의 타입](#type-of-variable)               
[2.1 기본형](#fundamental-form)           
[2.2 상수와 리터럴](#constant-and-literal)             
[2.3 형식화된 출력](#formatted-output)                         

[3. 진법](#system)               
[3.1 10진법과 2진법](#decimal-and-binary)        
[3.2 비트와 바이트](#bit-and-byte)              
[3.3 8진법과 16진법](#octal-and-hexadecimal)            
[3.4 정수의 진법 변환](#genetic-transformation-of-integers)            
[3.5 실수의 진법 변환](#genetic-transformation-of-real-number)             
[3.6 음수의 2진 표현](#negative-binary-representation)                

[4. 기본형](#fundamental-form)               
[4.1 논리형](#logical-type)            
[4.2 문자형](#character-type)             
[4.3 정수형](#integer-type)                 
[4.4 실수형](#real-number-type)                

[5. 형변환](#shape-conversion)              
[5.1 형변환이란](#what-is-shape-conversion)             
[5.2 형변환 방법](#shape-conversion-method)           
[5.3 정수형 간의 형변환](#transform-between-integers)            
[5.4 실수형 간의 형변환](#transform-between-real-number)               
[5.5 정수형과 실수형 간의 형변환](#transform-between-integers-real-number)               
[5.6 자동 형변환](Automatic-transformation)           

# Variables and Constants

## What is Variables

**변수**란 단 하나의 값을 저장할 수 있는 메모리상의 공간을 의미한다. 단 하나의 값을 저장할 수 있기 때문에 새로운 값을 저장하면 기존의 값은 사라진다.

## Declaration and Initialization of Variables

**변수 선언**
```Java
int age; //age라는 이름의 int 타입 변수를 선언
```

변수를 선언하면, 메모리의 빈 공간에 **'변수타입'** 에 알맞는 크기의 저장공간이 확보되고, 이 저장공간은 **'변수이름'** 을 통해 사용 가능하다.

**변수 초기화**
```Java
int age = 22; //age라는 이름의 int 타입 변수를 선언하고, 25로 초기화
```

'변수 초기화'란 *변수를 사용하기 전에 처음으로 값을 저장*하는 것을 의미한다. 

**변수 값 교환**

다음과 같은 과정으로 두 변수의 값을 교환한다고 해보자.

```markdown
1. x=10, y=20
2. x=y
3. y=x
```

> 2번 과정에서 x=y=20이 된다.          
  3번 과정을 진행하더라고 x=y=20이 된다.       
  
위 과정을 진행하더라도 우리가 원하는 결과인 x=20, y=10이 반환되지 않는다. 이러한 결과를 얻기 위해서는 다음과 같이 임시 저장소를 사용해야한다.
```markdown
1. x=10, y=20, tmp 선언
2. tmp=x
3. x=y
4. y=tmp
```

> 2번 과정에서 tmp=10이 된다.            
  3번 과정에서 x=20이 된다.            
  4번 과정에서 y=10이 된다.       

## Naming Rules for Variables

'변수의 이름'과 같은 프로그래밍에서 사용하는 모든 이름을 **'Identifier(식별자)'** 라고 부른다. 즉 모든 이름은 같은 영역 내에서 서로 구분될 수 있어야 한다. 식별자를 만들 때는 다음과 같은 규칙을 지켜야 한다.
```markdown
1. 대소문자가 구분되며 길이에 제한은 없다
2. 예약어를 사용해서는 안된다.
3. 숫자로 시작해서는 안된다.
4. 특수문자는 '\_'와 '$'만 허용된다.
```

그리고 필수 사항은 아니지만 프로그래머들에게 권장하는 규칙들은 다음과 같다. ~~안지키면 위에서 안좋아함~~
```markdown
1. 클래스 이름의 첫 글자는 항상 대문자로 한다.
2. 여러 단어로 이루어진 이름은 단어의 첫 글자를 대문자로 한다.
3. 상수의 이름은 모두 대문자로 한다.
4. 상수의 이름이 여러 단어로 이루어진 경우 -\_'로 구분한다.
5. 이름은 그 객체의 특성을 잘 나타내는 이름으로 작성한다 
```

# Type of Variable

우리가 사용하는 '값'은 '문자'와 '숫자'로 나눌 수 있다. 그리고 숫자는 '정수'와 '실수'로 나눌 수 있다. 

자료형은 크게 **기본형**과 **참조형**으로 나눌 수 있다.   
> **기본형 변수** : 실제 값을 저장        
  *논리형, 문자형, 정수형, 실수형*
  **참조형 변수** : 값이 저장되어 있는 메모리 주소 저장 

참조형 변수를 선언할 때는 변수의 타입으로 클래스의 이름을 사용한다. 즉 클래스의 이름이 참조형 변수의 타입이 되고, 새로운 클래스를 작성한다는 것은 새로운 참조형을 추가하는 것과 같다. 참조형 변수를 선언하는 방법은 다음과 같다.

```Java
Date today = new Date() // Date 객체를 생성하고, 그 주소를 today에 저장
```

위 코드는 Date 클래스 타입의 참조형 변수 today를 선언한 것이다. new는 객체를 생성하는 연산자로 객체의 주소를 만들어 낸다. new가 만들어낸 주소가 '='를 통해 참조형 변수 today에 저장되는 것이다. 

## Fundamental form

기본형에는 총 8개의 자료형이 있다. 이 자료형은 크게 **논리형**, **문자형**, **정수형**, **실수형**으로 구분된다. 

> 논리형 : boolean       
  문자형 : char             
  정수형 : int, byte, short, long          
  실수형 : float, double          
  
  
boolean을 제외한 나머지 7개의 기본형은 서로 연산과 변환이 가능하다. 각 타입마다 저장할 수 있는 값의 범위가 다르다. 정수의 경우 가장 많이 사용되므로 4가지의 타입이 있지만, 일반적으로 CPU가 가장 효율적으로 처리할 수 잇는 int 타입으로 지정한다. 각 기본형이 저장할 수 있는 값의 범위는 다음과 같다.

| | 1 byte | 2 byte | 4 byte | 8 byte |
|:-:|:-:|:-:|:-:|:-:|
| 논리형 | boolean | | | |
| 문자형 | | char | | |
| 정수형 | byte | short | int | long |
| 실수형 | | | float | double |

## Constant and Literal

### 상수

**상수**는 변수와 마찬가지로 '값을 저장할 수 있는 공간'이지만, 변수와는 달리 한 번 값을 저장하면 다른 값으로 변경할 수 없다. 상수를 선언하는 방법은 변수와 동일하며, 변수 타입 앞에 'final'을 붙여주면 된다. 선언 코드는 다음과 같다.

```Java
final int age = 22;
final int height; // error : 초기화 없이 상수 선언만 진행함
```

상수는 변수와는 다르에 선언과 동시에 초기화해야 한다.

### 리터럴

리터럴은 상수 값 다른 이름이다. 변수, 상수, 리터럴의 정의를 비교하면 다음과 같다.

> **변수** : 하나의 값을 저장하기 위한 공간
  **상수** : 값을 한 번만 저장할 수 있는 공간
  **리터럴** : 상수나 변수 값 자체
  
```Java
int year = 2021;
final int age = 22;
```

위 코드에서 year은 변수, age는 상수, 2021과 22는 리터럴에 해당한다.

#### 문자 리터럴과 문자형 리터럴

문자를 ''로 감싼 것은 **문자 리터럴**이라고 하고, 문자를 ""로 감싼 것을 **문자열 리터럴**이라고 한다. 하나의 문자를 저장할 때는 char 타입의 변수를 선언해야 하고, 여러 문자열을 저장하고 위해서는 String 타입의 변수를 선언해야한다. 이때 문자 리터럴과 문자열 리터럴을 구분해야한다. 

```Java
char ch = 'J'
String name = "Java";
char ch = ''; //error ''안에 반드시 하나의 문자 필요
char ch = ' ';  // 빈 문자
String str = "" // 빈 문자열
```

String은 원래 클래스이기 때문에 new를 사용해서 객체를 생성하는 것이 가능하다.
```Java
String name = new String("Java");
```

그리고 덧셈 연산자를 이용해서 문자열을 결합할 수 있다.
```Java
String name = "Ja" + "va"; // name = "Java"
String str = name + 8.0; // str = "Java8.0"
```

## Formatted Output

화면에 값을 출력하는 방법은 여러가지가 있다.
```Java
System.out.println(3.141592); // 3.141592
System.out.printf(3.141592); //3.14
System.out.printf("3.3f",3.141592); //003.141
System.out.printf("age : %d", 22); // age : 22
```

> **println**          
  자동으로 줄 바꿈           
  값의 모든 내용 출력         
  **printf**    
  %n을 사용해서 강제로 줄바꿈         
  값의 소수점 자리 조절 가능          
  지시자 사용 가능
  
printf()의 지시자 중에서 자주 사용되는 것은 다음과 같다.

| 지시자 | 설명 |
|:-:|:-:|
| %b | boolean 형식으로 출력 |
| %d | 10진 정수의 형식으로 출력 |
| %c | 문자 형식으로 출력 |
| %s | 문자열 형식으로 출력 |
| %f | 부동 소수점 형식으로 출력 |
| %e | 지수 표현식의 형식으로 출력 |
  
# System     

## Decimal and Binary

우리는 일상생활에서 10진법을 주로 사용한다. 1946년에 개발된 ENIAC 역시 10진법을 사용하도록 설계되었다. 하지만 전기회로는 전압이 불안정해서 전압을 10단계로 나누어 처리하는데 한계가 존재했다. 따라서 1950년에 개발된 EDVAC부터 0과 1의 2진법을 사용하는 컴퓨터가 개발되었다. 

2진법은 0과 1로만 데이터를 표현하기 때문에 10진법보다 많은 자리수를 필요로 한다. 

## Bit and Byte

한 자리의 2진수를 **bit**라고 하고, **byte**는 컴퓨터가 값을 저장할 수 있는 최소단위로 8bit에 해당한다. 그리고 **word**라는 단위도 있는데 이는 CPU가 한 번에 처리할 수 있는 데이터의 크기를 의미하며 컴퓨팅 환경에 따라 1word = 4byte, 1word = 8byte로 다양하다.

## Octal and Hexadecimal

2진법으로 값을 표현하면 자리수가 길어진다는 단점이 있다. 이러한 단점을 보완하기 위햇 8진법이나 16진법을 사용한다. 8진수는 2진수 3자리를 한 자리로 표현하고, 16진수는 2진수 4자리를 한 자리로 표현할 수 있다. 이로 인해 자리수가 짧이져서 알아보기 쉽고 서로 간의 변환방법 또한 간단하다. 

### 2진수를 8진수, 16진수로 변환
| 2진수 | 8진수 | 2진수 | 16진수 |
|:-:|:-:|:-:|:-:|
| 000 | 0 | 0000 | 0 |
| 001 | 1 | 0001 | 1 |
| 010 | 2 | 0010 | 2 |
| 011 | 3 | 0011 | 3 |
| 100 | 4 | 0100 | 4 |
| 101 | 5 | 0101 | 5 |
| 110 | 6 | 0110 | 6 |
| 111 | 7 | 0111 | 7 |
|  |  | 1000 | 8 |
|  |  | 1001 | 9 |
|  |  | 1010 | A |
|  |  | 1011 | B |
|  |  | 1100 | C |
|  |  | 1101 | D |
|  |  | 1110 | E |
|  |  | 1111 | F |

## Genetic Transformation of Integers

### 10진수를 n진수로 변환

10진수를 다른 진수로 변환
```markdown
1. 해당 진수(n)으로 나누고 옆에 나머지를 기록한다.
2. 위 과정을 더 이상 나눌 수 없을 때까지 반복한다.
3. 몫과 나머지를 아래부터 위로 순서대로 적는다.
```

예를 들어 800를 8진수로 변환하면 다음과 같다.
```markdown
800 / 8 = 100 + 0
100 / 8 = 12 + 2
12 / 8 = 1 + 4

800(10) -> 1420(8)
```

### n진수를 10진수로 변환

n진수를 10진수로 변환하기 위해서는 각 자리의 수에 해당하는 단위의 값을 곱해서 모두 더하면 된다.

예를 들어 8진수 1420을 10진수로 변환하면 다음과 같다.
```markdown
1\*8<sup>3</sup>
```

3.5 실수의 진법 변환(#genetic-transformation-of-real-number)
3.6 음수의 2진 표현(#negative-binary-representation)

4. 기본형(#fundamental-form)               
4.1 논리형(#logical-type)
4.2 문자형(#character-type)
4.3 정수형(#integer-type)
4.4 실수형(#real-number-type)

5. 형변환(#shape-conversion)              
5.1 형변환이란(#what-is-shape-conversion)
5.2 형변환 방법(#shape-conversion-method)
5.3 정수형 간의 형변환(#transform-between-integers)
5.4 실수형 간의 형변환(#transform-between-real-number)
5.5 정수형과 실수형 간의 형변환(#transform-between-integers-real-number)
5.6 자동 형변환(Automatic-transformation)










