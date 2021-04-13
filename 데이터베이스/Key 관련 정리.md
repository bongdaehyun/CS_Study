# Key 관련 정리

---

> key란 : 검색, 정렬시 Tuple을 구분할 수 있는 기준이 되는 Attribute

# Candidate key(후보키)

Tuple을 유일하게 식별하기 위해 사용하는 속성들의 부분 집합(기본키로 사용할 수 있는 속성들)

- 2가지 조건 만족
1. 유일성 : key로 하나의 Tuple을 유일하게 식별할 수 있음
2. 최소성 : 꼭 필요한 속성으로만 구성

# Primary key

후보키 중 선택한 Main key

- NOT NULL & UNIQUE
- Null을 가질 수 없음
- 중복된 값을 가질 수 없음

# Alternate key

후보키 중 기본키를 제외한 나머지 키= 보조키

# Super key

유일성은 만족하지만, 최소성은 만족하지 못하는 키

# Foregin key

다른 릴레이션의 기본키를 그대로 참조하는 속성의 집합

- **RESTRICT** : FK 관계를 맺고 있는 데이터 ROW 의 변경(UPDATE) 또는 삭제(DELETE) 를 막는다.
- **CASCADE** : FK 관계를 맺을 때 가장 흔하게 접할 수 있는 옵션으로, FK 와 관계를 맺은 상대 PK 를 직접 연결해서 DELETE 또는 UPDATE 시, 상대 Key 값도 삭제 또는 갱신시킨다. → 이  때에는 Trigger 가 발생하지 않으니 주의하자.
- **SET NULL** : 논리적 관계상 부모의 테이블, 즉 참조되는 테이블의 값이 변경 또는 삭제될 때 자식 테이블의 값을 NULL 로 만든다. UPDATE 쿼리로 인해 SET NULL 이 허용된 경우에만 동작한다.
- **NO ACTION** : RESTRICT 옵션과 동작이 같지만, 체크를 뒤로 미룬다.
- **SET DEFAULT** : 변경 또는 삭제 시에 값을 DEFAULT 값으로 세팅한다.

# Unique key

Uniqueness를 지닌 index를 말한다.

- 중복성 허용 x
- null 허용
- 테이블에 여러개 가능