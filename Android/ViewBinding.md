# 뷰 바인딩 (ViewBindig)
## 뷰 바인딩이란
뷰 바인딩은 뷰와 상호작용하는 코드를 쉽게 작성할 수 있는 기능이다.

뷰 바인딩을 활성화하면 각 xml 파일에 대해 ViewBinding 클래스를 상속받는 개별 뷰 바인딩 클래스가 자동으로 생성된다.

바인딩 클래스의 인스턴스에는 상응하는 레이아웃에 ID가 있는 모든 뷰에 대해 직접적으로 참조된다.
## 뷰 바인딩 설정
> 뷰 바인딩은 Android Studio 3.6 부터 사용 가능하다.

다음 예제와 같이 build.gradle 파일에 추가한다.
```gradle
android {
    ...
    viewBinding {
        enabled = true
    }
}
```
## 뷰 바인딩 사용 방법
뷰 바인딩을 활성화하면 각 xml 파일에 대해 바인딩 클래스가 생성된다.

각 바인딩 클래스에는 루트 뷰 및 ID가 있는 모든 뷰의 참조가 포함된다.

바인딩 클래스의 이름은 xml 파일의 이름은 카멜 표기법으로 변환하고 끝에 'Binding'을 추가하여 생성된다.
```kotlin
private val binding: ActivityMainBinding by lazy {
    ActivityMainBinding.inflate(layoutInflater)
}

override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(binding.root)

    binding.textView.text = "ViewBinding"
}
```
## 뷰 바인딩 장점
- Null-safe: 뷰 바인딩은 서로 다른 layout의 같은 ID를 가진 뷰를 정확히 구분할 수 있다. 만약 그럴 수 없을 경우 @Nullable로 만들어 사용할 수 없게 한다.
- Type-safe: findViewById를 사용할 경우 뷰에 잘못된 타입을 지정할 우려가 있는데 뷰 바인딩에서는 그런 문제가 발생하지 않는다.
## 데이터 바인딩과 뷰 바인딩의 차이
뷰 바인딩과 데이터 바인딩 라이브러리 둘 다 직접 참조하는 바인딩 클래스를 생성한다.

그러나 다음과 같은 차이점이 있다.
- 데이터 바인딩 라이브러리는 ```<layout>``` 태그를 사용하여 만든 레이아웃을 처리하고, TAG를 삽입한다.
- 뷰 바인딩은 양방향 바인딩을 지원하지 않는다.
- 뷰 바인딩의 속도가 더 빠르다.