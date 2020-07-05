## OCP(	개방-폐쇄 원칙 (Open/closed principle))
> 소프트웨어 개체(클래스, 모듈, 함수 등)는 확장에 대해 열려 있어야 하고, 수정에 대해서는 닫혀 있어야 한다. 

### **OCP를 따르는 모듈의 속성**
*  확장에 대해 열려있다. 어플리케이션의 요구 사항이 변경될 때, 이 변경에 맞게 새로운 행위를 추가해 모듈을 확장할 수 있다. 즉, 모듈이 하는 일을 변경할 수 있다는 것이다.

* 수정에 대해 닫혀 있다. 모듈의 행위를 확장할 때, 그 모듈의 소스 코드나 바이너리 코드의 변경을 초래해선 안된다.

* 변경에는 닫혀있고 확장에는 열려있어야 하는 이유는
기존의 모듈을 변경을 하면 그 모듈에 의존을 하는 모듈이 작동을 하지 않을 수도 있다. 그렇기에 요구사항이 변경되었을 때 변경 대신 확장하는 방향으로 해야한다.

## OCP 적용방법

로버트 C. 마틴은 소스 코드를 변경하지 않는다는 조건의 OCP를 가능하게 하는 것이 추상화라고 한다.

**적용 전**
![](https://postfiles.pstatic.net/MjAxOTA4MTFfMjQ4/MDAxNTY1NTI5ODUyMjc1.-klmjNH5olJ9zLHTQVx6-yEFU3CcdrS4KDsuNhF-ykcg.glRiMljkP-GOdbL7ypY0mgUlywuN-wYxO-wQ6f4g-mYg.JPEG.jwyoon25/56.JPG?type=w773)
```kt
class Server(sName : String){
    var name =sName
    fun connect(){
        println("소켓 연결 완료")
    }
}
class Client{

    fun connect(s: Server){
        println("${s.name} 과 연결")
        s.connect()
    }
}
interface ClientService{

}

fun main(){
    val server= Server("소켓")

    Client().connect(server)

}
```
Client와 Server라는 클래스가 있다고 하자. 

여기서 Client는 Server에 의존적인데, Server가 바뀔 때마다 기능을 변경해야 한다. 



**적용 후**
![](https://postfiles.pstatic.net/MjAxOTA4MTFfMjc0/MDAxNTY1NTMwMTQ5NTUz.9ngRA5Rgji0ddHk2gXA5BLKuxMEPgapkyRPwloftKAog.LYG0BN4zP126V3kP0FI2HoE1QpQfejzLYR5eHyi6uJIg.JPEG.jwyoon25/57.JPG?type=w773)
```kt

class Server(sName : String) : ClientService{
    override var name =sName
    override fun connect(){
        println("소켓 연결 완료")
    }

}
class Client(){

    fun connect(s: ClientService){
        println("${s.name} 과 연결")
        s.connect()

    }
}
interface ClientService{
    var name : String
    fun connect()

}

fun main(){
    val server : ClientService= Server("소켓")

    Client().connect(server)

}

```
그래서 서버의 추상 클래스인 ClientInterface를 두고 Client가 사용하게 하고, Server가 구현해야 하게 만든다. 

Server는 ClientInterface의 서브 타입이라 원하는 대로 인터페이스를 구현할 수 있고, Client가 하는 행위는 ClientInterface의 서브타입을 생성하여 확장 가능하다.


그렇기에 Client는 변경이 일어나지 않고 확장만이 일어난다.

* Server의 추상 클래스인데 AbstractServer가 아닌 이유는 추상 클래스는 그를 구현하는 구현체보다 사용하는 Client와 더 밀접하게 관련되어 있기 때문이다. 




