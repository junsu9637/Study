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

## 운영체제의 역사

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
  
---
---
  
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
  
---  
---  
  
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

## Process 생성

프로세스는 프로세스에 의해 만들어진다        
**init** : OS가 시작될 때 만드는 최초의 프로세스              
**PID(Process Identifier)** : OS가 프로세서에 지정하는 고유번호          

## Process 종료

해당 프로세스가 가졌던 모든 자원을 OS에 반납          

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

---
---

# CPU Scheduling

상황에 따라 기존 프로세스를 강제 중지 할 수 있다. 

> **Preemptive(선점)** : CPU 실행 중인 프로세스를 강제 중지하고 Scheduning을 진행하는 것       
  **Non-Preemptive(비선점)** : 프로세스가 끝난 후 Scheduling을 진행하는 것

## Scheduling criteria (성능 척도)
- **CPU Utilization (CPU 이용률)** : CPU의 실제 동작 시간의 비율
- **Throughput (처리율)** : 시간 당 프로그램 처리 개수
- **Turnaround time (반환시간)** : 작업 시작 ~ 작업 종료의 전체 시간
- **Waiting time (대기시간)** : Ready Queue의 시간
- **Response time (응답시간)** : 명령 후 첫 응답이 출력되는 

## CPU Scheduling Algorithms

> **FCFS(First-Come, First-Served)     
  SJF(Shortest-Job-First)      
  Priority      
  RR(Round-Robin)     
  Multilevel Queue      
  Multilevel Feedback Queue**      

### FCFS(First-Come, First-Served)

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

### SJF(Shortest-Job_First)

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

### Round-Robin

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

### Multilevel Queue Schduling

Quaue를 한개가 아닌 여러개를 동시에 진행한다.
> 각각의 Quaue에 절대적 우선순위 지정 
  CPU time을 각 Quaue에 차등분배
  각 Quaue에 독립된 Scheduming

프로세스는 여러 종류가 있고, 필요한 업무 조건이 다르다.
> system Processes : OS가 하는 프로세스
  Interactive Processes : 사용자외의 대화형 프로세스
  Interactive Editing Processes : 편집기능의 대화형 프로세스
  Batch Processes : 일괄 처리 프로세스
  Student Processes

### Multilevel *Feadback* Queue Schduling

특정 상태의 Quaue를 다른 Quaue로 점직적으로 이동시킨다.
> 많은 CPU time 사용 시 다른 Quaue로 이동
  기아 상태 우려 시 우선순위 높은 Quaue로 이동

---
---

# Thread

프로그램 내부의 흐름으로 한 프로세스는 1개 이상의 쓰래드를 가져야하한다.           
> 쓰래드 구조
  - Stack을 제외한 프로세스의 메모리 공간 공유 (Code, Data)        
  - 프로세스의 자원 공유 (File, I/O ...)          
  - 비공유 : 개별 PC, Stack Pointer, Registers, Stack

## MultiThread

한 프로그램에 2개 이상의 쓰래드가 있는 상태로 쓰래드가 짧은 시간 간격으로 스위칭된다.           
여러 쓰래드가 동시에 실행되는 것처럼 보인다.       
> Concurrent : 한 번에 한 동작만 진행하지만 빠른 스위칭으로 동시에 작업을 수행하는 것처럼 보이는 상태              
  Simultaneous : 동시에 여러 작업을 수행하는 상태

---
---

# Proces Synchronization(프로세스 동기화)

공유 데이터의 동시 접근 문제를 해결하기 위해 프로세스를 순차적으로 실행하여 데이터 일관성을 유지한다.             
틀린 답이 나오지 않도록 임계구역 문제를 해결해야한다. -> Mutual exclusion         
원하는대로 프로세스 실행 순서를 제어해야한다. -> Ordering    

**임계구역 문제** : 여러 쓰래드가 공통변수에 동시 업데이트를 진행하여 생기는 시간 지연            

> Independent Process : 같은 시스템 내의 다른 프로그램과 아무런 관계도 없는 프로세스          
  Coperating Process : 같은 시스템 내의 다른 프로그램과 영향을 주고 받는 프로세스

## The Critcal-Section Problem(임계구역 문제)

여러개의 쓰래드로 이루어진 시스템에서 여러 쓰래드가 공통변수에 동시 업데이트를 진행하는 문제
Critical Section(임계구역) : 각 쓰래드 내부에 있는 쓰레드가 공통 변수를 변경할 수 있는 코드 영역

