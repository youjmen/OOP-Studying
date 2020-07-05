# ISP
> 클라이언트가 자신이 사용하지 않는 메서드에 의존하도록 강제 되서는 안된다.

클래스 A와 B가 있다. A는 씻기 기능, B는 요리하기 기능이 있다.
이 두 기능을 interface에 넣고 A, B에서 구현하게 하면, A는 요리하기 기능을 사용하지 않는데도 요리하기 기능이 변경되면 재 컴파일되고, 문제가 생기면 클래스 A에도 문제가 생긴다.

```kt
class A : doSomething{
    override fun cook() {
        println("요리하기")
    }

    override fun shower() {
    }

}
class B : doSomething{
    override fun cook() {
    }

    override fun shower() {
        println("씻기")

    }

}
interface doSomething{
    fun cook()

    fun shower()
}
```

그래서, 인터페이스를 분리해야 한다.
하나의 비대한 인터페이스를 만들지 말고, 클라이언트가 사용하는 메서드에 따라 인터페이스를 분리하면 된다.
```kt
class A : Cook{
    override fun cook() {
        println("요리하기")
    }

  

}
class B : Shower{
    override fun shower() {
        println("씻기")

    }

}
interface Cook {
    fun cook()
}
interface Shower{
    fun shower()
}

```