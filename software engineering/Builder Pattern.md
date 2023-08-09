## 개요
- 생성자에 들어갈 매개 변수를 메서드로 하나하나 받아들이고 마지막에 통합 빌드해서 객체를 생성하는 방식
- 클래스의 선택적 매개변수가 많은 상황에서 유용하게 사용됨

## 탄생 배경

### 점층적 생성자 패턴
-> 생성자 오버로딩 방식
- 몇번째 인자가 어떤 필드였는지 헷갈림
- 필드를 선택적으로 생략할 방법이 없음(억지로 0,null 전달)
- 타입이 다양할수록 생성자 수가 기하급수저으로 늘어나 가독성이나 유지보수 측면에서 좋지 않다.

### Java Beans 패턴
-> 기본생성자로 생성 후 Setter 메소드 이용하여 초기값 설정

1. 일관성 문제

초기화할때 필수 매개변수를 깜빡하고 Setter 메서드 일부를 호출하지 않았다면 이 객체는 일관성이 무너진 상태가 된다.

2. 불변성 문제

Setter메서드가 객체 생성 이후에도 외부적으로 노출하고 있으므로, 누군가 Setter메서드를 호출해 함부로 객체를 조작할 수 있게 된다.

## 빌더 패턴 구조

### Simple 빌더 패턴 구현
```java
class Person {
    // final 키워드로 필드들을 불변 객체로 만든다.
    private final String name;
    private final String age;
    private final String gender;
    private final String job;
    private final String birthday;
    private final String address;

    // 정적 내부 빌더 클래스
    public static class Builder {

        // 필수 파라미터
        private final String name;
        private final String age;

        // 선택 파라미터
        private String gender;
        private String job;
        private String birthday;
        private String address;

        // 필수 파라미터는 빌더 생성자로 받게 한다
        public Builder(String name, String age) {
            this.name = name;
            this.age = age;
        }

        // 선택 파라미터는 각 메서드를 통해 정의한다
        public Builder gender(String gender) {
            this.gender = gender;
            return this;
        }

        public Builder job(String job) {
            this.job = job;
            return this;
        }

        public Builder birthday(String birthday) {
            this.birthday = birthday;
            return this;
        }

        public Builder address(String address) {
            this.address = address;
            return this;
        }

        // 대상 객체의 private 생성자를 호출하여 최종 인스턴스화 한다
        public Person build() {
            return new Person(this); // 빌더 객체 자신을 넘긴다.
        }
    }

    // private 생성자 - 생성자는 외부에서 호출되는것이 아닌 빌더 클래스에서만 호출되기 때문에
    private Person(Builder builder) {
        this.name = builder.name;
        this.age = builder.age;
        this.gender = builder.gender;
        this.job = builder.gender;
        this.birthday = builder.birthday;
        this.address = builder.address;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age='" + age + '\'' +
                ", gender='" + gender + '\'' +
                ", job='" + job + '\'' +
                ", birthday='" + birthday + '\'' +
                ", address='" + address + '\'' +
                '}';
    }
}
```
### 빌더 클래스 실행
```java
public static void main(String[] args) {

    Person person = new Person
            .Builder("홍길동", "26") // static inner class 초기화 (필수 파라미터)
            .gender("man") // 선택 파라미터
            .job("Warrior")
            .birthday("1800.10.10")
            .address("조선")
            .build();

    System.out.println(person);
}
```

## 빌더 패턴 장단점

### 장점

1. 객체 생성 과정을 일관된 프로세스로 표현
- 가독성과 실수 방지
2. 디폴트 매개변수 생략을 간접적으로 지원
- 디폴트 매개변수가 설정된 필드를 설정하는 메서드를 호출하지 않는 방식
3. 필수 멤버와 선택적 멤버를 분리 가능
- 생성자 방식이였으면 오버로딩 열거나, 전체 생성자 후 null을 해야함.
4. 초기화 검증을 멤버별로 분리
- 객체의 멤버 변수의 초기화와 검증을 각각의 멤버별로 분리해서 작성할 수 있어서 유지보수에 용이.
5. 멤버에 대한 변경 가능성 최소화를 추구
- 클래스 맴버 초기화를 Setter을 통해 구성하는 것은 매우 좋지 않은 방법
- 협업시에 가장 중요시되는 점 중 하나가 바로 불변(immutalbe) 객체
- 현업에서 불변 객체를 이용해 개발해야 하는 이유
  + 불변 객체는 Thread-Safe 하여 동기화를 고려하지 않아도 된다
  + 만일 가변 객체를 통해 작업을 하는 도중 예외(Exception)가 발생하면 해당 객체가 불안정한 상태에 빠질 수 있어 또 다른 에러를 유발할 수 있는 위험성이 있기 때문
  + 불변 객체로 구성하면 다른 사람이 개발한 함수를 위험없이 이용을 보장할 수 있어 협업에도 유지보수에도 유용

> 빌더 패턴은 생성자 없이 어느 객체에 대해 '변경 가능성을 최소화' 를 추구하여 불변성을 갖게 해주게 되는 것이다.