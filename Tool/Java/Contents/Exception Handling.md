[1. 예외처리](#excetion-handling)          
[1.1 프로그램 오류](#program-error)                           
[1.2 try-catch 문](#try-catch)                
[1.3 예외 발생과 catch 블록](#exception-occurrence-and-catch-block)             
[1.4 예외 발생시키기](#exception-occurrence)              
[1.5 메서드에 예외 선언](#declare-exception-to-method)              
[1.6 finally 블록](#finally-block)             
[1.7 try-with-resources 문](#try-with-resources)             
[1.8 사용자정의 예외 만들기](#create-custom-exception)             
[1.9 예외 되던지기](#exception-re-throwing)                     

# Excetion Handling

## Program Error

프로그램이 실행 중 오작동을 하거나 비정상적인 종료를 했을 때, 이런 결과를 초래하는 원인을 **에러**라고 한다. 에러는 발생시점에 따라 '컴파일 에러'와 '런타임 에러'로 나뉜다. 그리고 '논리적 에러'도 존재하는데 이들은 다음과 같이 정의된다.

> **컴파일 에러** : 컴파일 시 발생하는 에러           
  **런타임 에러** : 실행 시 발생하는 에러           
  **논리적 에러** : 실행은 되지만 의도와 다르게 동작하는 경우

이 중 런타임 에러를 방지하기 위해서는 프로그램 실행 중 발생할 수 있는 모든 경우의 수를 고려하여 이에 대한 대비를 하는 것이 필요하다. 이렇게 발생할 수 있는 경우의 수는 다음과 같이 **에러**와 **예외**로 구분할 수 있다. 에러가 발생하면 프로그래머가 할 수 있는 방법이 없지만, 예외는 발생하더라도 프로그래머가 적절한 코드를 미리 작성해 놓는다면 해결할 수 있다.

> **에러** : 프로그램 코드에 의해서 수숩될 수 없는 오류          
  **예외** : 프로그램 코드에 의해서 수습될 수 있는 오류

## Try-Catch

**예외 처리**란 프로그램 실행 시 발생할 수 있는 예외의 발생에 대한 코드를 미리 작성해 놓는 것을 말한다. 예외 처리를 위해서는 다음과 같은 try-catch 문을 사용한다.
```Java
try {// 예외가 발생할 가능성이 있는 문장}
catch (Exception1 e1) 
{ 
    // Exception1이 발생했을 경우, 이를 처리하기 위한 문장 
}
catch (Exception2 e2) 
{ 
    // Exception2이 발생했을 경우, 이를 처리하기 위한 문장 
}
```

## Exception Occurrence and Catch Block)

예외가 발생되면 catch 문은 다음과 같이 실행된다. 다음 코드는 예외 종류를 파악하고 그에 따른 예외처리를 진행하는 작업을 수행한다.
```Java
class Ex
{
    public static void main(String args[])
    {
        System.out.println(1);
        System.out.println(2);
        
        try 
        {
            System.out.println(3);
            System.out.println(0/0); // 예외 발생
            System.out.println(4); // 실행되지 않음
        }
        catch (ArithmeticException ae)
        {
            if (ae instanceof ArithmeticException)
            {
                System.out.println("ArithmeticException")
            }
        }
        System.out.println(5)
    }
}
// 1
// 2
// 3
// ArithmeticException
// 5
```

위와 같은 작업 외에도 다음과 같은 메서드를 통해 다양한 작업을 진행할 수 있다.

| 메서드 | 특징 |
|:-:|:-|
| printStackTrace() | 예외발생 당시의 호출스택에 있었던 메서드의 정보와 예외 메시지를 화면에 출력 |
| getMessage() | 발생한 예외 클래스의 인스턴스에 저장된 메시지를 얻는다. |

## Exception Occurrence

프로그래머는 'throw'를 사용해서 고의적으로 예외를 발생시킬 수 있다.
```Java
class Ex
{
    public static void main(String args[])
    {
        try
        {
            Exception e = new Exception("고의로 발생");
            throw e;
            // 위 두 코드를 throw new Exception("고의로 발생"); 으로 줄일 수 있음
        }
        catch (Exception e)
        {
            System.out.println(e)
        }
        System.out.println("프로그램 종료");
    }
}
// 고의로 발생
// (에러 문구)
// 프로그램 종료
```

## Declare Exception to Method)

메서드에서 예외를 선언하는 방법은 다음과 같다.
```Java
void Method() throws Exception1, Exception2, ... {} 
```
```Java
class Ex
{
    public static void main(String args[])
    {
        try
        {
            Method{};
        }
        catch (Exception e)
        {
            System.out.println(1);
        }
    }
    static void Method() throws Exception
    {
        throw new Exception();
    }
}
// 1
// (Method에서 에러 발생 메시지)
// (main에서 에러 발생 메시지)
```

## Finally Block

finnaly 블록은 예외 발생 여부에 관계없이 실행되어야할 코드를 포함시키기 위해 사용된다. 다음과 같이 try-catch문의 끝에 덧붙여서 사용할 수 있고, try-catch-finally 순서로 코드가 진행된다.
```Java
try {}
catch(Exception1 e1) {}
finally {}
```

## Try with Resources

try-with-resorce문은 try-catch문이 변형되어 만들어졌다. try-with-resorce문은 입출력 장치가 사용되는 클래스 중에서 사용한 후 사용한 입출력 자원을 반환하기 위해 사용한다. 
```Java
try {}
catch(IOException1 ie) {}
finally {}
```

## Create Custom Exception

지금까지는 Java에서 지정한 예외처리 명령어를 사용해서 예외를 처리했다. 기존에 정의 된 예외 클래스 외에도 다음과 같이 사용자지정 예외 클래스를 정의할 수 있다.
```Java
class MyException extends Exception
{
    MyException(String a)
    {
        super(a) // 조상 Exception 클래스 생성자 호출
    }
}
```

## Exception re-Throwing

한 메서드 내에서 여러 예외가 발생할 수 있다. 하지만 try-catch문을 통해서 모든 에러를 다 처리하지 못할 수 있다. 이를 해결하기 위해서 예외 던지기를 사용한다. **예외 되던지기**는 예외를 처리한 후 인위적으로 다시 예외를 발생시키는 것을 의미한다. 이를 통해 발생한 예외를 모두 처리할 수 있게 된다. 예외 되던지기는 다음과 같이 작성한다.
```Java
class Ex
{
    public static void main(String args[])
    {
        try { Method(); }
        catch (Exception e)
        {
            System.out.println("main 메서드 예외처리 완료")
        }
    }
    
    static void Method() throw Exception
    {
        try { throw new Exception(); }
        catch (Exception e)
        {
            System.out.println("Method 메서드 예외처리 완료")
            throw e; // 예외 다시 발생
        }
    }
}
// main 메서드 예외처리 완료
// Method 메서드 예외처리 완료
```
