# 운영체제

컴퓨터 하드웨어를 잘 관리하여 *성능*을 높이고 사용자에게 *편의성*을 제공하는 컴퓨터 하드웨어 관리 프로그램      
`하드웨어 < 운영체제 (Kernel < Shell) < 애플리케이션`
> **Kernel** : 하드웨어 관리      
  **Shell** : 사용자 명령 해석

**부팅** <br>
컴퓨터 시스템 내부에서 OS 실행
> **1. POST를 실행**       
  컴퓨터 하드웨어 상태 확인 (프로세서 - 메모리(ROM, RAM) - 보조기억장치)     
  **2. Boot loader 실행**      
  보조기억장치에 있는 OS를 RAM으로 옮겨옴       
  컴퓨터가 종료 될 때까지 상주(Resident)한다. 

## 역사

- **1940s 컴퓨터 개발**       
입력장치 - 메모리 - 프로세서 - 출력장치

  \+ 운영체제

- **Batch Processing System (일괄처리)**      
연속되는 과정을 메모리에 저장 -> 운영 과정 단순화       
*Resident Monitor : 최초의 운영체제*

  \+ 보조기억장치

- **Multiprogramming System (다중프로그래밍)**        
느린 하드웨어로 인한 CPU 작업 중지(Idle) -> 메모리에 여러 프로그램       
*CPU scheduling, 메모리 관리 및 보호*

  \+ 모니터, 키보드

- **Time-Sharing System (시공유 시스템)**       
일정시간이 지나면 프로그램 강제 전환 -> 여러 프로그램 동시 수행    
대화형 시스템    
*가상 메모리, 프로세스간 통신, 동기화*       
*Unix, Linux 기반 기술*

  \+ 고등 컴퓨터 구조 
  
- **Multiprocessor OS (다중 프로세서 운영체제)**       
  *Multiprocessor System (다중 프로세서 시스템)*       
  여러 CPU를 병렬 연결한 시스템        
  성능, 가격, 신뢰성에 유리
  
- **Distributed OS (분산 운영체제)**        
  *Distributed System(분산 시스템)*        
  여러 컴퓨터를 연결한 시스템
  
  
- **RTOS = Real-Time OS (실시간 운영체제)**       
  *Real-Time System (실시간 시스템)*        
  일정 시간 내에 작업을 끝내야 하는 시스템
  *군사, 항공, 우주, 공장 자동화에 *
  
# 인터럽트 기반 시스템

다양한 하드웨어를 사용하는 현대 운영체제는 인터럽트 기반으로 운영된다

**인터럽트** : 현재 진행하던 작업을 중지하고 다른 작업 수행

- **하드웨어 인터럽트**       
  인터럽트 발생 시 운영체제 내의 특정 코드 실행 (ISR)     
  Interrupt Service Routine 종료 후 대기       

- **소프트웨어 인터럽트**       
  운영체제 서비스 이용이 필요한 사용자 프로그램이 실행      
  인터럽트 발생 시 운영체제 내의 특정 코드 실행 (ISR)       
  Interrupt Service Routine 종료 후 대기
 
> **운영체제 대기 상태**       
  \- 하드웨어 인터럽트에 의해 ISR 실행      
  \- 소프트웨어 인터럽트에 의해 ISR 실행       
  \- 내부 인터럽트에 의해 ISR 실행       
  **ISR 종료**       
  **원래 대기상태 또는 사용자 프로그램으로 복귀**

## 이중모드 (Dual mode)

한 컴퓨터를 여러 사람이 동시에 사용 or 한 사람이 여러 개의 프로그램을 동시에 사용하는 환경       
한 사람이 전체 프로그램에 영향을 미칠 수 있으므로 특권 명령으로 권한을 제한 -> 컴퓨터 시스템 보호       
*특권 명령: STOP, HALT, RESET, SET_TIMER, SET_HW ...*

> **사용자(user) 모드**       
  **관리자(Supervisor or System) 모드**
  
**플래그** : 레지스터에 모드를 나타냄
> 운영체제 서비스 실행 : *관리자 모드*       
  사용자 프로그램 실행 : *사용자 모드*       
  HW/ SW 인터럽트 발생 : *관리자 모드*       
  운영체제 서비스 종료 : *사용자 모드*       

