# Concurrent Programming

### 동시성 프로그래밍
작업을 분산시키고 여러 스레드에서 동시에 일을 할 수 있도록 처리하여 앱의 성능과 반응성을 최적화하기 위해, 애플에서는 GCD와 Operation을 통해 동시성(Concurrent) 프로그래밍을 지원하고 있다.

### GCD (Grand Central Dispatch) 란?
GCD는 '디스패치 큐'를 이용하여 멀티코어 환경에서 여러 작업을 동시에 빠르고 효율적으로 처리할 수 있도록 multi threading을 지원하고 작업들을 관리해주는 framework.

### Dispatch Queue
디스패치 큐란 작업들이 여러 쓰레드에서 동기적 or 비동기적으로 동작하며 동시에 일을 할 수 있도록 작업을 분산 처리 하는 FIFO 대기열이다.<br>
디스패치 큐의 종류에는 main, global, private(custom) 큐가 있는데,<br>
main Queue에서 실행되는 main thread는 iOS 에서 오직 하나만 존재하고, 모든 UI 작업들이 이 메인 쓰레드에서 처리된다.<br>
그런데 이 메인 큐는 한 번에 하나의 task 밖에 실행하지 못하는 serial 큐이기 때문에, <br>
UI 실행에 영향을 끼칠 수 있는 시간이 오래 걸리는 작업들의 경우, 글로벌 큐에서 비동기적으로 구현하는 것이 좋다.<br>

### DispatchQoS
Global 큐에서는 작업의 처리 우선 순위를 설정할 수 있도록 QoS 파라미터(.userInteractive, .userInitiated, default, .utility, .background)를 제공하고 있다.<br> 
우선 순위가 높을수록 더 빠르게 처리되는 대신 더 많은 리소스와 에너지가 필요하기 때문에, 작업에 따라 QoS를 적절하게 사용해야 앱의 성능과 에너지 효율성을 최적화할 수 있다.<br>
\+ QoS 종류가 다른 글로벌 큐가 중첩되어 사용될 경우, 더 높은 우선순위를 가진 QoS 를 따라 처리가 된다. 

### DispatchGroup
여러 쓰레드에서 분산 처리하고 있는 작업들을 그룹으로 묶어, 작업들이 끝나는 시점을 알고 싶을 때 사용한다. 
