# Cluster

### **How it works**

**작동 원리**

The worker processes are spawned using the `[child_process.fork()](https://nodejs.org/docs/latest-v15.x/api/child_process.html#child_process_child_process_fork_modulepath_args_options)` method, so that they can communicate with the parent via IPC and pass server handles back and forth.

작업자 프로세스는 IPC를 통해 상위 프로세스와 통신하고 서버 핸들을 앞뒤로 전달할 수 있도록 child_process.fork() 메소드를 사용하여 생성됩니다.

The cluster module supports two methods of distributing incoming connections.

클러스터 모듈은 들어오는 연결을 분배하는 두 가지 방법을 지원합니다.

The first one (and the default one on all platforms except Windows), is the round-robin approach, where the master process listens on a port, accepts new connections and distributes them across the workers in a round-robin fashion, with some built-in smarts to avoid overloading a worker process.

첫 번째 방법은 (윈도를 제외한 모든 플랫폼에서 기본) 라운드 로빈 접근법으로, 마스터 프로세스가 포트에서 수신하고 새로운 연결을 허용하고 라운드 로빈 방식으로 작업자에게 배포하며, 일부 내장된 스마트로 작업자 프로세스에 과부하를 방지한다.

The second approach is where the master process creates the listen socket and sends it to interested workers. The workers then accept incoming connections directly.

두 번째 접근 방식은 마스터 프로세스가 수신 소켓을 생성하여 관심 있는 작업자에게 보내는 것입니다. 그런 다음 작업자는 들어오는 연결을 직접 수락합니다

The second approach should, in theory, give the best performance. In practice however, distribution tends to be very unbalanced due to operating system scheduler vagaries. Loads have been observed where over 70% of all connections ended up in just two processes, out of a total of eight.

두 번째 접근 방식은 이론적으로 최상의 성능을 제공해야 합니다. 그러나 실제로는 운영 체제 스케줄러의 변동으로 인해 분배가 매우 불균형한 경향이 있습니다. 모든 연결의 70% 이상이 총 8개 중 2개 프로세스에서 끝나는 부하가 관찰되었습니다.

[부가적](https://www.notion.so/bb1409418dfb441a8009a7db4d26c9be)