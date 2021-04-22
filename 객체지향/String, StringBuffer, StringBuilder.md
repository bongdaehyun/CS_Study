# String, StringBuffer, StringBuilder

---

[제목 없음](https://www.notion.so/71098f6996294792846efebc89571461)

---

# 1. String

- new 연산을 통해 생성된 인스턴스의 메모리 공간은 변하지 않음(lmmutable)
- Garbage Collector로 제거 되어야함
- 문자열 연산시 새로 객체를 만드는 Overhead 발생
- 객체가 불변하므로, Multithread에서 동기화를 신경 쓸 필요가 없음

# 2. StringBuffer, StringBuilder

- 공통점
    - new 연산으로 클래스를 한 번만 만듬(Mutable)
    - 문자열 연산시 새로 객체를 만들지 않고, 크기를 변경시킴
    - 클래스의 메서드가 동일
- 차이점
    - StringBuffer는 Thread-Safe
    - StringBuilder는 Thread-sage하지 않음