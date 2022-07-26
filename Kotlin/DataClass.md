# 데이터 클래스

아래는 자바로 구현한 이름, 나이, 키, 몸무게, 성별을 갖는 데이터 클래스이다.
```java
public Student {
    String name;
    int age;
    double height;
    double weight;
    String gender;

    public Student(String name, int age, double height, double weight, String gender) {
        this.name = name;
        this.age = age;
        this.height = height;
        this.weight = weight;
        this.gender = gender;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    ...
}
```
이 코드 처럼 간단한 클래스더라도 보일러 플레이트 코드가 너무 비다하다.

코틀린에서는 data class 키워드로 생성하여 생성자에 파라미터들만 정의해주면 된다.

```kotlin
data class Student
(
    var name: String,
    var age: Int,
    var height: Double,
    var weight: Double,
    var genedr: String
)
```
훨씬 코드가 깔끔해졌다. 코틀린 data class는 생성자, getter, setter, canonical methods 를 생성해준다.

## 제안 사항
- 기본 생성자에느 최소 하나의 파라미터가 있어야 한다.
- 기본 생성자의 파라미터는 val 이거나 var 이어야 한다.
- 데어터 클래스는 abstract, open, sealed, inner가 되면 안 된다.

## copy() 메서드
copy() 메서드는 원하는 객체를 특정 필드 값만 바꿔서 복사한다.

```kotlin
val student1 = Student("ABC", 20, 160.4, 50.5, "male")
val student2 = student1.copy(name = "DEF", age = 25)
```

## 디스트럭쳐링(Destructuring)
디스트럭쳐링은 객체가 소유한 데이터를 쪼개주는 기능이다.
```kotlin
val student = Student("ABC", "20", 160.4, 50.5, "male")
val (name, age, height, weight, gender) = student
```