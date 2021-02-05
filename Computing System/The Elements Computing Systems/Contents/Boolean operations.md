[2. 불 연산](#boolean-operations)           
[2.1 배경](#background)              
[2.2 명세](#specification)             
[2.2.1 가산기](#adder)              
[2.2.2 산술 논리 연산 장치](#arithmetic-logical-unit)            

# Boolean Operations

## Background

### 2진수         
기수(base)를 2로 한다. 예를 들어 10진법의 19를 2진법으로 표현하면 다음과 같다.

19 = (10011)<sub>2</sub> = 1\*2<sup>4</sup> + 0\*2<sup>3</sup> + 0\*2<sup>2</sup> + 1\*2<sup>1</sup> + 1\*2<sup>0</sup>

19가 16비트 컴퓨터에 저장될 때는 0000000000010011, 8비트 컴퓨터에 저장될 대는 00010011로 저장된다. 

### 2진 덧셈
두 개의 2진수를 덧셈하려면 오른쪽부터 왼쪽 자릿수로 숫자들을 더한다. (최하위 비트 ~ 최상위 비트)
> Least Significant Bit(LSB) : 최하위 비트 : 가장 오른쪽 숫자         
  Most Significant Bit(MSB) : 최상위 비트 : 가장 왼쪽 숫자
  
마지막 비트를 더하고 나서도 자리올림수가 1이라면, 오버플로(Overflow)가 발생한다.

### 부호가 있는 2진수

2진 코드에서 부호가 있는 숫자를 표현하기 위해서 여러가지 코딩 방식이 개발되었다. 그 중 오늘날 가장 많이 사용하는 방법은 **2의 보수법**이다. n개의 숫자로 된 2진수 x가 있을 때, x의 2의 보수는 다음과 같이 정의한다.
```markdown
x의 2진 보수 = 2<sup>n</sup> - x
```

예를 들어 (00010)<sub>2</sub>의 2진 보수는 2<sup>5</sup> - (00010)<sub>2</sub> = (32)<sub>10</sub> - (2)<sub>10</sub> = (30)<sub>10</sub> = (11110)<sub>2</sub>이다. 

**2진 보수의 특징**
```markdown
1. 2<sup>n</sup>개의 부호가 있는 숫자를 표현할 수 있다.           
2. 최대값은 2<sup>n-1</sup>-1, 최솟값은 -2<sup>n-1</sup>이다.            
3. 모든 양수 코드는 0으로 시작한다.          
4. 모든 음수 코드는 1로 시작한다.           
```

**2진 보수를 구하는 간단한 방법**
```markdown
1. 최하위 비트부터 시작해서 처음으로 나오는 1까지는 바꾸지 않고, 그 다음 비트부터 모두 반대로 바꾼다.           
2. 모든 비트를 반대로 바꾸고 1을 더한다.
```

2의 보수법은 2의 보수로 표현된 숫자의 덧셈과 양수끼리의 덧셈 방식이 완전히 똑같다. 따라서 양수와 음수를 신경쓰지 않고 연산이 가능하다. 이런 내용은 ALU(산술 논리 연산 장치) 칩 하나에 모든 기초 산술과 논리 연산자를 담을 수 있다는 뜻이 된다. 

## Specification

### Adder

가산기는 두 개의 n비트 숫자를 더한다. n은 환경에 따라 16, 32, 64 등으로 다양하다. 주어진 값의 2의 보수 덧셈을 진행하고, 오버프로는 감지나 처리되지 않는다. 
```markdown
칩 이름 : Add16
입력 : a[16], b[16]
출력 : out[16]
기능 : out = a + b
```

#### Half-Adder

반가산기는 두 비트를 더한다. 보통 덧셈 한 값의 최하위 비트를 sum, 최상위 비트를 carry라고 한다. 
```markdown
칩 이름 : HalfAdder
입력 : a, b
출력 : sum, carry
기능 : 
sum = a + b의 LSB
carry = a + b의 MSB
```

#### Full-Adder

전가산기는 세 비트를 더한다. 보통 덧셈 한 값의 최하위 비트를 sum, 최상위 비트를 carry라고 한다. 
```markdown
칩 이름 : FullAdder
입력 : a, b, c
출력 : sum, carry
기능 : 
sum = a + b + c의 LSB
carry = a + b + c의 MSB
```

#### Incrementer

증분기는 주어진 숫자에 1을 더한다. 
```markdown
칩 이름 : Inc16
입력 : in[16]
출력 : out[16]
기능 : out = in + 1
```

### Arithmetic Logical Unit

ALU는 16비트 x, y의 2개의 입력값을 받고, 16비트의 1개의 out 출력을 내보낸다. 그리고 Control bit(제어 비트)라는 6개의 입력(zx, nx, zy, xy, f, no)을 추가적으로 받아서 x, y 값을 정해진 18개의 산술 및 논리 함수 중 어떤 연산을 진행할 지 결정한다. ALU의 구성은 다음과 같다.
```markdown
칩 이름 : ALU
입력 : 
x[16], y[16] // 두 개의 16 비트 데이터 입력
zx // 입력 x를 0으로 지정
nx // 입력 x를 반전
zy // 입력 y를 0으로 지정
nx // 입력 y를 반전
f // 함수 코드(Add면 1, And면 0)
no // 출력 out을 반전
출력 :
out[16] // 16비트 출력
zr // out=0일 때, True
ng // out<0일 때, True
기능 :
if zx then x = 0 // 16비트 상수 0
if nx then x = !x // 비트 반전
if zy then y = 0 // 16비트 상수 0
if ny then y = !y // 비트 반전
if f then out = x + y  else out = x & y // 2의 보수법으로 정수 덧셈 또는 And 연산
if no then out = !out // 비트 반전
if out=0 then zr = 1 else zr = 0 // 16비트 eq
if out<0 then ng = 1 else ng = 0 // 16비트 neq
```
