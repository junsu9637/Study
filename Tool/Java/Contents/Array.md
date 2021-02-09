[1. 배열](#array)             
[1.1 배열이란](#what-is-array)               
[1.2 배열의 선언과 생성](#declaration-and-creation-of-array)           
[1.3 배열의 길이와 인덱스](#length-and-index-of-array)            
[1.4 배열의 초기화](#initialize-of-array)              
[1.5 배열의 복사](#copy-of-array)            
[1.6 배열의 활용](#utilization-of-array)              

[2. String 배열](#string-array)                               
[2.1 String 배열의 선언과 생성](#declaration-and-creation-of-string-array)           
[2.2 String 배열의 초기화](#initialize-of-string-array)             
[2.3 char 배열과 String 클래스](#char-array-and-string-class)            
[2.4 커맨드 라인을 통해 입력받기](#receive-input-via-command-line)               

[3. 다차원 배열](#multi-dimensional-array)               
[3.1 2차원 배열의 선언과 인덱스](#declaration-and-creation-of-two-dimensional-array)             
[3.2 2차원 배열의 초기화](#initialize-of-two-dimensional-array)          
[3.3 가변 배열](#variable-array)          
[3.4 다차원 배열의 활용](#utilization-of-multi-dimensional-array)          

# Array

## What is Array

**배열**은 같은 타입의 여러 변수를 하나의 묶음으로 다루는 방식이다. 여기서 중요한 것은 '같은 타입'이어야 한다는 것이다. 배열은 한번 선언되고 나면 길이를 변경할 수 없다. 배열은 다음과 같이 생성한다.
```Java
type[] array_name = new type[ARRAY_SIZE]; // type 타입의 ARRAY_SIZE 크기의 배열 생성
```

| array |
|:-:|

| array[0] | array[1] | ... | array[ARRAY_SIZE-1] |
|:-:|:-:|:-:|:-:|

## Declaration and Creation of Array

### 배열의 선언
```Java
type[] array_name;
```

| array |
|:-:|

### 배열의 생성
```Java
array_name = new type[ARRAY_SIZE];
```

| array[0] | array[1] | ... | array[ARRAY_SIZE-1] |
|:-:|:-:|:-:|:-:|

## Length and Index of Array

생성된 배열의 각 저장공간을 '배열의 요소'라고 하며 '배열이름[인덱스]'의 형식으로 배열의 요소에 접근한다. **인덱스**는 배열의 요소마다 붙여진 일변번호로 각 요소를 구별하는데 사용한다. 인덱스는 0부터 배열길이-1까지의 범위를 갖는다.

배열은 한 번 선언되고 나면 길이를 변경할 수 없기 때문에 다음과 같은 방법을 거쳐야 배열의 길이를 변경할 수 있다. 
```markdown
1. 더 큰 배열을 새로 생성한다
2. 기존 배열의 내용을 새로운 배열에 복사한다
```

이러한 작업은 메모리 낭비를 야기하기 때문에 처음부터 배열의 길이를 넉넉하게 잡아서 새로운 배열을 생성해야하는 상황을 피해야한다. 만일 용량 부족으로 새로운 배열을 생성하는 경우, 보통 기존의 2배의 길이로 생성한다.


## Initialize of Array

다음과 같은 3개의 방법은 같은 배열 초기화를 진행한다. 
```Java
int[] array = new int[5];
array[0] = 50;
array[1] = 60;
array[2] = 70;
array[3] = 80;
array[4] = 90;
```

```Java
int[] array = new int[5];

for (int i=0; i < array.length; i++)
    array[i] = i*10 + 50;
```

```Java
int[] array = new int[]{ 50, 60, 70, 80, 90 };
```

이렇게 초기화한 배열은 다음과 같이 3가지 방법으로 표현할 수 있다.
```Java
int[] array = new int[]{ 50, 60, 70, 80, 90 };
char[] str = new char[]{ a, b, c };

System.out.printf(array); // I@12345(배열의 주소)

System.out.printf(str); // abc

for (int i=0; i < array.length; i++)
    System.out.printf(array[i] + " ,"); // 50, 60, 70, 80, 90
    
System.out.printf(Array.toString(array)) // [50, 60, 70, 80, 90]
```

위와 같이 배열을 바로 출력하려고 하면 배열의 주소가 출력된다. 주소는 `타입@주소`의 형태로 출력된다. 하지만 char 타입은 예외로 모든 문자가 연결되어 출력된다 

## Copy of Array

1.6 배열의 활용](#utilization-of-array)

2. String 배열](#string-array)
2.1 String 배열의 선언과 생성](#declaration-and-creation-of-string-array)
2.2 String 배열의 초기화](#initialize-of-string-array)
2.3 char 배열과 String 클래스](#char-array-and-string-class)
2.4 커맨드 라인을 통해 입력받기](#receive-input-via-command-line)

3. 다차원 배열](#multi-dimensional-array)
3.1 2차원 배열의 선언과 인덱스](#declaration-and-creation-of-two-dimensional-array)
3.2 2차원 배열의 초기화](#initialize-of-two-dimensional-array)
3.3 가변 배열](#variable-array)
3.4 다차원 배열의 활용](#utilization-of-multi-dimensional-array)







