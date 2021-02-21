[1. 컬렉션 프레임워크](#collection-framework)         
[1.1 컬렉션 프레임워크의 핵심 인터페이스](#core-interface-of-collection-framework)               
[1.2 ArrayList](#arraylist)         
[1.3 LinkedList](#linkedlist)          
[1.4 Stack과 Queue](#stack-and-queue)                
[1.5 lterator, Listterator, Enumeration](#lterator-Listterator-Enumeration)                 
[1.6 Arrays](#arrays)               
[1.7 Comparator와 Comparable](#comparator-and-comparable)            
[1.8 HashSet](#hashset)           
[1.9 TreeMap](#treemap)            
[1.10 HashMap과 Hashtable](#hashmap-and-hashtable)           
[1.11 TreeMap](#treemap)            
[1.12 Properties](#properties)           
[1.13 Collections](#collections)                 
[1.14 컬렉션 클래스 정리 및 요약](#cleaning-up-and-summarizing-collection-classes)           

# Collection Framework

**컬렉션 프레임워크**란 다수의 데이터를 저장하는 클래스들을 표준화한 설계를 의미한다. 컬렉션 프레임워크는 다양한 클래스들을 제공하고, 인터페이스와 다향성을 이용한 객체지향적 설계를 통해 표준화되어 있기 때문에 재사용성 뫂은 코드를 작성할 수 있다.

## Core Interface of Collection Framework

컬렉션 프레임워크에서 컬렉션 데이터 그룹을 **List, Set, Map 인터페이스**로 구분한다. List와 Set을 구현한 컬렉션 클래스들은 서로 많은 공통점이 있기 때문에 공통된 부분을 뽑아 Collection으로 정의할 수 있다. Map은 List와 Set과는 전혀 다른 형태로 컬렉션을 다룬다. 컬렉션 프레임워크의 핵심 인터페이스는 다음과 같은 특징을 갖는다.

| 인터페이스 | 특징 |
|:-:|:-|
| List | 순서가 있는 데이터 집합. 데이터의 중복을 허용한다. |
| Set | 순서를 유지하지 않는 데이터 집합. 데이터의 중복을 허용하지 않는다. |
| Map | key와 value의 쌍으로 이루어진 데이터 집합. 순서는 유지되지 않고, key는 중복을 허용하지 않고 value는 중복을 허용한다. |

### Collection 인터페이스

Collection 인터페이스는 컬렉션 클래스에 저장된 데이터를 읽고, 추가하고, 삭제하는 등 컬력션을 다루는 가장 기본적인 메서드를 정의한다. Collection 인터페이스에 정의된 메서드는 다음과 같다.

| 메서드 | 설명 |
|:-|:-|
| boolean add(Object o) | 지정된 객체(o)들을 Collection에 추가 |
| boolean add(Collection c) | 지정된 객체(c)들을 Collection에 추가 |
| void clear() | Collection의 모든 객체 제거 |
| boolean contains(Object o) | 지정된 객체(o)들이 Collection에 포함되어 있는지 확인 |
| boolean containsAll(Collection c) | 지정된 객체(c)들이 Collection에 포함되어 있는지 확인 |
| boolean equals(Object o) | 동일한 Collection인지 확인 |
| int hashCode() | Collection의 hash code 반환 |
| boolean inEmpty() | Collection이 비어있는지 확인 |
| lterator iterator() | Collection의 lterator를 얻어서 반환 |
| boolean remove(Object o) | 지정된 객체(o) 삭제 |
| boolean removeAll(Collection c) | 지정된 Collection에 포함된 객체 삭제 |
| int size() | Collection에 저장된 객체 수 반환 |
| Object[] toArray() | Collection에 저장된 객체를 객체배열(Object[])로 반환 |
| Object[] toArray(Object[] a) | 지정된 배열(a)에 Collection의 객체를 저장해서 반환 |

### List 인터페이스

List 인터페이스는 중복을 허용하면서 저장순서가 유지되는 컬렉션을 구현하는데 사용된다. List 인터페이스에 정의된 메서드는 다음과 같다. Collection 인터페이스로부터 상속된 메서드는 제외했다.

| 메서드 | 설명 |
|:-|:-|
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |

### Set 인터페이스

| 메서드 | 설명 |
|:-|:-|
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |

### Map 인터페이스

| 메서드 | 설명 |
|:-|:-|
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |
|  |  |

## ArrayList
## LinkedList
## Stack and Queue
## lterator Listterator Enumeration
## Arrays
## Comparator and Comparable
## HashSet
## TreeMap
## HashMap and Hashtable
## TreeMap
## Properties
## Collections
1.14 컬렉션 클래스 정리 및 요약](#cleaning-up-and-summarizing-collection-classes)
