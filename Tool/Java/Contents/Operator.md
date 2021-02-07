[1. 연산자](#operator)            
[1.1 연산자와 피연산자](#operator-and-operand)              
[1.2 식과 대입연산자](#expression-and-substitution-operator)             
[1.3 연산자의 종류](#type-of-operator)               
[1.4 연산자의 우선순위와 결합규칙](#priority-and-combination-rules-for-operator)               
[1.5 산술 변환](#arithmetic-transformation)             

[2. 다항 연산자](#polynomial-operator)            
[2.1 증감 연산자](#increasing-and-decreasing-operators)             
[2.2 부호 연산자](#sign-operator)             

[3. 산술 연산자](#arithmetic-operators)            
[3.1 사칙 연산자](#four-pronged-operator)           
[3.2 나머지 연산자](#other-operator)             

[4. 비교 연산자](#comparison-operators)               
[4.1 대소비교 연산자](#consumption-bridge-operator)             
[4.2 등가비교 연산자](#equivalent-comparison-operator)             

[5. 논리 연산자](#logical-operator)           
[5.1 논리 연산자](#logical-operators)            
[5.2 비트 연산자](#bit-operator)            

[6. 그 외의 연산자](#the-other-operator)           
[6.1 조건 연산자](#condition-operators)             
[6.2 대입](#substitution)          


# Operator

## Operator and Operand

> **연산자** : 연산을 수행하는 기호(사칙연산 등)          
  **피연산자** : 연산자의 작업 대상(변수, 상수, 리터럴, 수식 등)

연산자는 피연산자로 연산을 수행하고 나면 항상 결과값을 반환한다.

## Expression and Substitution Operator

연산자와 피연산자를 조합하여 계산하고자하는 바를 표현한 것을 **식**이라고 한다. 그리고 식을 계산하여 결과를 얻는 것을 **평가**한다고 한다.

## Type of Operator

연산자는 연산자의 우선순위로 인해 연산자의 기능과 피연산자의 개수에 의해 분류해야 한다. 

### 연산자의 기능에 의한 분류 

연산자를 기능별로 분류하면 다음과 같다.
| 종류 | 연산자 | 설명 |
|:-:|:-:|:-:|
| 산술 연산자 | +, -, \*, /, %, <<, >> | 사칙연산과 나머지  |
| 비교 연산자 | >, <, >=, <=, ==, != | 크고 작음과 같고 다름을 비교 |
| 논리 연산자 | &&, \|\|, !, &, \|, ^, ~  | AND, OR으로 조건을 연결 |
| 대입 연산자 | = | 우변의 값을 좌변에 저장 |
| 기타 | (type), ?:, instanceof | 형변형 연산자, 삼항 연산자, instanceof 연산자 |

### 피연산자의 개수에 의한 분류

피연산자의 개수로 연산자를 분류하기도 한다. 피연산자가 하나면 '단항 연산자', 피연산자가 두 개면 '이항 연산자'. 피연산자가 세 개면 '삼항 연산자'라고 부른다. 대부분의 연산자는 '이항 연산자'이고, '삼항 연산자'는 오직 '?',':'뿐이다.

## Priority and Combination-Rules for Operator

### 연산자의 우선순위

연산자의 우선순위는 다음과 같다. `단항 연산자 > 이항 연산자`, `산술(곱셈 > 덧셈 > 쉬프트) > 비교 > 논리 > 대입`
```markdown
1. 단항 연산자가 이항 연산자보다 우선순위가 높다.
-x > 3
2. 곱셈과 나눗셈이 덧셈과 뺄셈보다 우선순위가 높다.
x + 3 * y
3. 덧셈과 뺄셈이 쉬프트보다 우선순위가 높다.
x << 2 + 1
4. 비교 연산자보다 산술 연산자가 먼저 수행된다.
x + 3 > y - 2
5. 논리 연산자보다 비교 연산자가 먼저 수행된다.
x > 3 && x < 5
6. 대입 연산자는 연산자 중에서 우선순위가 제일 낮다.
result = x + y * 3;
```

### 연산자의 결합규칙

우선순위가 같은 연산자를 결합하는 방법을 **연산자의 결합규칙**이라고 한다. 결합규칙은 연산자마다 다르고, 다음과 같이 진행된다.
```markdown
1. 왼쪽에서 오른쪽
1 + 2 = 3
2. 오른쪽에서 왼쪽
x = y = 3
```

1.5 산술 변환(#arithmetic-transformation)

2. 다항 연산자(#polynomial-operator)
2.1 증감 연산자(#increasing-and-decreasing-operators)
2.2 부호 연산자(#sign-operator)

3. 산술 연산자(#arithmetic-operators)
3.1 사칙 연산자(#four-pronged-operator)
3.2 나머지 연산자(#other-operator)

4. 비교 연산자(#comparison-operators)
4.1 대소비교 연산자(#consumption-bridge-operator)
4.2 등가비교 연산자(#equivalent-comparison-operator)

5. 논리 연산자(#logical-operator)
5.1 논리 연산자(#logical-operators)
5.2 비트 연산자(#bit-operator)

6. 그 외의 연산자(#the-other-operator)
6.1 조건 연산자(#condition-operators)
6.2 대입(#substitution)
