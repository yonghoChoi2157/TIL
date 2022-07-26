# 커맨드 패턴

## 커맨드 패턴이란
커맨드 패턴은 요청을 객체의 형태로 캡슐화하여 사용자가 보낸 요청을 나중에 이용할 수 있도록 메서드 이름, 매개변수 등 요청에 필요한 정보를 저장 또는 로깅. 취소할 수 있게 하는 패턴이다.

쉽게 말해 요처사항을 객체로 캡슐화하는 것이다.

## 구성 요소
커맨드 패턴은 다음과 같은 요소들이 필요하다.
- 수신자(Recevier) : 커맨드 실행
- 명령(Command) : 수신자의 정보 + 행동이 들어있는 객체
- 발동자(Invoker) : 커맨드 저장, 커맨드 실행 요청
- 클라이언트(Client) : 커맨드 객체를 생성하고, 발동자를 통해 수신자에게 할 행동을 결정

## 예제 코드
```kotlin
// 명령 인터페이스
interface Command {
    fun execute()
}

// 명령 인터페이스 구현
class ConcreteCommand(private val receiver: Example4Receiver) : Example4Command {
    override fun execute() {
        receiver.start()
    }
}

class Invoker {

    private val queue = ArrayList<Example4Command>()

    // 명령 저장
    fun addToQueue(vararg command: Example4Command) = apply { queue.addAll(command) }

    // 명령 실행 요청
    fun processCommands() = apply {
        queue.forEach { it.execute() }
        queue.clear()
    }

}

// 명령 실행
class Example4Receiver(private val state: State) {
    enum class State { SLEEP, EAT, WORK }

    fun start() = when (state) {
        State.SLEEP -> print("잠잔다")
        State.EAT -> print("먹는다")
        State.WORK -> print("일한다")
    }

}

fun main() {
    Example4Invoker().addToQueue(
        Example4ConcreteCommand(Example4Receiver(Example4Receiver.State.SLEEP)),
        Example4ConcreteCommand(Example4Receiver(Example4Receiver.State.EAT)),
        Example4ConcreteCommand(Example4Receiver(Example4Receiver.State.WORK))
    ).processCommands()
}
```