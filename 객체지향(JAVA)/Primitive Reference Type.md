# Primitive / Reference Type

# primitive data type

- 기본적인 값을 기억하는 변수 타입
- byte,short,int,float,double,char,boolean

    ![/객체지향/image/PRT.png](/객체지향/image/PRT.png)

- Stack 메모리에 저장 → 비객체 타입이며 null값을 가질 수 없다.

## **Implicit Type Casting(암시적 형변환)**

작은 크기의 타입은 큰 크기의 타입으로 자동 형변환된다.

## Explicit Type Casting(명시적 형변환)

큰 크기의 타입을 작은 크기의 타입으로 변경

# Reference Data Type

- 기본 타입을 제외한 모든 타입이 Reference type
- 객체의 참조값을 기억하는 변수
- class, interface, 배열
- Null 사용 가능 , 런타임 에러가 발생하는 경우도 잇음.
- Heap 메모리에 생성된 인스턴스는 메소드나 각종 인터페이스에서 접근하기 위해 JVM의 Stack 영역에 존재하는 Frame에 참조 값을 가지고 있어 이를 통해 핸들링됨..

![/객체지향/image/PRT01.png](/객체지향/image/PRT01.png)

---

#
