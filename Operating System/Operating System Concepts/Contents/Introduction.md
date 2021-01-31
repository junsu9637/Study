# 서론

> \- 컴퓨터 시스템의 일반적인 구성과 인터럽트의 역할
  \- 현대 다중 처리기 컴퓨터 시스템의 구성요소
  \- 사용자 모드에서 커널 모드로의 전환
  \- 다양한 컴퓨팅 환경에서 운영체제의 사용 방식
  \- 공개 소스 운영체제의 예


**Operating System(운영체제)**
하드웨어를 관리하는 소프트웨어    
응용 프로그램을 위한 기반을 제공하며 컴퓨터 사용자와 컴퓨터 하드웨어 사이의 중재자 역할 수행

운영체제의 역할을 학습하기 위해서는 먼저 컴퓨터 하드웨어의 구성과 구조를 이해하는 것이 중요하다.

운영체제는 덩치가 크고 복잡하기 때문에 부분별로 생성 되어야 하고, 이 하나의 부분은 전체 시스템 윤곽에 잘 맞는 일부여야 한다.

# 차례
[1.1 운영체제가 할 일](#What-Operating-System-Do)
[1.1.1 사용자 관점](#User-View)
[1.1.2 시스템 관점](#System-View)
[1.1.3 운영체제의 정의](#Operating-System-Definitions)

[1.2 컴퓨터 시스템의 구성](#Computer-System-Organization)
[1.2.1 인터럽트](#Interrupts)
[1.2.2 저장장치 구조](#Storage-Structure)
[1.2.3 입출력 구조](#io-structure)

[1.3 컴퓨터 시스템의 구조](#Computer-System-Architecture)

[1.4 운영체제의 작동](#Operating-System-Operations)

[1.5 자원 관리](#Resource Management)

[1.6 보안과 보안](#Security and Protection)

[1.7 가상화](#Virtulization)

[1.8 분산 시스템](#Distributed-Systems)

[1.9 커널 자료구조](#Kernel_Data-Structures)

[1.10 계산 환경](#Computing Environments)

[1.11 무료 및 공개 소스 운영체제](#Free-and-OpenSource-Operating-Systems)

# IO Structure