[3. 순차 논리](#sequential-logic)         

[3.1 배경](#background)             

[3.2 명세](#specification)           
[3.2.1 데이터 플립플롭](data-flip-flops)           
[3.2.2 레지스터](#register)          
[3.2.3 메모리](#memory)           
[3.2.4 계수기](#counter)            

# Sequential Logic

'무언가를 기억'하는 행위는 본질적으로 시간과 관련이 있다. '지금' 떠올리는 것은 '예전'의 기억이다. 따라서 무언가를 '기억하는' 칩을 만들기 위해서는 먼저 시간 진행을 표현할 수 있는 도구를 개발해야한다.

## Background

### 클록

대부분의 컴퓨터에서는 연속적으로 신호를 발생하는 **Master Clock(마스터 클록)** 으로 시간을 표현한다. 하드웨어는 두 신호(high/low, 0/1, tick/tock) 상태를 연속해서 오고가는 Oscillate(발진기)로 구현된다. tick에서 시작해서 다음 tock까지 경과된 시간을 **Cycle**이라고 부르며, 한 클록 사이클은 하나의 시간 단위 구분을 모델링한 것이다. 현재 클록 상태는 2진 신호로 표현되며 하드웨어의 회로망을 통해 컴퓨터에 있는 모든 순차 칩들에 동시 전달된다.

### 플립플롭

플립플롭은 컴퓨터에서 가장 기본적인 순차 소자이다. 그 중 DFF(Data Flip-Flop)은 1비트 데이터 입력과 1비트 데이터 출력으로 구성된다. 여기서 추가로 마스터 클록에 따라 계속적으로 바뀌는 클록 입력 신호를 받는다. 이 데이터 입력과 클록 입력을 종합해서 시간에 따른 동작을 수행하게 된다. 즉 DFF는 전 시간의 입력을 출력하는 작업을 수행한다. 

`out(t) = in(t-1)`

DFF는 레지스터, RAM 등 컴퓨터에서 상태를 유지하는 모든 하드웨어의 기초가 된다.

### 레지스터 

레지스터는 시간이 지나도 값을 '저장'하고 '로드'할 수 있는 장치로 기본적인 저장 기능을 구현한 장치다.

`out(t) = out(t-1)`

위에서 확인한 바와 같이 DFF는 `out(t) = in(t-1)`을 따른다. 그렇다면 DFF의 출력을 다시 입력으로 되돌린다면 레지스터를 구현 할 수 있을 것이다. 하지만 DFF가 언제 in에서 입력을 받고 out으로 출력하는지 알 수 없기 때문에 이 장치가 새로운 데이터 값을 로드할 수 있을지 확실하지 않다. 

즉 내부 핀은 하나의 fan-in 단자만 있어야 하며, 내부 핀의 입력원이 오로지 하나여야만 한다는 것을 의미한다. 

단 하나의 입력 핀을 만들기 위해 멀티플렉서를 도입한다. 이때, 멀티플렉서의 '선택 비트'는 전체 레지스터의 '로드 비트'가 된다. 만약 레지스터가 새로운 값을 저장하게 하려면 입력 in에 새로운 값을 넣고 로드 비트를 1로 설정하면 된다. 그리고 내부 값을 유지하기 위해서는 로드 비트를 0으로 설정하면 된다. 

레지스터가 저장할 수 있는 비트의 개수를 레지스터의 폭이라고 부르며 레지스터에 저장되는 멀티비트 값은 보통 단어라고 부른다. 그리고 단어의 수를 나타내는 값을 레지스터 크기라고 부른다.

### 메모리

레지스터를 여러 개 쌓아 올리면 RAM(임의 접근 메모리(Random Access Memory))소자를 만들 수 있다. RAM은 메모리 내의 모든 단어는 물리적 저장 위치와 관계없이 똑같은 속도로 접근 가능하다. 

같은 속도로 접근 가능한 이유는 다음과 같이 메모리를 제작하기 때문이다.
```markdown
1. n개의 레지스터 RAM에 있는 각 단어들마다 사용되는 주소 할당
2. n개의 레지스터 배열 구성
3. 주소 x의 레지스터를 개별적으로 선택할 수 있도록 게이트 논리 제작
4. 위 과정에서 물리적 표시를 하지 않음
```

즉 RAM 설계에서 '주소'라는 개념이 명확하게 설정되지 않았기 때문에 같은 속도로 접근이 가능하다. 이는 차후 더 자세히 살펴본다.

RAM은 입력, 주소 입력, 로드 비트의 3 종류의 입력을 받는다. 

### 계수기

계수기는 매 시간 단위마다 내부 상태 값을 증가시키는 순차 칩으로 다음과 같은 연산을 진행한다.          
`out(t) = out(t-1) + c`         

계수기는 디지털 아키텍쳐에서 중요한 역할을 한다. 예를 들어 PC(Program Counter(프로그램 계수기))는 CPU에 탑재되어 다음에 실행해야 할 프로그램 명령의 주소를 출력하는 기능을 한다.

계수기 칩은 표준 레지스터의 입력/출력 논리와, 상태 값에 상수를 더하는 논리가 조합된 것이다. 이를 통해 다음과 같은 작업이 가능해졌다.
```markdown
1. 계수기의 값을 0으로 초기화
2. 새로운 계수 값을 불러옴
3. 값을 증가시키는 대신 감소시키는 기능 추가
```

### 시간 문제

지금까지 설명한 칩들은 모두 **순차적**이다. 순차 칩은 직접적이든 간접적이든 하나 이상의 DFF 게이트를 장착한 칩이다. 
> **기능적 측면**                 
  DFF 게이트를 이용해서 상태를 유지(메모리)하거나 상태를 조작하는 기능(계수기)을 수행한다.                  
  **기술적 측면**             
  피드백 루프와 DFF를 통해 데이터 경쟁을 피하고, 출력이 자신에 영향을 받으며 피드백을 진행한다.

조합 칩의 출력은 시간과 무관하게 입력이 바뀔 때만 변경된다. 반면에 DFF가 들어간 순차 칩의 출력은 한 클록 사이클이 넘어갈 때 바뀌며, 한 사이클 안에서는 바뀌지 않는다. 

이렇게 순차 칩 출력의 이산화(연속적인 신호를 잘게 쪼개서 디지털 시스템에서 표현될 수 있도록 서로 구분되는 불연속적인 신호로 바꾸는 것)로 전체 컴퓨터 아키텍쳐를 동기화 하는데 활용할 수 있다. 

예를 들어 ALU에 x+y를 계산하려고 명령을 내렸다고 가정해보자. x는 근처 레지스터의 값이고 y는 멀리 있는 RAM 레지스터의 값이다. 여기서 물리적 제한(거리, 저항 등)으로 인해 x와 y에 해당하는 전기신호는 ALU의 다른 시점에 도착할 가능성이 크다. 그러나 조합 칩인 ALU는 시간 개념이 없기 때문에 어떤 데이터 값이 도착하던 계속 값을 더한다. 따라서 x+y를 출력하는 데 시간이 오래 걸리고, 그 전까지 ALU의 출력은 의미 없는 값이 된다. 

사실 ALU의 출력은 항상 어떤 순차 칩(레지스터, RAM)으로 전송되기 때문에 이러한 문제를 신경 쓸 필요가 없다. 그냥 비트 하나가 컴퓨터 아키텍쳐 내에서 가장 긴 경로를 따라 전송되는 시간보다 클록 사이클 주기를 조금 더 길게 만들기만 하면 된다. 이렇게 하면 다음 클록 사이클이 시작되기 전까지 ALU에서 전송받은 입력값의 유효함을 보장할 수 있다. 즉 다른 하드웨어들을 하나의 시스템으로 동기화가 가능하다. 



## Specification

### Data Flip-Flops

데이터 플립플롭 게이트는 모든 메모리 소자의 기본 부품이 되는 순차 칩 중 가장 기초적인 칩이다. DFF는 다음과 같이 1비트를 입력받아 1비트를 출력한다.
```markdown
칩 이름 : DFF
입력 : in
출력 : out
기능 : out(t) = in(t-1)
```

DFF는 모두 하나의 마스터 클록에 연결된다. 클록 사이클이 시작할 때, 컴퓨터의 모든 DFF 출력들은 전 사이클의 입력에 따라 맞춰진다. 그 외 시간에는 DFF가 '잠금' 상태가 되어 입력이 변해도 출력이 곧바로 영향을 받지 않는 상태로 변환한다. 

DFF가 들어간 칩은 그 칩에 기반한 모든 상위 계층 칩들에 시간의존성을 부여하는 **순차 칩**이라고 부른다.

DFF를 물리적으로 구현하는 것은 복잡하며, 몇 가지 기본 논리 게이트를 피드백 루프로 연결하는 방법이 사용된다. 

### Register

1비트 레지스터는 하나의 정보 비트를 저장하도록 설계된 소자다. 1비트 레지스터를 연결한 개수 만큼 레지스터의 저장 가능한 용량이 증가한다. 칩 인터페이스는 다음과 같이 데이터 비트를 전달하는 입력 핀, 쓰기 기능을 설정하는 로드 핀, 셀의 현재 상태를 내보내는 출력 핀으로 이루어진다(16개의 레지스터 연결). 
```markdown
칩 이름 : Bit
입력 : in[16], load
출력 : out[16]
기능 : 
If load(t-1) then out(t) = in(t-1)
else out(t) = out(t-1)
```

레지스터 칩은 읽기/쓰기 기능이 완전히 동일하다.

**읽기**
```markdown
출력 신호를 확인한다.
```

**쓰기**
```markdown
1. in에 쓰려는 데이터를 입력한다.
2. load에 명령 신호(1로 설정)를 준다.
3. 다음 클록 사이클이 시작되면 레지스터는 새로운 데이터 값을 받고 출력에서 값을 내보낸다.
```

### Memory

RAM은 직접 접근 메로리 장치로, n개의 w-비트 레지스터를 배열하고 직접 접근 회로로 연결한 소자다. 메모리에 들어간 레지스터의 개수(n)을 메모리의 크기, 비트수(w)를 메모리의 폭이라고 부른다. 메모리는 그 크기에 의해 이름이 다음과 같이 정해진다.
> RAMn = RAM64 = RAM2<sup>k</sup> =  RAM2<sup>6</sup>

폭이 16비트인 다양한 크기(n)의 RAM은 다음과 같이 구성된다.
```markdown
칩 이름 : RAMn
입력 : in[16], address[k], load
출력 : out[16]
기능 : 
out(t) = RAM[address(k)](t)
If load(t-1) then RAM[address(t-1)](t) = in(t-1)
```

**읽기**
```markdown
1. 레지스터 번호 m에 해당하는 주소의 내부 값을 읽기위해 address에 m을 넣는다.
2. RAM의 직접 접근 논리에 따라 레지스터 번호 m이 선택된다.
3. RAM의 출력 핀에 레지스터 번호 m의 값이 출력된다. 
```
**쓰기**
```markdown
1. 새로운 데이터 d를 레지스터 번호 m에 해당하는 주소에 쓰기 위해 address에 m을, in에 d를 입력하고고 load 비트를 활성화 한다.
2. RAM의 직접 접근 논리에 따라 레지스터 번호 m이 선택된다. 
3. load 비트로 인해 RAM이 쓰기 모드로 전환된다.
4. 클록 사이클에서 선택된 레지스터가 새로운 값 d를 받아 출력한다.
```

### Counter

계수기는 그 자체로 독립적인 추상화 계층이다. 예를 들어 컴퓨터가 다음에 실행할 명령의 주소를 기록하는 계수기 칩(PC)을 생각해보자. 일반적인 상태에서 계수기는 매 클록 사이클마다 단순히 상태 값을 1 증가시켜 컴퓨터가 프로그램에서 다음 명령을 불러올 수 있게 해야한다. 그리고 n번호 명령으로 접근하기 위한 기능과 명령 주소를 0으로 재시작하는 기능을 추가하기 위해 **load** 기능과 **reset** 기능을 수행하는 계수기가 필요하다. 

이러한 인터페이스를 바탕으로 16비트 PC를 구현하면 다음과 같다.
```markdown
칩 이름 : PC
입력 : in[16], inc, load, reset
출력 : out[16]
기능 : 
If reset(t-1) then out(t) = 0
  else if load(t-1) then out(t) = in(t-1)
    else if inc(t-1) then out(t) = out(t-1) + 1
      else out(t) = out(t-1)
```

> ict = 1이면, 계수기는 매 클록 사이클마다 상태 값을 증가시키고 out(t) = out(t-1) + 1을 출력한다.        
  reset 비트를 활성화화면, 계수기를 0으로 재설정한다.             
  load 비트를 활성화하고 in에 d를 입력하면, 계수를 d로 초기화한다.             

