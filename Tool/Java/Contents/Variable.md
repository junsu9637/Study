[1. 변수와 상수](#variables-and-constants)               
[1.1 변수란](#what-is-variables)          
[1.2 변수의 선언과 초기화](#declaration-and-initialization-of-variables)        
[1.3 변수의 명명규칙](#naming-rules-for-variables)

[2. 변수의 타입](#type-of-variable)               
[2.1 기본형](#fundamental-form)
[2.2 상수와 리터럴](#constant-and-literal)
[2.3 형식화된 출력](#formatted-output)
[2.4 입력받기](#receive-inputs)

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

'변수'란 *단 하나의 값을 저장할 수 있는 메모리상의 공간*을 의미한다. 단 하나의 값을 저장할 수 있기 때문에 새로운 값을 저장하면 기존의 값은 사라진다.

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

2. 변수의 타입(#type-of-variable)               
2.1 기본형(#fundamental-form)
2.2 상수와 리터럴(#constant-and-literal)
2.3 형식화된 출력(#formatted-output)
2.4 입력받기(#receive-inputs)

3. 진법(#system)               
3.1 10진법과 2진법(#decimal-and-binary)
3.2 비트와 바이트(#bit-and-byte)
3.3 8진법과 16진법(#octal-and-hexadecimal)
3.4 정수의 진법 변환(#genetic-transformation-of-integers)
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










