[4. 기계어](#machine-language)         
[4.1 배경](#background)
[4.1.1 기계](#machine)
[4.1.2 언어](#language)
4.1.3 명령(#command)

[4.2 명세](#specification)      
개요(#outline)
A-명령어(a-command)
C-명령어
기호
입출력 조작
구문 규칙과 파일 형식

# Machine Language

컴퓨터는 어떤 하드웨어 플랫폼을 저수준 칩들로 어떻게 구성했는지를 **구성적**으로 설명할 수 있다. 그리고 기계어의 함수들을 정의하고 사용법을 보여주는 방식으로 **추상적**으로 설명할 수 있다. 기계어 프로그램을 통해 하드웨어가 왜 이렇게 설계되었는지 이해하는데 도움이 된다.

기계어는 기계 수준의 명령어들로 이루어진 저수준 프로그램을 코딩할 수 있도록 미리 정의된 규칙으로 해당 하드웨어 플랫폼에서 직접적으로 명령을 실행하거나 하드웨어를 완전히 제어하는 것을 주요 목표로 삼는다. 

기계어는 전체 컴퓨터 시스템에서 가장 기본이 되는 인터페이스로 하드웨어와 소프트웨어가 만나는 접점이다. 즉 기계어는 프로그래밍 도구인 동시에 하드웨어 플랫폼의 구성 요소가 된다. 

## Background

### Machine

**기계어**는 프로세서와 레지스터들을 이용해서 메모리르 조작할 수 있도록 미리 정의된 규칙이라고 볼 수 있다.

#### 메모리

메모리는 컴퓨터에서 데이터와 명령어를 저장하는 하드웨어 장치들을 통칭하는 용어다. *'단어'* 나 *'위치'* 라고 불리는 정해진 폭의 셀들이 연속적으로 배열되어 각각에 유일한 *'주소'* 가 있는 구조다. 따라서 개별 단어는 주소를 통해 특징된다. 이러한 주소는 `Memory[address], RAM[address], M[address]` 로 표현한다.

#### 프로세서 

CPU 혹은 중앙 처리 장치라고 불리는 특정한 기초 연산들을 수행하는 장치다. 기초 연산은 산술 및 논리 연산, 메모리 접근 연산, 제어 연산이 포함된다. 이 연산의 피연산자는 선택된 메모리 위치와 레지스터에 있는 2진 값이다. 연산의 결과값은 선택된 메모리 주소나 레지스터에 저장된다.

#### 레지스터

레지스터는 프로세서 바로 엎에 위치해서, 프로세서가 명령어와 데이터를 빠르게 조작할 수 있도록 도와주는 로컬 고속 메모리의 역할을 수행한다. 

### Language


# A-Command