### 하드웨어 보호

> 입출력장치 보호    
  메모리 보호    
  CPU 보호

#### 입출력장치 보호

사용자의 잘못된 입출력 명령으로 다른 사용자의 입출력, 정보 등에 방해하는 문제 방지
> **입출력 명령을 특권명령으로 제어 : IN, OUT**       
  IN : 입력장치로부터 정보를 받아들임       
  OUT : 출력장치에 명령               
  **운영체제가 입출력 대행**      
  입출력 실행 시 System mode      
  입툴력 종료 시 User mode      
  올바른 요청이 아니라면 운영체제가 거부

#### 메모리 보호

다른 사용자 메모리 or 운영체제 영역 메모리에 접근하는 문제 방지
> **MMU를 통한 메모리 영역 침범 감시**         
  MMU의 특권 명령은 운영체제만 바꿀 수 있음
  
#### CPU 보호

한 사용자가 CPU 시간을 독점하여 다른 사용자가 실행 못하는 문제 방지         
> **Timer을 통한 강제 타이머 인터럽트**       
인터럽트를 통해 운영체제가 다른 프로그램으로 강제 전환한다.

## 운영체제 서비스

> 프로세스 관리      
  주기억장치 관리      
  파일 관리      
  보조기억장치 관리     
  입출력장치 관리       
  네트워킹      
  보호
  
### 프로세스 관리

프로세스 : 메모리에서 실행 중인 프로그램

- 프로세스의 생성, 소멸
- 프로세스 활동 일시 중지, 활동 재개
- 프로세스간 통신
- 프로세스간 동기화
- 교착상태 처리

### 주기억장치 관리

- 프로세스에게 메모리 공간 할당
- 메모리의 어느 부분이 어느 프로세스에 할당되었는가 추적, 감시
- 프로세스 종료 시 메모리 회수
- 메모리의 효과적 사용
- 가상 메모리 : 물리적 실제 메모리보다 큰 용량 작업 수행

### 파일 관리

파일 : Track/Sector로 구성된 디스크의 논리적 관점 접근

- 파일의 생성, 삭제
- 디렉토리(=폴더)의 생성, 삭제
- 기본동작 지원 : open, close, read write, create, delete
- Track/Sector-file 간의 매핑
- 백업

### 보조기억장치 관리

- 빈 공간 관리
- 저장공간 할당
- 디스크 스케쥴링 : 데이터 읽는 시간 단축

### 입출력장치 관리

- 장치 드라이브
- 입출력장치 성능향상

### 시스템 콜

운영체제 서비스를 받기 위한 호출

> **Process**    
  end, abort, load, execute, create, terminate, get/set, atributes, wait event, signal event      
  **Memory**       
  allocate, free       
  **File**        
  create, delete, open, close, read, write, get/set atributes    
  **Device**    
  request, release, read, write, get/set atributes, atach/detache devices       
  **Information**      
  get/set ime, get/set system data     
  **Communication**     
  socket, send, receive
  
  # 프로세스 관리
  
  CPU 자원을 효과적으로 나누는 방법      
  프로세스가 실행되는 동안 text(code), data, stack, pc, register 등의 값이 변화
  
  **프로세스 상태**
  > **new** : 보조기억장치에서 메모리로 올라온 상태    
    **ready** : 메모리에서 초기화 진행 후 실행 준비 완료된 상태    
    **running** : 실제 동작     
    **waiting** : 다른 프로세스 진행 과정 동안 기다림(다시 running)      
    **terminated** : 프로세스 종료
    
  > Multiprogramming System : running -> waiting       
    Time-Sharing System : running -> waitting or ready
  
**PCB(Process Control Block)**

프로세스에 대한 모든 정보 (프로세스 상태, PC, register, CPU time ...)      
프로세스 상태 결정을 위해 참조하는 자료

## Queues

프로세스가 다음 과정을 위해 자신의 순서를 기다리는 과정

> **job Queue** : 보조기억장치 -> 메모리      
  - Job scheduler : 메모리 적재 순서 결정      
  프로세스가 끝날때까지 기다려야 하므로 Long-term scheduler이라고도 부름 
