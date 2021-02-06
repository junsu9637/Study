[서론](#introduction)         
[1. 불 논리](https://github.com/junsu9637/Study/blob/main/Computing%20System/The%20Elements%20Computing%20Systems/Contents/Boolean%20Logic.md#multi-bit-version-of-the-basic-gate)     
[2. 불 연산](https://github.com/junsu9637/Study/blob/main/Computing%20System/The%20Elements%20Computing%20Systems/Contents/Boolean%20operations.md)           
[3. 순차 논리](https://github.com/junsu9637/Study/blob/main/Computing%20System/The%20Elements%20Computing%20Systems/Contents/Sequential%20Logic.md)            
4. 기계어               
5. 컴퓨터 아키텍쳐            
6. 어셈블러              
7. 가상 머신의 스택 산술            
8. 가상 머신의 프로그램 제어             
9. 고수준 언어               
10. 컴퍼일러의 구문 분석             
11. 컴파일러의 코드 생성             
12. 운영체제             
13. 추가 내용             
부록 A. 하드웨어 기술 언어              
부록 B. 테스트            

# Introduction

컴퓨터 과학 전공생들이 나무만 보고 숲을 놓치는 경우가 많다. 보통 추상화, 인터페이스, 실제 구현을 통해 하드웨어와 소프트웨어 시스템의 전체 그림을 그려볼 여유도 없이 바로 프로그래밍, 이론, 엔지니어링 과목을 수강하게 된다. 그렇게 때문에 대부분의 학생들은 복잡하고 규모가 큰 시스템에서 컴퓨터가 어떤 일을 진행하는지 잘 모른다는 느낌을 많이 받는다.

그래서 이 문서는 컴퓨터 시스템의 기본 논리 게이트부터 시작해서 컴퓨터 시스템을 설계해본다. 뿐만 아니라 대규모 하드웨어 및 소프트웨어 개발 프로젝트를 계획하는 방법을 설명한다. 이 문서에 포함되어 있는 내용은 다음과 같다. 

> **하드웨어**      
  논리 게이트 / 불 산술 / 멀티플렉서 / 플립플롭 / 레지스터 / RAM / 카운터 / HDL / 칩 시뮬레이션
  
> **아키텍쳐**      
  ALU,CPU 설계 / 기계어 코드 / 어셈블리 언어 프로그래밍 / 주소 지정 방식 / 메모리 매핑
  
> **운영체제**      
  메모리 관리 / 수학 라이브러리 / 기본 IO드라이버 / 스크린 관리 / 파일 관리 / 고수준 언어 지원
  
> **컴파일러**       
  어휘 분석 / 하향식 파싱 / 기호 테이블 / 가상 스택 기반 기계 / 코드 생성 / 배열 및 객체 구현
  
> **데이터 구조 및 알고리즘**        
  스텍 / 해시 테이블 / 리스트 / 재귀 / 산술 알고리즘 / 기하학적 알고리즘 / 실행시간 고려
  
> **소프트웨어 공학**         
  모듈식 설계 / 인터페이스 구현 페러다임 / API 설계 및 문서화 / 사전 테스트 계획 / 대규모 프로그래밍 / 품질 보증
  
## 구성

본 문서의 구성은 다음과 같다. 

![0.1](https://github.com/junsu9637/Study/blob/main/Computing%20System/The%20Elements%20Computing%20Systems/Image/0.1.png?raw=true)







  