> Mutual exclusion (상호배타) : 임계구역에는 한 번에 한 쓰래드만 진입해야 한다.             
  Progres (진행): 어떤 쓰래드가 먼저 진입할 것인가        
  Bounded waitng (유한대기): 어느 쓰레드라도 유한 시간 내에 들어갈 수 있다.             


## Synchronization Tools(동기화 도구)

> Semaphores     
  Monitors      
  Misc     

### Semaphores

동기화 문제 해결을 위한 소프트웨어 도구 (Mutual exclusion, Ordering 등에 사용)
구조 : 정수형 변수 + P 동작 + V 동작

> P 동작 : acquire() 정수값 검사를 통한 프로세스 감금
  ```Java
  void acquire()
  {
     value--;
     if(value < 0)
     {
        add this process/thread to list;
        block;
     }
  }
  ```
> V 동작 : release() 정수값 증가를 통한 프로세스 복귀        
  ```Java
  void release() 
  {
     value++;
     if(value <= 0)
     {
        remove a process P from list;
        wakeup P;
     }
  }
  ```
---

#### Mutual exclusion
세마포를 이용하여 임계구역에 sem.value 수만큼의 쓰래드만 접근하게 하여 지연시간에 관계없이 정확히 동작             
sem.value = 1 (*1개의 쓰래드만 접근 가능*)        
| sem. acquire() |
|:-:|
| *Critical-Section* |
| sem.release() |

```markdown
1. P1이 실행되면서 acquire() 실행 -> sem.value = 0           
2. P1이 끝나기 전에 스위칭            
3. P2가 실행되기 위해 acquire()을 실행하지만 sem.value로 인해 잡힘           
4. P1이 끝나면서 release() 실행 -> sem.value = 1         
5. P2 실행
```

#### Ordering
프로세스 실행 순서 제어           
sem.value = 0
| P1 | P2 |
|:-:|:-:|
|| sem.acquire() |
|S1|S2|
|sem.release()||

```markdown
1. P2가 실행되기 위해 acquire() 실행하지만 sem.value로 인해 잡힘        
2. P1 실행         
3. P1이 끝나면서 release() 실행 -> sem.value = 1          
4. P2 실행           
```

### Monitor

세마포 이후에 생긴 프로세스 동기화 도구(세마포보다 고수준의 개념)

**구조**
> 공유자원 + 공유자원 접근함수
  2개의 Queue : 상호배타 + 조건동기

```markdown
1. 공유자원 접근함수에는 최대 1개의 쓰레드만 접근
2. 진입 쓰레드가 조건동기로 블록되면 새 쓰레드 집입 가능
3. 새 쓰레드는 조건동기로 블록된 쓰레드를 깨울 수 있음
4. 깨워진 쓰레드는 현재 쓰래드가 나가면 재진입 가능
```

#### Mutual exclusion

| synchronized { |
|:-:|
| Critical-Section |
| } |

```markdown
**synchronized()** 를 실행하면 Critical-Section에 한 쓰레드만 접근
```

#### Ordering

| P<sub>1</sub> | P<sub>2</sub> |
|:-:|:-:|
| | wait(); |
| S<sub>1</sub>; | S<sub>2</sub>; |
| notify(); | |

```markdown
1. P2가 먼저 실행되더라도 wait()으로 인해 실행되지 않음
2. P1 실행 
3. P1이 끝나면서 notify()실행
4. notify()로 인해 P2 
```

---
---

# Clasical Synchronization Problems (전통적 동기화 예제)

> Producer and Consumer Problem(생산자-소비지 문제(유한버퍼 문제))        
  Readers-Writers Problem(공유 데이터베이스 접근)         
  Dining Philosopher Problem(식사하는 철학자 문제)       

## Producer and Consumer Problem

생산자가 데이터를 생산하면 소비자는 그것을 소비
생산 속도와 소비 속도 차이로 인해 발생하는 문제를 해결하기 위해 Bounded Buffer(유한 버퍼) 사용

> **Bounded Buffer**      
  \- 생산된 데이터를 일단 저장           
  \- 생산자 : 버퍼가 가득차면 넣을 수 없다           
  \- 소비자 : 버퍼가 비면 뺄 수 없다          

아래와 같은 문제는 세마포를 통해 해결 가능
> 임계구역에 대한 동시 진입(공통변수 count, buf[])으로 인한 실행 불가, count != 0문제 발생           
  **Busy-wait** : 버퍼가 가득 차거나 비어있으면서 생기는 문제        
  > 생산자 : empty.acquire() - 빈 공간 기다림        
    소비자 : full.acquire() - 가득 차 있는 공간 기다림         

