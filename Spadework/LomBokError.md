# 안드로이드 스튜디오 LomBok 에러
안드로이드 스튜디오 버전을 올리니 Lombok을 사용하는 곳에서 cannot find symbol 에러가 발생했다.

구글링을 해보니 build.gradle 에 아래 코드를 추가해주면 해결이 된다고 한다.
```gradle
dependencies {
    ...
    compile 'org.projectlombok:lombok:1.18.16'
    annotationProcessor 'org.projectlombok:lombok:1.18.16'
}
```

하지만 나는 해결되지 않았다.

또 하나의 방법으로 나는 Room과 Lombok를 같이 사용하고 있었는데

Room과 Lombok을 같이 사용하려면 아래와 같이 Lombok 라이브러리가 Room 라이브러리 보다 위에 있어야 한다.
```gradle
dependencies {
    ...
    compile 'org.projectlombok:lombok:1.18.16'
    annotationProcessor 'org.projectlombok:lombok:1.18.16'

    implementation 'androidx.room:room-rxjava2:2.2.5'
    implementation 'androidx.room:room-runtime:2.2.5'
    annotationProcessor 'androidx.room:room-compiler:2.2.5'
}
```

여기까지 했는데 해결이 되지 않았다.

세 번째 방법으로 안드로이드 스튜디오에 호환되는 Lombok 파일을 다운 받아 플러그인 폴더로 시켜준다.

## 플러그인 폴더에 외부 라이브러리 추가 방법
File -> Settings -> Plugins -> 상단 톱니바퀴 아이콘 클릭(아래 이미지 참고) -> Install Plugin from Disk -> 설치한 Lombok 선택

## 상단 톱니바퀴 참고 이미지
![plugins1](https://user-images.githubusercontent.com/73802331/179897587-1b52b3a7-d288-46ad-ba0c-11afd41a492a.png)


dependencies 라이브러리를 추가하고 Lombok 플러그인을 변경까지 했더니 문제가 해결됐다.

## Lombok 설치 파일
https://github.com/mplushnikov/lombok-intellij-plugin/issues/1111
