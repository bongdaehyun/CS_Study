# Stream

스트림은 '데이터의 흐름’입니다. 배열 또는 컬렉션 인스턴스에 함수 여러 개를 조합해서 원하는 결과를 필터링하고 가공된 결과를 얻을 수 있습니다. 또한 람다를 이용해서 코드의 양을 줄이고 간결하게 표현할 수 있습니다. 즉, 배열과 컬렉션을 함수형으로 처리할 수 있습니다.

또 하나의 장점은 간단하게 병렬처리(*multi-threading*)가 가능하다는 점입니다. 하나의 작업을 둘 이상의 작업으로 잘게 나눠서 동시에 진행하는 것을 병렬 처리(*parallel processing*)라고 합니다. 즉 쓰레드를 이용해 많은 요소들을 빠르게 처리할 수 있습니다.

- 자바 7 이전 코드

```java
List<String> list = Arrays.asList("홍길동", "신용권", "김남준");
Iterator<String> iterator = list.iterator();
while(iterator.hasNext()) {
  String name = iterator.next();
  System.out.println(name);
}

```

- 자바 8 이후 코드

```java
List<String> list = Arrays.asList("홍길동", "신용권", "김남준");
Stream<String> stream = list.stream();
stream.forEach(name -> System.out.println(name));
```

[스트림 구현 객체를 얻는 방법](https://www.notion.so/0abc74c661954814b4508d4221966b0a)

# Stream의 작업

1. 생성하기 : 스트림 인스턴스 생성
2. 가공하기 : 필터링, 맵핑 등 원하는 결과를 만들어간느 중간 작업
3. 결과 만들기 

## 생성하기

보통 배열과 컬렉션을 이용해서 스트림을 만들지만 이 외에도 다양한 방법으로 스트림을 만들 수 있습니다. 

### 배열 스트림

```java
String arr[]=new String[]{"1","2","d"};
Stream<String> stream=Arrays.stream(arr);
stream.forEach(System.out::println);// 1 2 d

Stream<String> PartArr=Arrays.stream(arr,1,3);
PartArr.forEach(System.out::println); // 2 d
```

### 컬렉션 스트림

```java
List<String> names =Arrays.asList("List","ststs","names");
Stream<String>stream= names.stream();
Stream<String>stream= names.parallelStream();//별렬 처리 스트림

```

### Stream.builder()

```java
Stream<String> builderStream=Stream.<String>builder()
                .add("Eric").add("Abc")
                .build();
builderStream.forEach(s->
                System.out.println("s = " + s)
        );
```

### 스트림 연결

```java
Stream<String> stream1 = Stream.of("Java", "Scala", "Groovy");
Stream<String> stream2 = Stream.of("Python", "Go", "Swift");
Stream<String> concat = Stream.concat(stream1, stream2);
```

## 가공하기

### Filtering

- 스트림 내 요소들을 하나씩 평가해서 걸러내는 작업

```java
Stream<String> builderStream=Stream.<String>builder()
                .add("Eric").add("Abc")
                .build();
builderStream
        .filter(s->s.contains("A"))
        .forEach(s->
                System.out.println("s = " + s)
        );
```

### Mapping

- 스트림 내 요소들을 하나씩 특정 값으로 변환해줌

```java
Stream<String> builderStream=Stream.<String>builder()
                .add("Eric").add("Abc")
                .build();
  builderStream
          .filter(s->s.contains("A"))
          .map(String::toUpperCase)
          .forEach(s->
                  System.out.println("s = " + s)
          );
```

### FlatMap

- 중첩된 구조를 한 단계 제거하고 단일 컬렉션으로 만들어주는 역할

```java
List<List<String>> list = 
  Arrays.asList(Arrays.asList("a"), 
                Arrays.asList("b"));
// [[a], [b]]

List<String> flatList = 
  list.stream()
  .flatMap(Collection::stream)
  .collect(Collectors.toList());
// [a, b]
```

### Sorting

- Comparator를 이용해서 정렬

```java
Stream<String> builderStream=Stream.<String>builder()
                .add("Eric").add("Abc")
                .build();
    builderStream
            .sorted()
            .forEach(s->
                    System.out.println("s = " + s)
          );

builderStream
    .sorted(Comparator.reverseOrder())
    .collect(Collectors.toList())//stream to list
    .forEach(s->
            System.out.println("s = " + s)
    );
```

## 결과 만들기

- 최소 최대합 합 평균 등 기본형 타입으로 결과를 만들어냄

```java
long count = IntStream.of(1,3,4,5,6).count();
long sum = IntStream.of(1,3,4,5,6).sum();
System.out.println("count = " + count); //count 5
System.out.println("sum = " + sum);//sum 19
```

평균, 최소, 최대의 경우에는 0을 표현할 수 없어서 Optional을 이용해 리턴

```java
OptionalInt min = IntStream.of(1, 3, 5, 7, 9).min();
OptionalInt max = IntStream.of(1, 3, 5, 7, 9).max();

DoubleStream.of(1.1, 2.2, 3.3, 4.4, 5.5)
  .average()
  .ifPresent(System.out::println);
```