Bounded Buffer 생성 
```Java
class Buffer
{
   int[] buf;
   int size;
   int count; // Buffer 내부의 생산품 개수
   int in; // 생산품 저장 위치
   int out; // 생산품 추출 위치
   
   Buffer(int size)
   {
      buf = new int[size];
      this.size = size;
      count = in = out = 0;
   }
}
```
Buffer에 데이터 저장
```Java
void insert(int item)  
{
   while(count == size){};
   
   buf[in] = item;
   in = (in+1)%size;
   count++;
}
```
Buffer의 데이터 추출
```Java
void remove(int item) 
{
   while(count == 0){};
   
   int item = buf[out];
   out = (out+1)%size;
   count--;
   return item;
}
```
## Readers-Writers Problem

데이터베이스를 읽기만 하면(Reader) 한 번에 여러 프로세서 접근 가능


> Readers : 데이터베이스를 읽기만 가능
  Writers : 데이터베이스를 읽고 쓰기 가능
  
### The first R/W problem(readers-preference)
Reader에게 데이터베이스 접근 우선권을 부여하는 방식

### The second R/W problem(writers-preference)
Writer에게 데이터베이스 접근 우선권을 부여하는 방식

### The third R/W problem
아무에게도 데이터베이스 접근 우선권을 부여하지 않는 방식

## Dining Philosopher Problem

생각 - 작동 - 생각 - 작동 ... 의 형식으로 진행
Starvation : 교착상태(Deadlock)로 인한 오류로 필요한 자원이 다른 프로세서에 할당되어 있어 프로세스를 실행하지 못함

# Deadlock(교착상태)

어떤 자원은 갖고 있으나 다른 자원은 가지 못해 대기해야하는 상태(자주 일어나지 않음)

**Necessary Conditions(필요조건)** : 아래 4가지를 만족해야지 교착상태 가능
> **Mutual exclusion(상호배타)** : 임계구역에 한 쓰래드만 접근       
  **Hold and Wait(보유 및 대기)** : 자원이 보유되거나 대기        
  **No Preemption(비선점)** : 자원 강제 회수 불가        
  **Circular wait(환형대기)** : 자원이 순환해야 함             

## 교착상태 처리

> Deadlock Prevention (교착상태 방지)
  Deadlock Avoidance (교착상태 회피)
  Deadlock Detection & Recovery (교착상태 검출 및 복구)
  Don't Care (교착상태 무시)

### 교착상태 

교착상태의 4가지 필요조건 중 1개 이상을 방지한다.

#### Mutual exclusion

자원을 공유 가능하게 설정(불가능할 가능성 높음)

#### Hold and Wait

자원을 가지고 있으면서 다른 자원을 기다리지 않게 설정       
자원 활용률 저하, starvation(기아) 발생 가능

#### No Preemption

자원을 선점 가능하게 설정(불가능할 가능성 높음)

#### Circular wait

자원에 번호를 부여하고, 오름차순으로 자원 요청하게 설정             
자원 활용률 저하

### 교착상태 회피

자원 요청에 대한 잘못된 승인을 교착상태라고 정의

**안전한 할당**
총 12개의 자원
| Process | Max needs | Current needs |
|:-:|:-:|:-:|
| P<sub>1</sub> | 10 | 5 |
| P<sub>2</sub> | 4 | 2 |
| P<sub>3</sub> | 9 | 2 |

```markdown
1. P1, P2, P3에 자원을 할당 : 12 - 9 = 3
2. P2에 2개 할당 : 3 - 2 = 1
3. P2가 종료 되면서 사용한 자원 반환 : 1 + 4 = 5
4. P1에 자원 할당 : 5 - 5 = 0
5. P1가 종료 되면서 사용한 자원 반환 : 0 + 10 = 10
6. P3에 자원 할당 : 10 - 7 = 3
7. P3가 종료 되면서 사용한 자원 반환 : 3 + 9 = 12
```

**불안전한 할당**
총 12개의 자원
| Process | Max needs | Current needs |
|:-:|:-:|:-:|
| P<sub>1</sub> | 10 | 5 |
| P<sub>2</sub> | 4 | 2 |
| P<sub>3</sub> | 9 | 3 |

```markdown
1. P1, P2, P3에 자원을 할당 : 12 - 10 = 2
2. P2에 2개 할당 : 2 - 2 = 0
3. P2가 종료 되면서 사용한 자원 반환 : 0 + 4 = 4
4. P1, P3에 할당할 자원 부족
```

### 교착상태 검출 및 복구

교착상태가 일어나는 것을 허용하고 주기적으로 교착상태를 검사한다          
검출 과정에서 계산과 메모리에 추가적인 부담이 가해진다.

