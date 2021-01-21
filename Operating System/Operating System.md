# 운영체제

컴퓨터 하드웨어를 잘 관리하여 *성능*을 높이고 사용자에게 *편의성*을 제공하는 컴퓨터 하드웨어 관리 프로그램 <br>
`하드웨어 < 운영체제 (Kernel < Shell) < 애플리케이션`
> **Kernel** : 하드웨어 관리 <br>
  **Shell** : 사용자 명령 해석

**부팅**
> **1. POST를 실행** <br>
  컴퓨터 하드웨어 상태 확인 (프로세서 - 메모리(ROM, RAM) - 보조기억장치) <br>
  **2. Boot loader 실행** <br>
  보조기억장치에 있는 OS를 RAM으로 옮겨옴 <br>
  컴퓨터가 종료 될 때까지 상주(Resident)한다. 

## 역사

1940s 컴퓨터 개발
입력장치 - 메모리 - 프로세서 - 출력장치

+ 운영체제

Batch Processing System (일괄처리)
연속되는 과정을 메모리에 저장 -> 운영 과정 단순화
*Resident Monitor : 최초의 운영체제*

+ 보조기억장치

Multiprogramming System (다중프로그래밍)
느린 하드웨어로 인한 CPU 작업 중지(Idle) -> 메모리에 여러 프로그램 
*CPU scheduling, 메모리 관리 및 보호 필요*
