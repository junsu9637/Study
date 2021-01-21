# 운영체제

컴퓨터 하드웨어를 잘 관리하여 *성능*을 높이고 사용자에게 *편의성*을 제공하는 컴퓨터 하드웨어 관리 프로그램 <br>
`하드웨어 < 운영체제 (Kernel < Shell) < 애플리케이션`
> **Kernel** : 하드웨어 관리 <br>
  **Shell** : 사용자 명령 해석

**부팅**

컴퓨터 시스템 내부에서 OS 실행
> **1. POST를 실행** <br>
  컴퓨터 하드웨어 상태 확인 (프로세서 - 메모리(ROM, RAM) - 보조기억장치) <br>
  **2. Boot loader 실행** <br>
  보조기억장치에 있는 OS를 RAM으로 옮겨옴 <br>
  컴퓨터가 종료 될 때까지 상주(Resident)한다. 

## 역사

- **1940s 컴퓨터 개발** <br>
입력장치 - 메모리 - 프로세서 - 출력장치

  \+ 운영체제

- **Batch Processing System (일괄처리)** <br> 
연속되는 과정을 메모리에 저장 -> 운영 과정 단순화 <br>
*Resident Monitor : 최초의 운영체제*

  \+ 보조기억장치

- **Multiprogramming System (다중프로그래밍)** <br>
느린 하드웨어로 인한 CPU 작업 중지(Idle) -> 메모리에 여러 프로그램 <br>
*CPU scheduling, 메모리 관리 및 보호*

  \+ 모니터, 키보드

- **Time-Sharing System (시공유 시스템)** <br>
일정시간이 지나면 프로그램 강제 전환 -> 여러 프로그램 동시 수행 <br>
*가상 메모리, 프로세스간 통신, 동기화* <br>
*Unix, Linux 기반 기술*

  \+ 고등 컴퓨터 구조 
  
- **Multiprocessor OS (다중 프로세서 운영체제)** <br>
  *Multiprocessor System (다중 프로세서 시스템)* <br>
  여러 CPU를 병렬 연결한 시스템 <br>
  성능, 가격, 신뢰성에 유리
  
- **Distributed OS (분산 운영체제)** <br>
  *Distributed System(분산 시스템)* <br>
  여러 컴퓨터를 연결한 시스템
  
  
- **RTOS = Real-Time OS (실시간 운영체제)** <br>
  *Real-Time System (실시간 시스템)* <br>
  일정 시간 내에 작업을 끝내야 하는 시스템
  *군사, 항공, 우주, 공장 자동화에 *
  
## 인터럽트 기반 시스템

다양한 하드웨어를 사용하는 현대 운영체제는 인터럽트 기반으로 운영된다

**인터럽트** : 현재 진행하던 작업을 중지하고 다른 작업 수행

- **하드웨어 인터럽트** <br>
  인터럽트 발생 시 운영체제 내의 특정 코드 실행 (ISR) <br>
  Interrupt Service Routine 종료 후 대기 <br>

- **소프트웨어 인터럽트** <br>
  운영체제 서비스 이용이 필요한 사용자 프로그램이 실행 <br>
  인터럽트 발생 시 운영체제 내의 특정 코드 실행 (ISR) <br>
  Interrupt Service Routine 종료 후 대기
 
> **운영체제 대기 상태** <br>
  \- 하드웨어 인터럽트에 의해 ISR 실행 <br>
  \- 소프트웨어 인터럽트에 의해 ISR 실행 <br>
  \- 내부 인터럽트에 의해 ISR 실행 <br>
  **ISR 종료** <br>
  **원래 대기상태 또는 사용자 프로그램으로 복귀**