**복구**
> 프로세스 일부 강제 종료         
  자원을 선점하여 일부 프로세스에게 할당

### 교착상태 무시

교착상태 발생 시 재시동(거의 사용하지 않)

## Resources(자원)

**Instance** : 동일 형식(type) 자원이 여러 개 있을 수 있다
Request(요청) -> Use(사용) -> Release(반납)의 순서를 진행해야 자원 사용 가능

### Resource Allocation Graph(자원 할당도)

> 자원 : 사각형(개수는 .으로 표시)        
  프로세스 : 원         
  할당 : 화살표        
>> 자원 -> 프로세스 : 할당 됨       
   프로세서 -> 자원 : 요청 
  
> 어떤 자원이 어떤 프로세스에게 할당되었는가          
  어떤 프로세스가 어떤 자원을 할당 받으려고 기다리고 있는가           

# Main Memory Management(주기억장치 관리)

## 메모리의 역사
- Core Memory
- 진공관 메모리
- 트랜지스터 메모리
- 집적회로 메모리 : SRAM, DRAM

메모리의 용량이 증가하고 있지만, 프로그램의 크기도 증가하기 때문에 메모리는 언제나 부족하다.

## 프로그램을 메모리에 적재

프로그램 개발 : Code + Data + Loader
> Source file(원천파일) : 고수준언어 또는 어셈블리언어 (.src)       
  Object file(목적파일) : 컴파일 또는 어셈블 결과 (.oj)         
  Executable file(실행파일) : 링크 결과(다른 라이브러리와 연결) (.exe)          
  
프로그램 개발 관련 도구
> 컴파일러 : 고수준언어로 이루어진 원천파일을 목적파일로 변환          
  어셈블러 : 어셈블리어로 이루어진 원천파일을 목적파일로 변환        
  링커 : 목적파일과 라이브러리를 결합        
  로더 : 실행 파일을 메모리에 적재         
  
## 메모리 낭비 방지

> Dynamic Loading(동적 적재)
  Dynamic Linking(동적 연결)
  Swapping

### Dynamic Loading(동적 적재)

프로그램 실행에 반드시 필요한 루틴/데이터만 적재          
실행 시 필요하면 그때 해당 부분을 메모리에 적재

### Dynamic Linking(동적 연결)

여러 프로그램에 공통적으로 사용되는 라이브러리의 중복 적재 방지

> 라이브러리 루틴 연결을 실행 직전까지 미룸          
  하나의 라이브러리 루틴만 메모리에 적재         
  다른 애플리케이션 실행 시 이 루틴과 연결            

### Swapping

메모리에 적재되어 있으나 현재 사용되지 않고 있는 프로세스 Backing store(=Swap Device)로 몰아냄

## 연속 메모리 할당

프로세스가 생성&종료를 반복하면서 크고 작은 hole들이 만들어짐

**Hole** : 메모리가 비어있는 곳           
**Compaction** : hole을 모으는 과정 (최적 알고리즘 없음)

> first-fit : 처음으로 찾은 메모리가 들어갈 수 있는 공간에 적재           
  Best-fit : 들어갈 수 있는 공간 중에서 메모리 크기가 가장 유사한 공간에 적재
  
### Mamory Fragmentation(메모리 단편화)

**외부 단편화** : hole들이 불연속적으로 존재해서 프로세스 적재 불가능한 상태         
**내부 단편화** : 프로세스 크기가 페이지 크기의 배수가 아니면 마지막 페이지는 한 프레임을 다 체울 수 없는 상태

## Paging(페이징)

프로세스를 일정 크기의 페이지로 잘라서 메모리에 적재

> 프로세스 : page(페이지)의 집합
  메모리 : frame(프레임)의 집합

불연속적인 페이지는 프로세스를 진행할 수 없음
```markdown
1. 프로세스를 페이지 단위로 나눔         
2. CPU가 연속적인 주소로 메모리로 적재 명렬         
3. MMU 내의 재배치 레지스터로 값을 바꿈(MMU = page table, 주소변환)        
4. 적절한 장소로 위치 설정            
5. CPU는 프로세스가 연속된 메모리 공간에 위치한다고 착각
```

### Address Translation(주소 변환)

**Logical address(논리주소)**
CPU가 내보내는 2진수로 표현된 주소          
하위 n 비트 : offset 또는 displacement(변위) -> 페이지 사이즈에 의해 결정(페이지 크기 : 2<sup>n</sup> -> n 비트)         
상위 m-n 비트 : 페이지 번호

