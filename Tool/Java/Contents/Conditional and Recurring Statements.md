[1. 조건문](#conditional-statement)         
[1.1 if 문](#if)          
[1.2 if-else 문](#if-else)          
[1.3 if-else if 문](#if-else-if)           
[1.4 중첩 if 문](#overlay-if)          
[1.5 switch 문](#switch)            

[2. 반복문](#recurring-statement)         
[2.1 for 문](#for)         
[2.2 while 문](#while)        
[2.3 do-while 문](#do-while)        
[2.4 break 문](#break)                     
[2.5 continue 문](#continue)             
[2.6 이름 붙은 반복문](#named-repeating-statement)            

# Conditional Statement

**조건문**은 조건식과 문장을 포함하는 블록{}으로 구성되고, if문과 switch문이 존재한다.

## if

if 문은 가장 기본적인 조건문으로 다음과 같이 이루어져 '만일 조건식이 참이라면 괄호 안의 문장을 수행'한다.
```Java
if (조건식)
{
    // 조건식이 참일 때 수행될 문장
}
```

## if-else

if 문의 변형으로 if문에 else블록을 추가하여 '그 밖에 다른'이라는 의미를 추가했다.
```Java
if (조건식)
{
    // 조건식이 참일 때 수행될 문장
} 
else 
{
    // 조건식이 거짓일 때 수행될 문장
}
```

## if-else-if

if 문의 변형으로 처리해야하는 상황이 셋 이상인 경우 사용한다.
```Java
if (조건식 1)
{
    // 조건식1이 참일 때 수행될 문장
} 
else if (조건식 2) 
{
    // 조건식2이 참일 때 수행될 문장
}
else
{
    // 모든 조건식이 거짓일 때 수행될 문장
}
```

## Overlay-if

if 문의 변형으로 if 문 내에 다른 if 문을 포함시키는 방식이다.
```Java
if (조건식 1)
{
    if (조건식 2) 
    {
        // 조건식 1,2가 모두 참일 때 수행할 문장
    }
    else
    {
        // 조건식 1만 참일 때 수행할 문장
    }
}
else
{
    // 조건식 1,2가 모두 거짓일 때 수행할 문장
}
```

## switch

switch 문은 단 하나의 조건식으로 많은 경우의 수를 처리할 수 있는 방법이다. 따라서 처리할 경우가 많은 경우에는 if 문 보다는 switch 문으로 작성하는 것이 바람직하다. 하지만 switch 문은 다음과 같은 제약조건을 가지고 있어서 항상 사용할 수는 없다.

```markdown
1. switch 문의 조건식 결과는 정수 또는 문자열이어야 한다
2. case 문의 값은 정수, 상수만 가능하고 중복되면 안된다
```

switch 문은 다음과 같은 순서로 연산을 진행한다.

```markdown
1. 조건식을 계산한다
2. 조건식의 결과와 일치하는 case 문으로 이동한다
3. 이후의 문장들을 수행한다
4. break 문이나 switch 문의 끝을 만나면 switch 문 전체를 빠져나간다
```

switch 문은 다음과 같이 작성된다.
```Java
switch (조건식) 
{
    case 값1 : 
        // 조건식의 결과가 값1과 같을 경우 수행될 문장
        break;
    case 값2 : 
        // 조건식의 결과가 값2과 같을 경우 수행될 문장
        break;
    case 값3 : 
        // 조건식의 결과가 값3과 같을 경우 수행될 문장
        break;
    default : 
        // 조건식의 결과와 일치하는 case 문이 없을 때 수행될 문장
}
```

# Recurring Statement

**반복문**은 어떤 작업이 반복적으로 수행되도록 구성하는데 사용한다. 반목문은 for, while, do-while 문이 있다.

## for

for 문은 반복 횟수를 알고 있을 때 사용하기 적합하다. for 문은 다음과 같이 구성된다.
```Java
for (초기화; 조건식; 증감식)
{
    // 조건식이 참일 때 수행될 문장
}
```
```Java
for (int i=1; i<=5; i++)
{
    // 5번 반복
}
```

## while

while 문은 조건식이 거짓이 될 때까지 블록{} 내의 문장을 반복한다. 조건식을 생략하면 에러가 발생한다. 
```Java
while (조건식)
{
    // 조건식의 연산결과가 참인 동안 반복될 문장
}
```

## do-while

while 문의 변형으로 조건식에 관계 없이 한 번의 문장 수행을 보장한다. 
```Java
do
{
    // 조건식의 연산결과가 참인 동안 반복될 문장
} while (조건식);
```

## break

break 문은 자신이 포함된 반복문에서 벗어난다.

## continue

continue 문은 반복문의 끝으로 이동하여 다음 반복으로 넘어간다. continue 문은 반복문 전체를 벗어나지 않고 다음 반복을 계속 수행한다는 점에서 break 문과는 다르다. 예를 들어 중첩 if 문에서 break 문은 전체 중첩 if 문에서 벗어나지만 continue는 특정 if 문에서만 벗어난다.

## Named Repeating Statement

break 문과 continue 문에 이름을 지정하여 하나 이상의 반복을 벗어나거나 건너뛸 수 있다. 

```Java
class Ex
{
    public static void main(String[] args)
    {
        Loop1 : for (int i=2; i<=9; i++)
        {
            for (int j=1; j<=9; j++)
            {
                if(j==5)
                {
                    break Loop1;
                }
                System.out.println(i + "*" + j + "=" + i*j)
            }
        }
        
    }
}
// 2*1=2
// 2*2=4
// 2*3=6
// 2*4=8
```

