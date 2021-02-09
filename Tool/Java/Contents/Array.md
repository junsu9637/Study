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

앞서 언급했듯이 배열은 한번 생성하면 길이를 변경할 수 없기 때문에 더 많은 저장공간이 필요하다면 보다 큰 배열을 새로 만들고 이전 배열로부터 내용을 복사해야한다. 복사 방법은 for 문을 사용한 방법과 System.arraycopy()를 사용하는 방법 2가지가 있다.

### for

```Java
// 배열 array와 타입이 같고 길이가 2배 긴 tmp 배열을 정의한다.
int[] array = new int[5];
int[] tmp = new int[array.length*2];

// for 문을 이용해서 array의 모든 요소에 저장된 값을 하나하나 tmp에 복사한다.
for (int i; i < array.length; i++)
    tmp[i] = array[i];
    
// 변수 tmp에 저장된 값을 변수 array에 저장하여 array와 tmp가 같은 배열을 가리키게 만든다.
array = tmp; 
```

### System.arraycopy()

```Java
int[] array = new int[5];
int[] tmp = new int[array.length*2];

System.arraycopy(array, 0, tmp, 0, array.length);
    
// 변수 tmp에 저장된 값을 변수 array에 저장하여 array와 tmp가 같은 배열을 가리키게 만든다.
array = tmp; 
```

System.arraycopy(array, 0, tmp, 1, array.length)를 통해 System.arraycopy()를 살펴보면 `array[0]부터 array.length개의 데이터를 tmp[1]를 시작점으로 복사한다.`와 같은 작업을 수행한다.


## Utilization of Array

배열은 다음과 같이 여러가지 방법으로 활용할 수 있다.

### 총합과 평균
```Java
class ArrayEx1
{
    public static void main(String[] args)
    {
        int sum = 0 // 총합 저장 변수
        float average = 0f // 평균 저장 변수
        
        int[] array = {1,2,3,4,5}
        
        for (int i=0; i < array.length; i++)
        {
            sum += array[i]; // 배열의 총합 저장
        }
        
        average = sum / (float)array.length; // 배열의 평균 저장
    }
}
```

### 최대값과 최소값

```Java
class ArrayEx2
{
    public static void main(String[] args)
    {
        int[] array = {1,2,3,4,5}
        
        int max = array[0] // 배열의 첫 번째 값으로 초기화
        int min = array[0] // 배열의 첫 번째 값으로 초기화
        
        for (int i=1; i < array.length; i++)
        {
            if (array[i] > max)
            {
                max = array[i] 
            }
            else if (array[i] < min)
            {
                min = array[i] 
            }
        }
        
    }
}
```

### 섞기

```Java
class ArrayEx3
{
    public static void main(String[] args)
    {
        int[] array = new int[10];
        
        for (int i=0; i < 100; i++)
        {
            int n = (int)(Math.random()*10) // 0~9 중 하나의 임의의 값
            
            // array[0]과 array[n] 값 변경
            int tmp = array[0];
            array[0] = array[n];
            array[n] = tmp
        }
    }
}
```

### 랜덤하게 배열 채우기

```Java
class ArrayEx4
{
    public static void main(String[] args)
    {
        int[] array = new int[10];
        
         for (int i=0; i < array.length; i++)
         {
             array[i] = (int)(Math.random()*10) // 0~9 중 하나의 임의의 값
         }
    }
}
```

### 정렬

```Java
class ArrayEx5
{
    public static void main(String[] args)
    {
        // 배열을 랜덤하게 초기화
        int[] array = new int[10];
        
        for (int i=0; i < array.length; i++) 
        {
            array[i] = (int)(Math.random()*10) // 0~9 중 하나의 임의의 값
        }
        
        // 정렬
        for (int i=0; i < array.length-1; i++)
        {
            boolean changed = false; // 자리바꿈이 발생했는지 확인을 위한 변수 선언
            
            for (int j=0; j < array.lenght-1-i; j++)
            {
                // 뒤의 값이 작으면 서로 변경
                if(array[j] > array[j+1])
                {
                    int tmp = array[j];
                    array[j] = array[j+1];
                    array[j+1] = tmp
                    changed = true;
                }
            }
            
            if (!changed) break; // 자리바꿈이 없으면 반복문 종료
        }
    }
}
```

### 빈도수

```Java
class ArrayEx6
{
    public static void main(String[] args)
    {
        int array = new int[10];
        int counter = new int[10];
        
        for (int i=0; i < array.length; i++)
        {
            array[i] = (int)(Math.random() * 10) // 배열을 0~9로 초기화
        }
        
        for (int i=0; i < array.length; i++)
        {
            counter[array[i]]++;
        }
    }
}
```

# String Array

## Declaration and Creation of String Array

문자열 타입의 원소를 담는 배열은 다음과 같이 생성된다.
```Java
String[] array_name = new String[ARRAY_SIZE]
```

## Initialize of String Array

다음과 같이 String 배열은 일반 배열과 초기화 과정이 같다.

```Java
String[] array = new String[3];
array[0] = "juk";
array[1] = "yeo";
array[2] = "jwo";

```

```Java
String[] array = new String[]{ "juk", "yeo", "jwo" };
```

## char Array and string Class

string 클래스는 char 배열에 여러가지 기능을 추가해서 확장한 클래스다. 따라서 다음과 같이 기능을 수행하는 여러 메서드가 존재한다.

| 메서드 | 설명 |
|:-:|:-:|
| char charAt(int index) | 문자열에서 해당 위치(index)에 있는 문자 반환 |
| int length() | 문자열의 길이 반환 |
| String substring(int from, int to) | 문자열에서 해당 범위(from~to)에 있는 문자열 반환 |
| boolean equals(Object obj) | 문자열의 내용이 obj와 같은지 확인한다. 같으면 true, 다르면 false 반환 |
| char[] toCharArray() | 문자열을 문자배열로 변환해서 반환 |

2.4 커맨드 라인을 통해 입력받기](#receive-input-via-command-line)

3. 다차원 배열](#multi-dimensional-array)
3.1 2차원 배열의 선언과 인덱스](#declaration-and-creation-of-two-dimensional-array)
3.2 2차원 배열의 초기화](#initialize-of-two-dimensional-array)
3.3 가변 배열](#variable-array)
3.4 다차원 배열의 활용](#utilization-of-multi-dimensional-array)







