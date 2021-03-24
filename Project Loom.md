
[나는 왜 Reactive streams와 친해지지 않는가?](https://gunsdevlog.blogspot.com/2020/09/reactive-streams-reactor-webflux.html)   
[Java의 동시성 개선을 위한 Project Loom은 reactive streams를 대체할 것인가?](http://gunsdevlog.blogspot.com/2020/09/java-project-loom-reactive-streams.html)   
[Why Continuations are Coming to Java](https://www.infoq.com/presentations/continuations-java/)

## 동기 처리방식(Blocking)의 문제점
* 많은 수의 동시접속 발생 시 자원사용량/처리속도 문제가 발생


## 비동기 처리방식(Non BLocking)의 문제점
* 제어흐름을 잃는다.   
  비즈니스 코드에 부가적인 제어코드들이 많이 섞인다.
* Context를 잃는다.   
  정확한 Stacktrace를 알 수 없다.
* 전염성이 있다.   
  하나가 Future를 반환하면, 그것을 호출한 것도 Future를 반환해야 하고, ... 특정 페러다임을 강제한다.   
  [How do you color your functions?](https://medium.com/@elizarov/how-do-you-color-your-functions-a6bb423d936d)

## Project Loom
Blocking 방식의 문제는 Thread가 너무 무거워서 발생하는 것이다. Thread를 가볍게 만들자.   
[Project Loom: Fibers and Continuations for the Java Virtual Machine](https://cr.openjdk.java.net/~rpressler/loom/Loom-Proposal.html)

* OS Thread를 직접 사용하면 다량의 동시요청을 처리하기 어렵다.
* 경량 Thread(Fiber)를 수백만개 만들어서 blocking을 자유롭게 쓰게하자.

Fiber = Continuation + Scheduler
* Continuation: 작업을 수행하다가 IO를 만나면 자기 상태를 저장한 후 Thread를 반납
* Scheduler: IO가 완료되면 Thread를 할당하여 중지되었던 작업을 계속 진행