> **Ready Queue** : 메모리 -> CPU      
  - CPU scheduler : CPU 서비스 사용 순서 결정        
  프로세스 상태가 끝날때까지 기다려야 하므로 Short-term schduler이라고도 부름
> **Device Queue** : 주변기기 사용 
  - Device scheduler : 주변기기 사용 순서 결정

## Multiprogramming

멀티프로그래밍의 정도는 메모리에 적재되는 프로세스의 수에 영향        
전체 프로세스가 하는 일의 종류에 의해 멀티프로그래밍의 종류 결정
> **I/O bound process**      
  주로 디바이스 동작 (예: word)
  **CPU bound process**     
  계산량이 많은 동작 (예: 일기예보)

### Mudium-term scheduler

메모리에 적재된 프로그램들 중 Swapping 순서 결정

**Swapping**      
메모리에 있지만 작업을 수행하지 않는 프로그램을 보조기억장치로 보냄
> **Swap in** : Swapping된 프로그램을 다시 메모리로 가져옴       
  **Swap out** : 메모리에 적재된 프로그램을 보조기억장치로 보냄

### Context switching (문맥전환)

프로세스를 진행 중 프로세스를 다른 프로그램으로 바꿔서 실행하는 것

> **Scheduler** : Ready Queue 상태의 프로그램 CPU 서비스 사용 순서 결정      
  **Dispatcher** : Scheduler가 선택한 프로세서 실행을 위한 값 변환       
  현재 프로세서 : OS에 지금까지 결과 저장     
  다음 프로세서 : 실행 환경 초기화 및 복원             
  **Context switching overhead** : 문맥 전환을 진행하는 동안 발생하는 부담     

## CPU Scheduling

상황에 따라 기존 프로세스를 강제 중지 할 수 있다. 

> **Preemptive(선점)** : CPU 실행 중인 프로세스를 강제 중지하고 Scheduning을 진행하는 것       
  **Non-Preemptive(비선점)** : 프로세스가 끝난 후 Scheduling을 진행하는 것

### Scheduling criteria (성능 척도)
- **CPU Utilization (CPU 이용률)** : CPU의 실제 동작 시간의 비율
- **Throughput (처리율)** : 시간 당 프로그램 처리 개수
- **Turnaround time (반환시간)** : 작업 시작 ~ 작업 종료의 전체 시간
- **Waiting time (대기시간)** : Ready Queue의 시간
- **Response time (응답시간)** : 명령 후 첫 응답이 출력되는 

### CPU Scheduling Algorithms

> **FCFS(First-Come, First-Served)     
  SJF(Shortest-Job-First)      
  Priority      
  RR(Round-Robin)     
  Multilevel Queue      
  Multilevel Feedback Queue**      

#### FCFS(First-Come, First-Served)

먼저 온 프로그램부터 먼저 서비스하는 방식으로 Non-Preemptive Scheduling에 해당한다.    
가장 간단하고 공평한 방법이지만 가장 좋은 방법은 아니다.

---

아래와 같이 3개의 프로세스를 가정해보자.
| Process | Burst Time |
|:-:|:-:|
| P1 | 24 |
| P2 | 3 |
| P3 | 3 |

아래 경우의 Waiting Time은 0+24+27이다.      
| P1 | P2 | P3 |
|:-:|:-:|:-:|
| 24 | 3 | 3 |

아래 경우의 Waiting Time은 0+3+6이다.      
| P2 | P3 | P1 |
|:-:|:-:|:-:|
| 3 | 3 | 24 |

따라서 프로세스가 시작되는 순서에 따라 Waiting time이 달라진다.
**Convey Effect(호위효과)** : Waitiing Time이 긴 프로그램이 앞에 위치하여 뒤에 위치한 프로그램들이 오래 기다리는 상태

#### SJF(Shortest-Job_First)

작업시간이 짧은 프로그램부터 서비스하는 방식으로 Preemptive Scheduling과 Non-Preemptive Scheduling 둘 다 해당한다.        
실제 환경에서는 프로그램의 작업시간을 알 수 없기 때문에 완벽하게 구현할 수 없다.     
프로그램이 실행 되었던 기록을 바탕으로 작업시간을 예측하며 SJF를 구현한다.  

---

아래와 같이 4개의 프로세스를 가정해보자.
| Process | Burst Time |
|:-:|:-:|
| P1 | 6 |
| P2 | 8 |
| P3 | 7 |
| P4 | 3 |

