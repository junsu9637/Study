# 차례

[1. 불 논리](#boolean-logic) 

[1.1 배경](#background)              
[1.1.1 불 대수](#boolean-algebra)              
[1.1.2 게이트 논리](#gate-logic)           
[1.1.3 실제 하드웨어 구성](#physical-hardware-configuration)                      
[1.1.4 하드웨어 기술 언어](#hardware-technical-language)                 
[1.1.5 하드웨어 시레이션](#hardware-simulation)                

[1.2 명세](#specification)                                         
[1.2.1 Nand 게이트](#nand-gate)             
[1.2.2 기본 논리 게이트](#basic-logic-gate)                  
[1.2.3 기본 게이트의 멀티비트 버전](#multi-bit-version-of-the-basic-gate)                 
[1.2.4 기본 게이트의 다입력 버전](#multi-input-version-of-basic-gate)              
       
# Boolean Logic

디지털 기기는 모두 정보를 저장하고 처리하도록 설계된 칩들을 탑재한다. 이 칩들은 동일한 구성 요소인 **논리 게이트**로 만들어진다. 게이트는 물리적으로는 다양한 소재와 제작기술로 구현되지만 논리적 작동 방식은 모든 컴퓨터에서 동일하다. 이 문서에서는 Nand 게이트를 이용해 다른 논리 게이트를 만들 것이다. 여기서 Nand 게이트를 사용하는 것은 Nand 함수가 이론적으로 And, Or, Not 연산을 이 함수만으로 만들 수 있기 때문이다.

## Background

`Boolean Algebra -> Boolean Function -> Boolean Gate`               
불 대수를 기반으로 불 함수를 구현하고, 불 함수를 기반으로 불 게이트를 구현한다. 

### Boolean Algebra

불 대수는 참/거짓, 1/0과 같은 Boolean(2진수)값을 다루는 대수학이다. 불 함수는 2진수를 입력받아 2진수를 출력하는 함수다.              
컴퓨터는 2진수를 표현하고 처리하는 하드웨어이므로, 불 함수는 하드웨어 아키텍쳐에 중심적인 역할을 한다. 따라서 불 함수를 정의하고 분석하는 것이 컴퓨터 아키텍쳐를 구축하는 첫 단계가 된다.

#### 진리표 표현

Truth table(진리표)는 불 함수를 정의하는 가장 쉬운 방법으로 함수의 입력값들과 결과값을 나란히 쓰는 방식이다. 아래 표에서 앞의 세 열은 함수 입력값이 될 수 있는 모든 2진 값 조합을 나타낸다. 마지막 열은 2<sup>n</sup>개의 튜플v<sub>1</sub>...v<sub>n</sub>에 대한 함수 값f(v<sub>1</sub>...v<sub>n</sub>)이다.
| x y z | f(x,y,z)|
|:-:|:-:|
| 0 0 0 | 0 |
| 0 0 1 | 0 |
| 0 1 0 | 1 |
| 0 1 1 | 0 |
| 1 0 0 | 1 |
| 1 0 1 | 0 |
| 1 1 0 | 1 |
| 1 1 1 | 0 |

#### 불 표현식

불 표현식은 불 함수를 표현하는 다른 방식이다. 
> *x And y = x ∙ y                    
  x Or y = x + y       
  Not x = x¯*

위 표에서 정의된 함수를 불 표현식으로 표현하면 *f(x,y,z) = (x+y)∙z¯*가 된다. 

#### 정준 표현

정준 표현은 불 함수를 표현하는 다른 방식이다. 함수의 진리표에서 함수 값이 1인 행들을 살펴보면 각 행의 입력값에 대해 literal(변수나 변수의 부정값)을 And 연산으로 묶어 하나의 항으로 구성할 수 있다. 예를 들어 7행은 x=1,y=1,z=0이므로 *xyz¯*로 표현이 가능하다. 그리고 Or 연산으로 묶으면 주어진 진리표와 동등한 불 표현식을 얻게 된다. 따라서 위 표의 불 함수에 대한 정준 표현은 *f(x,y,z) = x¯yz¯ + xy¯z¯ + xyz¯*이다.

### Gate Logic

**Gate**는 불 함수를 구현한 물리적 장치다. n개의 변수를 받아 m개의 2진 결과값을 반환하는 불 함수 *f*가 잇을때, *f*를 구현하는 게이트에는 n개의 입력 핀과 m개의 출력 핀이 있다. 이 게이트의 입력 핀에 v<sub>1</sub>...v<sub>n</sub>을 넣으면 게이트의 '논리'(내부구조)가 출력값 *f*(v<sub>1</sub>...v<sub>n</sub>)를 계산한다.

가장 단순한 형태의 게이트들은 *트랜지스터*라고 불리는 아주 작은 스위치 장치들을 특정한 구조로 연결해서 특정 기능을 하도록 만든 것들이다. 따라서 오늘날 대부분의 컴퓨터는 2진 데이터 표현이나 게이트 사이의 데이터 전달에 전기 기술을 이용하지만, 스위치 기능이나 신호 전달 기능을 통해 다른 기술도 사용할 수 있다. 최근에는 대부분의 게이트가 실리콘 etching 방식(반도체 표면을 산으로 부식시켜 소거하는 방법)으로 만든 트랜지스터로 구현되며, 게이트들은 chip으로 집적된다. 

`Transistor -> Gate -> Chip`

스위치는 여러 기술로 구현할 수 있지만 이런 기술들을 모두 불 대수로 추상화할 수 있다. 이는 컴퓨터 과학자들이 전기회로, 스위치 등 물리적인 영역에 신경 쓸 필요가 없다는 것을 의미한다. 대신 컴퓨터 과학자들은 추상적인 불 대수와 논리 게이트만 신경쓰면 된다. 

**Primitive Gate(기본 게이트)** 는 기본 논리 연산을 구현한 블랙박스로 볼 수 있기 때문에 우리는 상세한 구현방식을 알 필요가 없다. 하드웨어 설계자는 이런 기본 게이트들이 서로 연결된 **Composite Gate(조합 게이트)** 를 통해 더 복잡한 기능을 구현한다.

#### 기본 게이트와 조합 게이트

모든 논리 게이트는 입력 및 출력 신호 형태가 2진수로 같으므로 서로 연달아 이으면 더 복잡한 조합 게이트를 만들 수 있다. 이렇게 게이트를 서로 연결해서 더 복잡한 기능을 하는 조합 게이트를 만드는 기술을 **Logic Design(논리 설계)** 라고 한다.

논리 게이트들은 내부와 외부의 2가지 관점으로 볼 수 있다. 
> 내부 : 게이트의 내부 아키텍쳐로 **Inplementation(구현)** 에 해당한다         
  외부 : 바깥에 노출된 입력 핀과 출력 핀으로 구성된 블랙박스로 **Interface(인터페이스)** 에 해당한다

내부 아키텍쳐는 직접 게이트를 설계하려는 사람에게만 의미가 있고, 게이트 내부 구조를 신경쓰지 않고 추상적인 구격 부품으로만 활용하려는 사람에게는 인터페이스 단계만으로 충분하다. 

게이트 인터페이스는 보통 진리표, 불 표현식으로 표현되며 본질적인 내용은 유일하다. 하지만 이 인터페이스를 구현하는 방식은 여러 가지가 있다. 따라서 기능적 관점에서 논리 설계에 가장 기본적으로 '어떤 방식으로든 정해진 인터페이스를 따르는 게이트를 구현한다'라는 요구사항과 효율성 관점에서 '최소 비용으로 최대 효과를 내야한다'라는 요구사항이 존재한다.

### Physical Hardware Configuration

조합 게이트를 설계할 때 직접 제작하는 방식은 제작 과정이 맞는지 검증하기가 어렵다. 따라서 우리는 침을 만들어서 전원을 연결하고, 입력 핀에 다양한 조합으로 신호를 입력하며 출력이 계간과 맞는지 확인해 보는 실험적 테스트만 진행할 수 있다. 그리고 설계가 잘못 되었다면 작업을 다시 진행해야 하니 더 좋은 방법이 필요하다. 
   
### Hardware Technical Language

최근에는 **HDL(Hardware Technical Language(하드웨어 기술 언어))** 또는 **VHDL(Virtual Hardware Technical Language(가상 하드웨어 기술 언어))** 라는 도구를 사용해서 칩 아키텍쳐를 설계하고 최적화한다. 설계자는 HDL 프로그램으로 칩 아키텍쳐를 작성하고, **하드웨어 시뮬레이터**를 사용한다. 

하드웨어 시뮬레이터는 HDL 프로그램을 입력으로 받아 메모리 위에 모델링된 칩 이미지를 만든다. 그리고 설계자는 이 가상 칩 이미지에 다양한 입력 집합을 주고 출력을 시뮬레이션해 보며 칩의 동작을 테스트한다. 이를 통해 출력값이 요구사항에 맞는지 확인한다. 뿐만 아니라 계산 속도, 전력 소비 등 칩의 요구 성능 대비 비용 수준을 확인할 수 있다. 

따라서 HDL을 활용하면 실제 칩 생산에 들어가기 전에 칩을 설계 디버깅, 최적화하는 일을 수행할 수 있다. 

HDL은 헤더 부분과 파트 부분으로 구성된다.
> 헤더 : 칩 인터페이스를 정의하는 부분으로 칩 이름과 입력 및 출력 이름 명시         
  파트 : 칩을 구성하는 아래 단계 파트들의 이름과 연결방식을 정의

HDL을 사용해서 Xor(a,b) = Or(And(a, Not(b)), And(Not(a),b))를 작성해 보자
```hdl
// Xor.hdl
CHIP Xor
{
    IN a, b;
    OUT out;
    
    PARTS:
    Not(in=a, out=nota);
    Not(in=b, out=nota);
    And(a=a, b=notb, out=w1);
    And(a=nota, b=b, out=w2);
    Or(a=w1, b=w2, out=out);
}
```

위 코드에서 파트 사이의 연결은 내부 핀을 생성하고 연결하는 방식으로 표현되는 것을 볼 수 있다. Not 게이트의 출력이 And 게이트의 입력과 이어지는 부분을 보면, Not(..., out=nota)와 And(a=nota, ...)라는 두 구문으로 구성했다. 

이제 HDL 프로그램을 테스트하는 코드를 작성해 보자
```tst
load Xor.hdl, output-list a, b, out;
set a 0, set b 0, eval, output;
set a 0, set b 1, eval, output;
set a 1, set b 0, eval, output;
set a 1, set b 1, eval, output;
```

위 코드에서 Xor.hdl이라는 HDL 프로그램을 로드하고 주어진 변수 값을 출력할 준비를 진행한다. 그리고 정해진 테스트 시나리오를 진행하면서 지정된 파일에 기록하고 있다. 

## Specification

이 절에서는 불 연산을 수행하는 게이트들을 정의한다. 게이트들의 명세나 인터페이스만 정의하고 상세 구현은 다음 문서에서 진행할 것이다. 특정 게이트에 대한 구현은 부록 A에서 정리된다.

### Nand Gate

모든 게이트들의 기초가 되는 Nand 게이트는 다음과 같은 불 함수를 계산한다.
| a b | Nand(a,b) |
|:-:|:-:|
| 0 0 | 1 |
| 0 1 | 1 |
| 1 0 | 1 |
| 1 1 | 0 |

앞으로는 이 내용을 아래와 같이 정의할 것이다.
```markdown
칩 이름 : Nand         
입력 : a, b             
출력 : out                      
기능 : If a = b = 1 then out = 0, else out = 1                         
```

### Basic Logic Gate

**And** : 입력값이 둘 다 1일 경우 1을, 그 외에는 0을 반환한다.
```markdown
**칩 이름 : And         
**입력 : a, b             
**출력 : out                      
**기능 : If a = b = 1 then out = 1, else out = 0  
```

**Or** : 입력값 중 적어도 하나가 1일 때 1을, 그 외에는 0을 반환한다.
```markdown
칩 이름 : Or         
입력 : a, b             
출력 : out                      
기능 : If a = b = 0 then out = 0, else out = 1  
```

**Xor** : *Exclusive or(베타적 논리합)* 이라고도 불리며 두 입력값이 다를 경우 1, 그 외에는 0을 반환한다.
```markdown
칩 이름 : Xor         
입력 : a, b             
출력 : out                      
기능 : If a != b then out = 1, else out = 0  
```

**Not** : *Converter(컨버터)* 라고도 불리며 입력값을 0에서 1 또는 1에서 0으로 바꿔서 반환한다.
```markdown
칩 이름** : Not         
입력 : in             
출력 : out                      
기능 : If in = 0 then out = 1, else out = 0
``` 

**Multiplexor** : 3-입력 게이트의 멀티플렉서는 Selection bit(선택 비트)를 입력받아 나머지 2개의 Data bit(데이터 비트) 중 하나를 선택한다. 따라서 Selector이라는 이름으로도 불린다.
```markdown
칩 이름 : MUX         
입력 : a, b, sel             
출력 : out                      
기능 : If sel = 0 then out = a, else out = b  
```

**DeMultiplexor** : 멀티플랙서와 반대 기능을 한다. 따라서 선택 비트에 따라 두 출력 중 하나를 선택해서 입력 신호를 보낸다. 
```markdown
칩 이름 : DMux         
입력 : in, sel             
출력 : a, b                      
기능 : If sel = 0 then {a = in, b = 0}, else {a = 0, b = in}
```
  
### Multi-Bit Version Of The Basic Gate

컴퓨터 하드웨어는 버스라고 불리는 멀티비트 배열에 대해 연산을 수행한다. 예를 들어 32비트 컴퓨터는 2개의 32비트 버스에 대한 And 함수를 연산할 수 있다. 이 연산은 32개의 2진 And 게이트를 나란히 놓고, 각각의 비트 쌍마다 And를 적용하는 방식으로 구현된다.

이 절에서는 16비트 컴퓨터 구축에 필요한 멀티비트 논리 게이트들을 소개한다. n 비트 논리 게이트의 아키텍쳑도 기본적으로 동일하다. 

버스 내의 개별 비트들을 가리킬 때는 배열 문법을 활용한다. 예를 들어 data라는 16비트 버스가 있다면 data[0], ... , data[15]와 같이 개별 비트를 표시한다.

**멀티비트 And** : n 비트 And 게이트는 2개의 n 비트 입력 버스에서 들어오는 모든 n 비트 쌍에 대해 And 연산을 수행한다.
```markdown
칩 이름 : And16
입력 : a[16] b[16]
출력 : out[16]
기능 : For i = 0...15 out[i] = And(a[i], b[i])
```

**멀티비트 Or** : n 비트 Or 게이트는 2개의 n 비트 입력 버스에서 들어오는 모든 n 비트 쌍에 대해 Or 연산을 수행한다.
```markdown
칩 이름 : Or16
입력 : a[16] b[16]
출력 : out[16]
기능 : For i = 0...15 out[i] = Or(a[i], b[i])
```

**멀티비트 Not** : n비트 Not 게이트는 n 비트 입력 버스의 모든 비트에 대한 Not 연산을 수행한다.
```markdown
칩 이름 : Not16
입력 : in[16]
출력 : out[16]
기능 : For i = 0...15 out[i] = Not(in[i])
```

**멀티비트 Multiplexor** : n 비트 Multiplexor는 입력 비트가 n 비트라는 것을 제외하면 기존과 동일하다. 선택 비트는 여전히 1비트다.
```markdown
칩 이름 :Mux16
입력 : a[16] b[16]. sel
출력 : out[16]
기능 : If sel = 0 then for i = 0...15 out[i] = a[i] else for i = 0...15 out[i] = b[i]
```

### Multi-Input Version Of Basic Gate

2-입력 논리 게이트들은 입력이 여러 개인 다입력 게이트들로 일반화할 수 있다. 

**다입력 Or** : n-입력 Or 게이트는 n 비트 입력 중 적어도 하나가 1이면 1을 출력하고, 그 외에는 0을 출력한다. 아래는 8-입력 게이트의 예시다.
```markdown
칩 이름 : Or8Way
입력 : in[8]
출력 : out
기능 : out = Or(in[0],...,in[7])
```

**다입력 Multiplexor** : m-입력 n 비트 multiplexor는 m개의 n비트 입력 버스 중에 하나를 골라서 n 비트를 출력 버스에 출력한다. 선택 입력은 k개의 제어 비트로 되어 있으며 *k = log<sub>2</sub>m*이다. 아래 예시는 4-입력 16비트 multiplexor다.
```markdown
칩 이름 : Mux4Way16
입력 : a[16], b[16], c[16], d[16], sel[2]
출력 : out[16]
기능 : 
If sel = 00 then out = a 
else if sel = 01 then out = b 
else if sel = 10 then out = c 
else if sel = 11 then out = d
```

**다입력 DeMultiplexor** : m-입력 n 비트 DeMultiplexor는 n 비트 입력을 하나 받아 m개의 n 비트 출력 중 하나를 내보낸다. 선택 입력은 k개의 제어 비트로 되어 있고, *k = log<sub>2</sub>m*이다. 아래 예시는 4-입력 1비트 Demultiplexor다.

```markdown
칩 이름 : DMux4Way
입력 : in, sel[2]
출력 : a, b, c, d
기능 : 
If sel = 00 then {a = in, b=c=d= 0} 
else if sel = 01 then {b = in, a=c=d= 0} 
else if sel = 10 then {c = in, a=b=d= 0} 
else if sel = 11 then {d = in, a=b=c= 0}
```




