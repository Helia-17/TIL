https://github.com/Dongkyun-Jang/TIL/blob/master/OS/Process%20Synchronization.md

> 개념에 대해서 한 줄로 정의할 수 있어야.



Context Switching이란?

- 프로세스 간, 스레드 간도 가능
- 스레드 간 교환될때는 TCB (thread control block)



Context switching 과정을 설명해보세요

- user mode에서 kernel mode로 바뀌어야 함
  - system call 혹은 interrupt

- P0의 PCB 저장
- P1의 PCB 복원= 로드= 불러오기



멀티프로세싱

- CPU 사용률을 최대화하기 위해서 두 개 이상의 프로그램을 



멀티프로그래밍과 멀티프로세싱?

프로그래밍 : 프로그램, 사용자 측면

프로세싱 : 프로세스, CPU 측면



Parallelism과 Concurrency의 차이?

parallelism : 복수의 작업들이 동시에 시작

Concurrency : 한정된 시간을 쪼개서 복수의 작업들이 사용

= 싱글코어와 멀티코어의 차이는?

싱글코어에서의 동시를 우리는 Concurrency라 합니다.

멀티코어에서의 동시를 우리는 Parallelism이라 합니다.

Concurrency에서 발생하는 전환이 사람이 느끼기엔 빠르기 때문에  둘 다 동시라고 얘기하지만 구분하는 것이 좋다.



멀티프로세싱이 유리한가요 멀티스레딩이 유리한가요?

> 반드시 상황 마다 다르다는 것을 먼저 말해야한다. 이후에 "통상적으로는 IO bound가 크면 멀티스레딩이 유리하고 CPU bound가 크면 멀티프로세싱이 유리합니다."
>
> IO bound가 크면 멀티프로세싱의 경우 한개의 프로세스가 계쏙 그 큰 IO burst time을 기다릴 것. 하지만 멀티스레딩에서는 한 스레드가 wait for IO를 하고 나머지는 다른 작업을 수행할 것.

