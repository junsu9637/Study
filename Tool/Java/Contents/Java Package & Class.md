[1. java.lang 패키지](#java-lang-package)        
[1.1 Object 클래스](#object-class)            
[1.2 Srting 클래스](#string-class)                
[1.3 SrtingBuffer클래스와 StringBuilder클래스](#stringbuffer-class-and-stringbuilder-class)                   
[1.4 Math 클래스](#math-class)                              

# Java lang Package

**java.lang 패키지**는 자바프로그래밍에 가장 기본이 되는 클래스들을 포함하고 있다. 그렇기 때문에 java.lang 패키지의 클래스들은 import문 없이 사용 가능하다. 자주 사용하는 메서드들은 아래 정리되어 있다.

## Object Class

| Object 클래스 메서드| 설명 |
|:-|:-|
| protected object clone() | 객체 자신의 복사본 반환 |
| public boolean equals(Object obj) | 객체 자신과 객체 obj각 같은 객체인지 확인 |
| public Class getclass() | 객체 자신의 클래스 정보를 담고 있는 Class 인스턴스 반환 |
| public int hashCode() | 객체 자신의 해시코드 반환 |
| public String toString() | 객체 자신의 정보를 문자열로 변환 |
| public void notify() | 객체 자신을 사용하려고 기다리는 쓰래드를 하나만 깨움 |
| public void notiryAll() | 객체 자신을 사용하려고 기다리는 모든 쓰래드를 깨움 |

## String Class

| String 클래스 메서드| 설명 |
|:-|:-|
| String(String s) | 주어진 문자열(s)을 갖는 String 인스턴스 생성 |
| String(char[] value) | 주어진 문자열(value)을 갖는 String 인스턴스 생성 |
| String(StringBuffer buf) | StringBuffer 인스턴스가 갖고 있는 문자열과 같은 내용의 String 인스턴스 생성 |
| char charAt(int index) | 지정된 위치(index)에 있는 문자를 알려줌 |
| int compareTo(String str) | 문자열(str)과 시전 순서 비교 |
| String concat(String str) | 문자열(str)늘 뒤에 덧붙임 |
| boolean contatins(CharSequence s) | 지정된 문자열(s)이 포함되었는지 검사 |
| boolean endsWith(String suffix) | 지정된 문자열(suffix)로 끝나는지 검사 |
| boolean equals(Object obj) | 매개변수로 받은 문자열(obj)과 String 인스턴스 문자열 비교 |
| boolean equalsIgnoreCase(String str) | 문자열과 String 인스턴스 문자열을 대소문자 구분없이 비교 |
| int indexOf(int ch) | 주어진 문자(ch)가 문자열에 존재하는지 확인하여 위치(index)를 알려줌 |
| int indexOf(int ch, int pos) | 주어진 문자(ch)가 문자열에 존재하는지 지정된 위치(pos)부터 확인하여 위치(index)를 알려줌 |
| int indexOf(String str) | 주어진 문자열이 존재하는지 확인하여 그 위치(index)를 알려줌 |
| String intern() | 문자열을 상수풀에 등록 |
| int lastIndexOf(int ch) | 지정된 문자 또는 문자코드를 문자열의 오른쪽 끝에서부터 찾아서 위치(index)를 알려줌 |
| int lastIndexOf(String str) | 지정된 문자열을 인스턴스 문자열 끝에서부터 찾아서 위치(index)를 알려줌 |
| int length() | 문자열 길이 반환 |
| String replace(char old, char nw) | 문자열 중 문자(old)를 새로운 문자(nw)로 바꾼 문자열 반환 |
| String replace(CharSequence old, CharSequence nw) | 문자열 중 문자열(old)를 새로운 문자열(nw)로 바꾼 문자열 반환 |
| String replaceAll(String regex, String replacement) | 문자열 중 지정된 문자열(regex)과 일치하는 것을 새로운 문자열(replacement)로 모두 변경 |
| String replaceFirst(String reget, String replacement) | 문자열 중 지정된 문자열(regex)과 일치하는 것들 중, 첫번째를 새로운 문자열(replacement)로 변경 |
| String[] split(String regex) | 문자열을 지정된 분리자(regex)로 나누어 분자열 배열에 담아 반환 |
| String[] split(String regex, int limit) | 문자열을 지정된 분리자(regex)로 나누어 지정된 수(limit)개의 분자열 배열에 담아 반환 |
| boolean startsWith(String prefix) | 주어진 문자열(prefix)로 시작하는지 검사 |
| String substring(int begin, int end) | 주어진 시작위치(begin)부터 끝위치(end)까지 포함된 문자열을 반환 |
| String toString() | String 인스턴스에 저장되어 있는 모든 문자열 반환 |
| String toLowerCase() | String 인스턴스에 저장되어있는 모든 문자열을 소문자로 변환하여 반환 |
| String toUpperCase() | String 인스턴스에 저장되어있는 모든 문자열을 대문자로 변환하여 반환 |
| String trim() | 문자열의 왼쪽 끝과 오른쪽 끝에 있는 공백을 없앤 결과를 반환 |
| Static String valueOf() | 지정된 값을 문자열로 변환하여 반환 |

## Stringbuffer Class and Stringbuilder Class

| StringBuffer 클래스 메서드| 설명 |
|:-|:-|
| StringBuffer() | 16문자를 담을 수 있는 버퍼를 가진 StringBuffer 인스턴스 생성 |
| StringBuffer(int length) | 지정된 개수의 문자(length)를 담을 수 있는 StringBuffer 인스턴스 생성 |
| StringBuffer(String str) | 지정된 문자열(str)을 갖는 StringBuffer 인스턴스 생성 |
| StringBuffer append() | 매개변수로 입력된 값을 문자열로 변환하여 StringBuffer 인스턴스가 저장하고 있는 문자열 뒤에 덧붙임 |
| int capacity() | StringBuffer 인스턴스의 버퍼 크기 반환 |
| char cahrAt(int index) | 지정된 위치(index)에 있는 문자 반환 |
| StringBuffer delete(int start, int end) | 지정된 범위(start~end)의 문자 제거 |
| StringBuffer deleteCharAt(int index) | 지정된 위치(index) 문자 제거 |
| StringBuffer insert() | 두 번째 매개변수로 받은 값을 문자열로 변환하여 첫 번째 매개변수 위치에 추가 |
| StringBuffer replace(int start, int end, String str) | 지정된 범위(start~end)의 문자들을 주어진 문자열(str)로 변환 |
| StringBuffer reverce() | StringBuffer 인스턴스에 저장되어 있는 문자열의 순서를 거꾸로 나열 |
| void setCharAt(int index, char ch) | 지정된 위치(index)의 문자를 주어진 문자(ch)로 변경 |
| void setLength(int newLength) | 지정된 길이(newLenght)로 문자열의 길이를 변경 |

## Math Class

| Math 클래스 메서드| 설명 |
|:-|:-|
| static double ads(double a) | 주어진 값의 절댓값 반환 |
| static float ads(float a) | 주어진 값의 절댓값 반환 |
| static int ads(int a) | 주어진 값의 절댓값 반환 |
| static long ads(long a) | 주어진 값의 절댓값 반환 |
| static double ceil(double a) | 주어진 값 올림 |
| static double floor(double a) | 주어진 값 버림 |
| static long round(double a) | 주어진 값 반올림 |
| static long round(float a) | 주어진 값 반올림 |
| static double max(double a, double b) | 주어진 값을 비교하여 큰 값 반환 |
| static float max(float a, float b) | 주어진 값을 비교하여 큰 값 반환 |
| static int max(int a, int b) | 주어진 값을 비교하여 큰 값 반환 |
| static long max(long a, long b) | 주어진 값을 비교하여 큰 값 반환 |
| static double min(double a, double b) | 주어진 값을 비교하여 작은 값 반환 |
| static float min(float a, float b) | 주어진 값을 비교하여 작은 값 반환 |
| static int min(int a, int b) | 주어진 값을 비교하여 작은 값 반환 |
| static long min(long a, long b) | 주어진 값을 비교하여 작은 값 반환 |
| static double random() | 0.0~1.0 사이 임의의 값 반환 |
