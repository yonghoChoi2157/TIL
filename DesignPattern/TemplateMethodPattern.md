# 템플릿 메소드 패턴
## 템플릿 메소드 패턴이란
전체적으로는 동일하지만 부분적으로 다른 경우 중복을 최소화 하는 패턴

동일한 기능을 상위 클래스에 정의하고 부분적으로 다른 부분은 서브 클래스에 정의

쉽게 말하면 같은 부분은 공통으로 사용하고 다른 부분만 따로 생성

GoF의 디자인 패턴에 의하면, 템플릿 메소드 패턴은 아래와 같이 정의한다.
> 알고리즘의 구조를 메소드에 정의하고, 하위 클래스에서 알고리즘 구조의 변경없이 알고리즘을 재정의 하는 패턴이다. 알고리즘이 단계별로 나누어 지거나, 같은 역할을 하는 메소드이지만 여러곳에서 다른형태로 사용이 필요한 경우 유용한 패턴이다.

토비의 스프링에 의하면, 템플릿 메소드 패턴은 아래와 같이 정의한다.
> 상속을 통해 슈퍼클래스의 기능을 확장할 때 사용하는 가장 대표적인 방법. 변하지 않는 기능은 슈퍼클래스에 만들어두고 자주 변경되며 확장할 기능은 서브클래스에서 만들도록 한다.

## 예제 코드
```kotlin
abstract class Recipe {
    // 로직이 같은 부분이므로 하위 클래스가 구현할 필요 없음.(중복제거)
    fun prepareRecipe(): String =
        "카페인 ${totalCaffeine()} 온도 ${temperature()}"

    // 로직이 다른 하위 메소드는 하위 클래스에서 구현
    abstract fun totalCaffeine(): Int
    abstract fun temperature(): Int
}

class ColdBrew : Recipe() {
    override fun totalCaffeine(): Int = 10
    override fun temperature(): Int = 4
}

class Americano : Recipe() {
    override fun totalCaffeine(): Int = 8
    override fun temperature(): Int = 2
}
```