아래와 같이 SJF로 계산하면 Waiting time은 0+3+9+16 = 28이다.
| P4 | P1 | P3 | P4 |
|:-:|:-:|:-:|:-:|
| 3 | 6 | 7 | 8 |

아래와 같이 FCFS로 계산하면 Waiting time은 0+6+14+21 = 41이다. 
| P1 | P2 | P3 | P4 |
|:-:|:-:|:-:|:-:|
| 6 | 8 | 7 | 3 |

따라서 SJF를 사용하면 Waiting time을 최소화할 수 있다.      

---

아래와 같이 4개의 프로세스를 가정하고 SJF의 Preemptive Scheduling과 Non-Preemptive Scheduling을 구현해보자
| Process | Burst Time | Arrival Time |
|:-:|:-:|:-:|
| P1 | 8 | 0 |
| P2 | 4 | 1 |
| P3 | 9 | 2 |
| P4 | 5 | 3 |

**Non-Preemptive Scheduling**

| P1 | P2 | P4 | P3 |
|:-:|:-:|:-:|:-:|
| 8 | 4 | 5 | 9 |

Arrival Time(도착지연시간)이 없는 P1부터 시작하고, Waiting time은 0+8+12+19=39

**Preemptive Scheduling**

| P1 | P2 | P2 | P2 | P3 | P1 | P4 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 1 | 1 | 1 | 2 | 5 | 7 | 9 |

Arrival Time에 의해 P1이 먼저 시작하고 1초 후 P1보다 작동시간이 작은 P2를 실행한다.      
P3,P4에 정해진 Arrival Time이 끝나도 P2보다 작동시간이 크기 때문에 P2를 실행한다.     
P2 종료 후 P3, P4와 남은 P1을 SJF 방식으로 진행한다.     

**Priority Scheduling**

우선순위가 높은 프로그램부터 서비스하는 방식으로 Preemptive Scheduling과 Non-Preemptive Scheduling 둘 다 해당한다.     
> **Priority(우선순위)** : 정수로 표시하며 숫자가 작을수록 우선순위 높음
  Internal(내부적 요소) : time limit, memory requirement, i/o to CPU burst …
  External(외부적 요소) : amount of unds being paid, politcal factors …
  
> Starvation : 계속 프로그램들이 메모리로 적재되기 때문에 우선순위가 낮은 프로그램은 작동 못하는 문제        
  Againg : 프로그램이 메모리에 적재되어있는 시간에 비례하여 우선순위에 가산점을 주는 방식

---

아래와 같이 4개의 프로세스를 가정해보자.
| Process | Burst Time | Priority |
|:-:|:-:|:-:|
| P1 | 10 | 3 |
| P2 | 1 | 1 |
| P3 | 2 | 4 |
| P4 | 5 | 2 |

Priority Scheduling 방식으로 계산하면 아래와 같다. 

| P2 | P4 | P1 | P3 |
|:-:|:-:|:-:|:-:|
| 1 | 5 | 10 | 2 |

#### Round-Robin

**Time Quantum(=Time Slice)** 를 통해 원형의 순서를 지정하고, 이 순서대로 서비스하는 방식이다.    
Time Quantum이 프로세스 중 가장 동작시간이 긴 프로그램보다 길게 설정하면 FCFS와 같게된다. 
Time Quantum이 작으면 Switching overhead가 발생한다. 

---

아래와 같은 3개의 프로세스를 가정해보자.
| Process | Burst Time |
|:-:|:-:|
| P1 | 24 |
| P2 | 2 |
| P3 | 3 |

Time Quantum이 1인 RR로 계산하면 아래와 같이 Waiting time은 8+7+4=19
| P1 | P2 | P3 | P1 | P2 | P3 | P1 | P3 | P1 |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| 1 | 1 | 1 | 1 | 1 | 1 | 1 | 1 | 21 |

Time Quantum이 3인 RR로 계산하면 아래와 같이 Waiting time은 8+0+0=8
| P1 | P2 | P3 | P1 |
|:-:|:-:|:-:|:-:|
| 3 | 2 | 3 | 21 |
   
따라서 Time Quantum에 의해 성능이 결정된다. 

