# DIP

하위 모듈에 의존하는 상위 모듈의 관계를 역전시켜,
하위 모듈이 상위 모듈에 의존하게 하는 것이다.

> 상위 수준의 모듈은 하위 수준의 모듈에 의존해서는 안 된다. 둘 모두 추상화에 의존해야 한다.


**상위 수준의 정책이란?**

구체적인 것이 변경되도 바뀌지 않는 진실. 구체적인 메커니즘이 아닌 그 자체의 행위. 

예를 들어, 램프를 키더라도 램프가 LED인지 형광등인지 상관 없이,  램프를 사용하기 위해서 변하지 않는 킨다/끈다 라는 명확한 행위. 




> 추상화는 구체적인 사항에 의존해서는 안 된다. 구체적인 사항은 추상화에 의존해야 한다.
* 어떤 변수도 구체 클래스(하위 모듈)에 대한 포인터나 참조값을 가져서는 안된다.
* 어떤 클래스도 구체 클래스에서 파생되어서는 안 된다.
* 어떤 메소드도 그 기반 클래스에서 구현된 메소드를 오버라이드해서는 안된다.

구체 클래스는 자주 변경될 수 있기 때문에, 클라이언트가
String과 같은 잘 변경되지 않고, 다른 파생 클래스가 만들어지지 않는 클래스라면 의존해도 큰 해가 되지 않는다.

자주 바뀌는 것에 의존하는 것이 해가 되는 것이다.



### *어떻게 역전시키는가?*
![의존적인 모듈들](https://upload.wikimedia.org/wikipedia/commons/4/42/Traditional_Layers_Pattern.png)

위의 사진은 Policy, Mechanism, Utility가 서로 의존하고 있다.


Policy는 Mechanism의 기능이 필요하고, Mechanism은 Utility의 기능이 필요하기 때문이다.


이럴 때, Policy가 직접 Mechanism을 사용하는 것이 아닌, Policy가 원하는 기능을 인터페이스에 선언 하고, Mechanism이 그것을 구현하게 한다.

 이러면 Policy는 Mechanism과 Utility에 의존하게 되지 않고,
 Mechanism과 Utility이 인터페이스에 의존하게 되어 역전이 된다.


![DIP 적용 후](https://upload.wikimedia.org/wikipedia/commons/8/8d/DIPLayersPattern.png)
