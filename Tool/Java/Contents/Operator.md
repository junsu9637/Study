[1. 연산자](#operator)            
[1.1 연산자와 피연산자](#operator-and-operand)              
[1.2 식과 대입연산자](#expression-and-substitution-operator)             
[1.3 연산자의 종류](#type-of-operator)               
[1.4 연산자의 우선순위와 결합규칙](#priority-and-combination-rules-for-operator)               
[1.5 산술 변환](#usual-arithmetic-conversion)             

[2. 다항 연산자](#polynomial-operator)            
[2.1 증감 연산자](#increasing-and-decreasing-operators)             
[2.2 부호 연산자](#sign-operator)             

[3. 산술 연산자](#arithmetic-operators)            
[3.1 사칙 연산자](#four-pronged-operator)           
[3.2 나머지 연산자](#other-operator)             

[4. 비교 연산자](#comparison-operators)               
[4.1 대소비교 연산자](#consumption-bridge-operator)             
[4.2 등가비교 연산자](#equivalent-comparison-operator)             

[5. 논리 연산자](#logical-operator)           
[5.1 논리 연산자](#logical-operators)            
[5.2 비트 연산자](#bit-operator)            

[6. 그 외의 연산자](#the-other-operator)           
[6.1 조건 연산자](#condition-operators)             
[6.2 대입 연산자](#substitution-operator)          


# Operator

## Operator and Operand

> **연산자** : 연산을 수행하는 기호(사칙연산 등)          
  **피연산자** : 연산자의 작업 대상(변수, 상수, 리터럴, 수식 등)

연산자는 피연산자로 연산을 수행하고 나면 항상 결과값을 반환한다.

## Expression and Substitution Operator

연산자와 피연산자를 조합하여 계산하고자하는 바를 표현한 것을 **식**이라고 한다. 그리고 식을 계산하여 결과를 얻는 것을 **평가**한다고 한다.

## Type of Operator

연산자는 연산자의 우선순위로 인해 연산자의 기능과 피연산자의 개수에 의해 분류해야 한다. 

### 연산자의 기능에 의한 분류 

연산자를 기능별로 분류하면 다음과 같다.
| 종류 | 연산자 | 설명 |
|:-:|:-:|:-:|
| 산술 연산자 | +, -, \*, /, %, <<, >> | 사칙연산과 나머지  |
| 비교 연산자 | >, <, >=, <=, ==, != | 크고 작음과 같고 다름을 비교 |
| 논리 연산자 | &&, \|\|, !, &, \|, ^, ~  | AND, OR으로 조건을 연결 |
| 대입 연산자 | = | 우변의 값을 좌변에 저장 |
| 기타 | (type), ?:, instanceof | 형변형 연산자, 삼항 연산자, instanceof 연산자 |

### 피연산자의 개수에 의한 분류

피연산자의 개수로 연산자를 분류하기도 한다. 피연산자가 하나면 '단항 연산자', 피연산자가 두 개면 '이항 연산자'. 피연산자가 세 개면 '삼항 연산자'라고 부른다. 대부분의 연산자는 '이항 연산자'이고, '삼항 연산자'는 오직 '?',':'뿐이다.

## Priority and Combination-Rules for Operator

### 연산자의 우선순위

연산자의 우선순위는 다음과 같다. `단항 연산자 > 이항 연산자`, `산술(곱셈 > 덧셈 > 쉬프트) > 비교 > 논리 > 대입`
```markdown
1. 단항 연산자가 이항 연산자보다 우선순위가 높다.
-x > 3
2. 곱셈과 나눗셈이 덧셈과 뺄셈보다 우선순위가 높다.
x + 3 * y
3. 덧셈과 뺄셈이 쉬프트보다 우선순위가 높다.
x << 2 + 1
4. 비교 연산자보다 산술 연산자가 먼저 수행된다.
x + 3 > y - 2
5. 논리 연산자보다 비교 연산자가 먼저 수행된다.
x > 3 && x < 5
6. 대입 연산자는 연산자 중에서 우선순위가 제일 낮다.
result = x + y * 3;
```

### 연산자의 결합규칙

우선순위가 같은 연산자를 결합하는 방법을 **연산자의 결합규칙**이라고 한다. 결합규칙은 연산자마다 다르고, 다음과 같이 진행된다.
```markdown
1. 왼쪽에서 오른쪽
1 + 2 = 3
2. 오른쪽에서 왼쪽
x = y = 3
```

연산자의 우선순위와 결합규칙을 정리하면 다음과 같다.(위에 위치할수록 우선순위가 높음)
| 종류 | 결합규칙 | 연산자 |
|:-:|:-:|:-:|
| 다항 연산자 | <-- | ++, --, +, -, ~, !, (type) |
| 산술 연산자 | --> | \*, /, % |
| 산술 연산자 | --> | +, - |
| 산술 연산자 | --> | <<, >> |
| 비교 연산자 | --> | <, >, <=, >= instanceof |
| 비교 연산자 | --> | ==, != |
| 논리 연산자 | --> | & |
| 논리 연산자 | --> | ^ |
| 논리 연산자 | --> | \| |
| 논리 연산자 | --> | && |
| 논리 연산자 | --> | \|\| |
| 삼항 연산자 | --> | ?: |
| 대입 연산자 | <-- | =, +=, -=, \*=, /=, %=, <<=, >>=, &=, ^=, \|= |

## Usual Arithmetic Conversion

**산술 변환**은 연산 수행 직전에 발생하는 피연산자의 자동 형변환을 의미한다. 산술 변환은 다음과 같은 규칙을 따른다.
```markdown
1. 두 피연산자의 타입을 같게 일치한다. 
2. 피연산자의 타입이 int보다 작은 타입이면 int로 변환한다.
```

# Polynomial Operator

**단항 연산자**에는 '증감 연산자'와 '부호 연산자'가 있다.

## Increasing and Decreasing Operators

**증가 연산자(++)** 는 피연산자의 값을 1 증가시킨다. 그리고 **감소 연산자(--)** 는 피연산자의 값을 1 감소시킨다.

증감 연산자는 연산자의 위치에 따라 **전위형**과 **후위형**으로 나눠지며 다음과 같이 결과가 나눠진다.

| 타입 | 설명 | 사용 예 |
|:-:|:-:|:-:|
| 전위형 | 값이 참조되기 전에 연산 | j = ++i; |
| 후위형 | 값이 참조된 후에 연산 | j = i++; |

```Java
int i=5, j=0;

j = i++; // a
j = ++i; // b
```

```markdown
a의 경우
1. i의 값을 1 증가 (i=6)
2. i의 값을 참조 (i=6)
3. 연산결과를 j에 저장 (j=6)

b의 경우
1. i의 값을 참조 (i=5)
2. 연산결과를 j에 저장 (j=5)
3. i의 값을 1 증가 (i=6)
```

이러한 증감연산자는 최소화하는 것이 좋고, 식에 두 번 이상 포함된 변수에 증감연산자를 사용하는 것은 피해야한다.

## Sign Operator

**부호 연산자(-)** 는 피연산자의 부호를 반대로 변경한 결과를 반환한다. **부호 연산자(+)** 는 하는 일이 없고, 쓰는 경우가 거의 없다. 

# Arithmetic Operators

**산술 연산자**에는 '사칙 연산자'와 '나머지 연산자'가 있다.


## Four-Pronged Operator

**사칙 연산자**는 +, -, \*, /가 존재한다. 하지만 이런 부호를 그냥 사용하는 경우 앞서 언급한 산술 변환에 의해 오류가 발생할 수 있다. 

```Java
class OperatorEx{
   public static void main(String[] args)
   {
      byte a = 10;
      byte b = 20;
      byte c = a + b;
   }
}
```

위 코드는 실행하면 에러가 발생한다. 그 이유는 앞서 언급한 바와 같이 산술 변환에 의해 '+' 연산을 진행 할 때, 두 개의 피연산자들의 자료형을 int 형으로 변환한 다음 연산을 수행하기 때문이다. 따라서 'a+b'의 타입이 int 타입이기 때문에 위 코드의 오류를 제거하기 위해서는 'a+b'를 byte 타입으로 변환해야 한다. 

위와 같은 상황에서는 리터럴의 값이 작기 때문에 문제가 생기지 않았지만 int 타입에서 크기가 작은 byte 타입으로 변환하는 과정에서 값이 변형되는 문제가 발생할 수 있으므로 타입을 설정할 때는 적절한 타입으로 설정해서 오버플로우를 방지하는 것이 중요하다.

### 문자형

다음과 같은 상황에서는 에러가 발생하지 않는다.
```Java
class OperatorEx1{
   public static void main(String[] args)
   {
      char a = 'a';
      char b = 'b';
      System.out.printf("'%c'", b-a);
   }
}
```

위 코드를 실행하면 3이라는 값이 출력된다. 이렇게 3이 출력되는 이유는 문자의 유니코드와 관련이 있다. 문자 'b'는 유니코드로 변환하면 100이고, 문자 'a'는 유니코드로 변환하면 97이 된다. char 타입은 메모리에 문자 그대로 저장하는 것이 아니라 유니코드의 형태로 저장한다. 따라서 **문자에 사칙 연산자를 사용하면 유니코드의 연산 결과가 출력된다.** 

하지만 아래 코드를 작동시키면 에러가 발행한다.
```Java
class OperatorEx2{
   public static void main(String[] args)
   {
      char c1 = 'a';
      char c2 = c1 + 1;
      System.out.printf(c2); // error
      char c2 = (char)(c2 + 1);
      System.out.printf(c2); // b
   }
}
```

이런 에러가 발생하는 이유는 'a'+1이 리터럴 간의 연산이기 때문이다. 상수 또는 리터럴 간의 연산은 실행 과정동안 변하는 값이 아니기 때문에 컴파일 시 컴파일러가 계산하여 그 결과로 대체함으로써 코드를 보다 효율적으로 만든다. 즉 `char c2 = c1 + 1`은 `char c2 = 'a' + 1`이 아니라 `char c2 = 97 + 1`이기 때문에 타입이 맞지 않기 때문에 문제가 생긴다. 이러한 문제를 해결하기 위해서는 `char c2 = (char)(c1 + 1)`로 코드를 변경해야 한다. 

이러한 특징들을 고려하면 다음과 같이 연속된 문자를 표현하는 코드도 구현할 수 있다. 

```Java
class OperatorEx3{
   public static void main(String[] args)
   {
      char a = 10;
      char b = 3;
      System.out.printf("'%c'", a/b); // 3
   }
}
```



### 실수형

int 타입 간의 나눗셈은 소숫점 아래 숫자는 버림을 진행하면서 int 값을 출력한다. 이러한 특징은 아래 코드에서 확인할 수 있다.
```Java
class OperatorEx1{
   public static void main(String[] args)
   {
      int c = 10;
      int b = 3;
      for(int i=0; i < 26; i++){ // 블록 안의 문장을 26번 반복
         System.out.print(c++); // 'a'부터 연속된 26개의 문자를 출력(a~z)
   } 
}
```

그리고 다음과 같이 나눗셈 연산자의 성질을 이용해서 실수형 변수의 값의 소수점을 제어할 수 있다. 
```Java
class OperatorEx2{
   public static void main(String[] args)
   {
      float pi = 3.141592f;
      float shortPi = (int)(pi*1000) / 1000f;
         System.out.print(shortPi); // 3.141
   } 
}
```

위 코드에서 변수 shortPi는 연산의 우선순위로 인해 다음과 같은 순서로 연산이 진행된다
```markdown
1. (int)(pi\*1000)/1000f;
2. (int)(3141.592f)/1000f;
3. 3141/1000f;
4. 3.141f
```

이러한 성질을 응용하면 다음과 같이 반올림을 수행하는 코드를 구현할 수 있다.
```Java
class OperatorEx3{
   public static void main(String[] args)
   {
      double pi = 3.141592;
      float shortPi = (int)(pi*1000+0.5) / 1000.0;
         System.out.print(shortPi); // 3.142
   } 
}
```

위 코드는 실수형 예제 2와 거의 유사하지만 shortPi 연산에서 +0.5가 추가된 모습을 보여준다. 이로 인해 다음과 같은 연산이 진행된다.
```markdown
1. (int)(pi\*1000+0.5)/1000.0;
2. (int)(3141.592+0.5)/1000.0;
3. (int)(3142.092)/1000.0
4. 3142/1000.0;
5. 3.142
```
Java에서 이러한 기능을 제공하는 Math.round라는 메서드가 있다. 이 기능을 사용하면 `float shortPi = (int)(pi*1000+0.5) / 1000.0;`를 `float shortPi = Math.round(pi*1000) / 1000.0;`와 같이 표현하면 된다.

## Other Operator

%연산자는 왼쪽의 피연산자를 오른쪽 피연산자로 나누고 난 나머지 값을 결과로 반환하는 연산자이다. 즉 10 % 3의 연산을 진행하면 1이 반환된다. 

# Comparison Operators

**비교 연산자**는 두 피연산자를 비교하는데 사용되는 연산자다. 주로 조건문과 반복문의 조건식에 사용되고, 연산결과는 오직 true와 false 둘 중 하나이다. 

## Consumption Bridge Operator

**대소비교 연산자**는 두 피연산자의 값의 크기를 비교하는 연산자로 **<, >, <=, >=** 가 있다. boolean과 참조형 타입을 제외한 모든 타입에 사용할 수 있다.

## Equivalent Comparison Operator

**등가비교 연산자**는 두 피연산자의 값이 같은지, 다른지를 비교하는 연산자로 **==, !=** 가 있다. 모든 자료형에 사용할 수 있다. 단, 기본형과 참조형 간의 관계처럼 서로 형변환이 불가능한 경우에는 등가비교 연산자를 사용할 수 없다. ~~대입 연산자'='와 등가비교 연산자 '=='를 구분해야한다.~~

[앞 문서의 형변형](https://github.com/junsu9637/Study/blob/main/Tool/Java/Contents/Variable.md#automatic-casting)에서 언급한 바와 같이 float와 double간의 형변형 과정에서 미세한 값의 차이가 발생하기 때문에 이러한 두 타입에 등가비교 연산자를 진행하면 다음과 같은 문제가 발생할 수 있다.

```Java
class OperatorEx{
   public static void main(String[] args)
   {
      float f = 0.1f;
      double d1 = 0.1;
      float d2 = (double)f;
      System.out.print(10.0 == 10.0f); // true
      System.out.print(0.1 == 0.1f); // false
      System.out.print(d1 == f); // false
      System.out.print(d2 == f); // false
      System.out.print(d1 == d2); // true
      System.out.print((float)d1 == f); // true
   } 
}
```

### 문자열

두 문자열을 비교하기 위해서는 '=='가 아니라 **equals()** 라는 메서드를 사용해야한다. 이 메서드는 다음과 같이 사용한다.
```Java
String str = new String("abc")

boolean result = str.equals("abc") // true
```

# Logical Operator

**논리 연산자**는 둘 이상의 조건을 AND, OR을 연결하여 하나의 식으로 표현하기 위해 사용한다. '논리 연산자'와 '비트 연산자'가 있다.

## Logical Operators

**논리 연산자**는 다음과 같다

> **&& (AND)** 피연산자 양쪽 모두 true이어야 true       
  **\|\| (OR)** : 피연산자 중 어느 한 쪽만 true이면 true            
  **! (NOT)** : 논리를 반대로 변환한다.

## Bit Operator

**비트 연산자**는 피연산자를 비트단위로 논리 연산한다. 피연산자를 이진수로 표현했을 때의 각 자리를 아래의 규칙에 따라 연산한다. 피연산자로 실수는 허용하지 않는다.

> & (AND) : 피연산자 중 한 쪽의 값이 1이면, 1을 결과로 반환한다. 그 외에는 0을 반환한다.            
  \| (OR) : 피연산자 양 쪽이 모두 1이어야만 1을 결과로 반환한다. 그 외에는 0을 반환한다.             
  ^ (XOR) : 피연산자의 값이 서로 다를 때만 1을 결과로 반환한다. 그 외에는 0을 반환한다.         
  ~ (NOT) : 비트를 반대로 전환한다. 0은 1로, 1은 0으로 변환한다.   


### 쉬프트 연산자

**쉬프트 연산자**는 2진수로 표현된 피연산자의 각 자리를 오른쪽(>>) 또는 왼쪽(<<)으로 이동하는 연산자이다. 예를 들어 8<<2은 다음과 같은 작업을 수행한다.
```markdown
1. 10진수 8을 2진수로 변환하면 00001000이다(8 bit).
2. <<2로 인해 전체 비트를 왼쪽으로 2자리 이동한다.
3. 00|001000__|와 같이 2개의 공백이 생성된다.
4. 공백에 0을 추가하고, 저장범위를 벗어난 비트는 삭제한다.
00100000
```

# The Other Operator

## Condition Operators

**조건 연산자**는 조건식, 식1, 식2가 필요한 삼항 연산자에 해당한다. 조건식은 다음과 같이 구현한다.
```Java
result = x>y ? x : y;
```

> 조건식이 참이면 x 반환        
  조건식이 거짓이면 y 반환

이러한 조건식을 사용해서 다음과 같이 음수를 양수로 변환하는 코드를 구현할 수 있다.
```Java
class OperatorEx
{
   public static void main(String args[])
   {
      int x = 10;
      TransformX = x>=0 ? x : -x 
   }
}
```

## Substitution Operator

**대입 연산자**는 변수와 같은 저장공간에 값 또는 수식의 연산결과를 저장하는데 사용한다. 대입 연산자의 왼쪽의 피연산자를 'lvalue', 오른쪽의 피연산자를 'rvalue'라고 한다. (left와 right)    
` lvalue = rvalue`

대입 연산자는 다른 연산자(op)와 결합하여 'op='의 형태로 사용할 수 있다. 이런 형태로 사용하면 추가된 op의 기능을 사용한 후 대입 연산을 진행한다.
| op= | = |
|:-:|:-:|
| i += 3; | i = i + 3 |
| i -= 3; | i = i - 3 |
| i \*= 3; | i = i \* 3 |
| i /= 3; | i = i / 3 |
| i %= 3; | i = i % 3 |
| i <<= 3; | i = i << 3 |
| i >>= 3; | i = i >> 3 |
| i &= 3; | i = i & 3 |
| i ^= 3; | i = i ^ 3 |
| i \|= 3; | i = i \| 3 |