**주소변환 (Logical address -> Physical address)(논리주소 -> 물리주소)**

페이지 번호(p) : 페이지 테이블 인덱스 값          
프레임 번호(f) : p에 해당되는 테이블 내용            
변위(d) : 변하지 않음

## Segmentation(세그멘테이션)

프로세스를 논리적인 내용으로 잘라서 메모리에 배치

Segment : 프로세스를 논리적인 내용으로 자른 부분(크기가 동일하지 않음)
```markdown
1. 프로세스를 세그먼트 단위로 나눔         
2. CPU가 연속적인 주소로 메모리로 적재 명렬         
3. MMU 내의 재배치 레지스터로 값을 바꿈(MMU = segment table, 주소변환)        
4. 적절한 장소로 위치 설정            
5. CPU는 프로세스가 연속된 메모리 공간에 위치한다고 착각
```

**주소변환 (Logical address -> Physical address)(논리주소 -> 물리주소)**

세그먼트 테이블 내용 : base + limit
세그먼트 번호(s) : 세그먼트 테이블 인덱스 값 -> 시작 위치 및 한계값 파악

limit를 넘어서면 segment violation 예외 상황 
물리주소 = base[s] + d

# Virtual Memory(가상 메모리)

물리 메모리보다 큰 프로세스를 실행하기 위해 사용하는 방법          
현재 실행에 필요한 부분만 메모리에 올린다.          

## Demand Paging(요구 페이징)

현재 요구되는 페이지만 메모리에 적재하고 나머지는 backing store에 저장

## Page Fault(페이지 부재)

접근하려는 페이지가 메모리에 없는 상태로 Backing store에서 해당 페이지를 가져온다.


### Effective Access Time(유효 접근 시간)

메모리의 평균 접근 시간

***T<sub>eff</sub> = (1-p)T<sub>m</sub> + pT<sub>p</sub>***

*p* : page fault 시간         
*T<sub>p</sub>* = seek time(헤더를 움직이는 시간) + retational delay(원판이 헤더까지 돌아오는 시간) + transfer time(데이터를 읽는 시간)

### Locality of reference(지역성의 원리)

메모리 접근은 시작적, 공간적으로 지역성을 가진다
> **시간적** : 한 번 읽었던 데이터를 다시 읽을 가능성이 있음          
  **공간적** : 현재 읽었던 데이터 주위를 다음에 읽을 가능성이 있음 

**reference** : CPU가 참조하는 주소

# Page Replacement(페이지 교체)

Demand Pageing
```markdown
1. 요구되어지는 페이지만 backing store에서 가져옴
2. 프로그램 실행하면서 요구 페이지가 늘어가면서 메모리가 가득차게됨
3. 어떤 페이지를 backing store로 몰아냄(page-out)
4. 빈 공간에 페이지를 가져온다(page-in)
```

## Victim Page

backing store로 쫓겨난 페이지로 modify 되지 않은 페이지를 선택한다.
modified bit : modify 여부 확인을 위해 추가하는 하나의 비트

## 페이지 교체 알고리즘

> **FIFO(First-In.First-Out)**          
  victim page : 처음 들어온 page 
  **OPT(Optimal)**         
  victim page : 앞으로 가장 오랫동안 사용되지 않을 page (비현실적)         
  **LRU(Least-Recently-Used)**      
  victim page : 최근에 가장 사용되지 않은 page         
  *(최근에 가장 사용되지 않음 = 앞으로 가장 사용되지 않음이라고 가정
  
**page reference string** :  페이지 번호 중 이어지는 번호를 넘긴 페이지 번호

```markdown
CPU가 내는 주소 : 100 101 102 432 612 103 104 611 612           
Page size = 100           
(한번에 100씩 가져오기 때문에 다음과 같이 변환 가능)         
페이지 번호 : 1 1 1 4 6 1 1 6 6           
Page reference string : 1 4 6 1 6
```

**Globla Replacement(전역 교체)** : 메모리 상의 모든 프로세스 페이지 교체           
**Local Replacement(지역 교체)** : 메모리 상의 자기 프로세스 페이지 교체

# Allocation of Frames(프레임 할당)

**Thrashing** : 프로세스 개수가 증가하면 CPU 이용률이 증가하지만 일정 범위를 벗어나면 빈번한 Page in/out으로 인해 CPU 이용률이 감소하는 현상

> Static Allocation(정적 할당)        
>> Equal allocation(균등 할당)         
>> Proportional allocation(비례 할당)         
> Dynamic Allocation(동적 할당)          
>> Working set model           
>> Page fault frequency










