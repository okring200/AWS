# chapter 1

## os 정의

* 정확한 정의 x
* 역할을 통해 다음과 같이 정의
  * 컴퓨터 하드웨어를 관리하는 프로그램
  * 프로그램의 실행을 제어하는 프로그램

* OS의 역할
  * 하드웨어 관리
    - I/O 기기 접근
    - 파일 접근
    - accounting
    - 에러 탐지
  * 프로그램 실행
    * 스케쥴링
    * 에러 보고

* OS는 자원할당자
  - 모든 자원을 관리
  - 충돌하는 요청에 자원을 할당하는 방법 결정
* OS는 제어프로그램
* 컴퓨터의 시스템 오류 및 부적절한 사용 방지위해 프로그램 실행 제어

* 또다른 정의
  * 컴퓨터에서 항상 실행되는 하나의 프로그램은 커널 또는 os라고 한다. 그 밖의 모든 프로그램은 시스템프로그램이거나 응용프로그램

## 컴퓨티시스템 주요원리

1. 컴퓨터 시스템 I/O 운영
2. I/O 구조
3. 인터럽트
4. 저장 구조

* 컴퓨터 시스템 I/O 운영
  * I/O 기기와 CPU 는 동시 실행 가능(DMA)
  * 각 장치 컨트롤러는 특정장치를 담당
    - 각 장치 컨트롤러는 로컬 버퍼가 존재
    - CPU가 주 메모리와 로컬메모리를 주고 받음
  * I/O 는 장치에서 컨트롤러 로컬 버퍼까지를 말함
  * 컨트롤러는 CPU에 인터럽트를 발생시켜 작동 완료되었음을 알림

* I/O 구조
  * I/O 트랜잭션은 버스를 통해 수행
    - 버스는 주소를 저장하는 병렬 와이어 모음. 데이터 및 제어 신호포함
    - system bus는 cpu와 i/o 브릿지를 연결
    - memory bus는 i/o 브릿지와 메모리를 연결
    - i/o bus는 여러 장치에 의해 공유
  * 일반적으로 dma 사용됨
    * cpu 개입없이 독자적으로 읽기 또는 쓰기 수행
    * cpu 사용 시 다른 작업을 수행할 수 있음

* 인터럽트
  * 인터럽트는 인터럽트 서비스 루틴으로 제어를 전송
  * 인터럽트 서비스 루틴의 주소는 인터럽트 벡터라는 테이블에 저장
  * 트랩은 오류 또는 사용자 요청으로 인한 소프트웨어적 인터럽트
  * 운영체제가 인터럽트 구동

* 인터럽트와 트랩의 차이점

  * 인터럽트

    프로세서 외부의 이벤트로 인해 발생(키보드의 ctrl + z)

  * 트랩

    * 소프트웨어 인터럽트 (시스템 콜, segmentation fault)

* 저장 구조

  * 주 메모리 - 하나의 큰 메모리로 cpu 직접 접근 가능

* 캐싱은 컴퓨터 시스템의 주요한 원리이다.
* 저장매체 접근 방법
  * 더 빠른 스토리지 (캐시)에 정보있는지 확인
  * 있는경우 캐시에서 직접 정보를 사용
  * 없으면 캐시에 복사후 거기에서 사용

* 현재의 os 는 듀얼 os 지원

  * 유저모드, 커널모드
  * mode bit(0) : 커널, mode bit(1) 유저
  * 잘못된 사용자로부터 운영체제 보호하기 위한 수단
    * privileged instruction - 커널모드에서만 실행가능

  * 유저모드에서 권한이 부여된 명령 실행시, 하드웨어가 실행하지 않음
    * i/o 제어 명령어
    * 인터럽트 명령

# Chapter 2

## OS 시스템의 서비스

* 유저
  * UI
  * 프로그램 실행
  * I/O 연산
  * 파일시스템 제어
  * 통신
  * 에러감지

* 효율성
  * 메모리할당
  * accounting(누가 메모리를 얼마나 사용하였는지)
  * 보호
  * 보안

* UI

  * CLI
    * 사용자가 운영체제에서 수행 할 명령을 직접 입력가능
    * 사용자로부터 명령어를 가져와 실행
    * 쉘이라고도 부른다.
    * 두가지 방법
      * 명령을 실행할 코드를 포함
      * 실행파일을 찾아서 실행

  * GUI
    * WINDOW, OSX, UNIX

## 시스템 콜

* 커널모드로의 접근

  * 인터럽트

  * 트랩

    * 소프트웨어가 커널로 가기위한 방법

      1. 예외
         * 0으로 나누기
         * 불법적인 기계코드
         * 불법적인 메모리접근

      2. 시스템콜

* 시스템콜 
  * 운영프로그램이 운영체제에서 서비스를 요청하는데 사용되는 메커니즘
  * Library as an itermediary(api를 통해 제공)

* 시스템콜을 직접 하지않고 api를 이용하는 이유
  * 이식성
  * 프로그래밍을 하기 쉽게(프로그래머가 시스템콜을 디테일하게 알지 않아도됨)

* system call interface
  * 시스템 콜에 대한 링크 역할
    1. 각 시스템 콜과 관련된 번호
    2. 이 번호에 따라 index된 테이블
    3. 시스템 콜을 호출하고 시스템콜의 상태와 반환값 전부 반환

* 시스템 콜에서 매개변수 전달하기
  * 매개변수를 레지스터에 전달(어떤경우에는 레지스터보다 많을 수 있음)
  * 매개변수를 메모리에 저장하고 메모리의 주소가 레지스터에 전달
  * 프로그램에 의해 스택으로 전달(push)될수 있음

* 시스템콜 유형
  * 프로세스 제어 (end, abort, create)
  * 파일 관리(create, open, r/w)
  * 기기 관리(r/w, get device attribute)
  * 상태 정보(get time, data)
  * 커넥션(send, receive message)

## os  구조

* simple structure
* layered opproach
* microkernel
* module
* vm

* simple structure

  * 특징
    * 모듈 또는 레이어로 분리 x(듀얼모드, h/w 보호기능 없음)
    * 인터페이스와 기능이 잘 분리 X

  * MS-DOS
  * 응용프로그램이 기본I/O 연산에 엑세스하여 기기에 직접 쓸수 있음\

* layered approach
  * 여러 계층으로 나뉘어져 있음
  * 각 계층은 하위 계층에서 제공되는 작업으로만 구현
  * 구성과 디버깅이 간편함

* microkernels

  * 커널에서 사용자 공간으로 많이 이동
  * 이점
    * 확장 용이
    * 운영체제를 새로운 아키텍쳐에 쉽게 포팅
    * 신뢰성 높음(커널모등체서 코드실행 감소)

  * 차단(단점?)
    * 메시지 전달의 성능 오버헤드

* modules
  * 특징
    * 각각의 핵심 구성요소 분리
    * 각각은 커널 내에서 필요시 따로 로드

* linux(layered + modules)에선 동적 로딩, 언로딩 지원
  * insmod - 커널에 모듈 삽입
  * rmmod - 커널에 모듈 제거

* vm

  * 각 프로세스에는 컴퓨터의 가상 복제본이 제공
    * 단일 컴퓨터의 하드웨어를 여러가지 다른 실행 환경으로 추상화

  * 동일한 하드웨어를 공유하면서 여러 운영체제를 동시 실행
  * 장점
    * 다른 os에서 동시 테스트 가능

  * 구현 어려움
  * 하드웨어 위에 virtualization layer가 올라가있음 ( 각각 커널 따로 가짐)
    * 여러 가상 시스템을 물리적 시스템으로 멀티프로그래밍

* bootstrap loader
  * 커널을 찾아 메모리에 적제하고 시작하는 작은 코드
  * 일부 시스템은 간단한 부트스트랩 로더가 디스크에서 복잡한 부트 프로그램을 가져옴
  * 컴퓨터 전원이 켜지면 rom에서 실행이 시작됨

# Chapter 3

* process - 메모리에 적재되어 실행되고 있는 프로세스
  * 스택 - 함수 매개변수의 임시 데이터, 지역 변수
  * 힙 - 동적 메모리 할당
  * PCB(프로세스 카운터, 레지스터)

* 프로세스상태
  * new
  * running
  * waiting - 이벤트 발생 대기
  * ready - 프로세서에 의해 할당 대기
  * terminate

* PCB
  * 프로세스 각각의 정보
    * 프로세스 상태
    * 프로그램 카운터(다음 수행)
    * CPU 레지스터
    * CPU 스케줄링 정보
    * 메모리 관리 정보
    * 메모리 사용량 정보
    * I/O 상태 정보(열린 파일)

## 프로세스 스케쥴링

* 프로세스 스케쥴링 큐
  * job 큐 - 시스템의 모든 프로세스 세트
  * ready queue - 주 메모리에 상주하며 실행 준비가 되어있고 대기중인 프로세스 집합
  * device queue - i/o 장치를 기다리는 프로세스 집합

* 프로세스는 i/o burst와 cpu burst를 바꿔가며 수행
  * i/o burst - i/o 요청 후 기다리는 시간
  * cpu burst - cpu 명령 실행 시간

* cpu bound process - cpu burst 가 더 큰 프로세스 ( 과학 계산용 프로그램)
* i/o bound process - i/o burst가 더큰 프로세스( 많은 프로세스들이 여기 속함)

* scheduler

  1. long-term scheduler(job scheduler)
     * ready queue에 포함할 프로세스 선택
     * 매우 드물게 호출
     * 멀티 프로그래밍의 정도를 제어함

  2. short-term scheduler
     * ready- queue에 있는 프로세스 중 running 할 프로세스 선택
     * cpu 효율을 위해 자주 빈번히 호출

  3. mid-term scheduler
     * 메모리에 로드되어있고 running 상태로 넘어가지 않는 프로세스 쫓아냄
     * 나중에 필요시 다시 메모리로 가져옴

* context switch
  * cpu가 다른프로세스로 전환되면 시스템은 이전 프로세스상태저장후 새 프로세스 적제
  * 전환시 시스템은 유용하지 않다.
  * 이러한 오버헤드를 줄이기 위한 메커니즘 존재

* 부모 프로세스는 자식 프로세스를 생성하며 트리를 형성.

* 이슈

  * 자원 공유
    1. 모든 자원을 부모와 자식이 공유
    2. 일부분 공유
    3. 공유  x

  * 실행
    1. 동시 실행
    2. 부모가 자식 끝날때까지 기다림

  * 주소 공간
    1. 자식은 부모의 주소공간 복제
    2. 자식은 적재되는 프로그램 가지고 있음

* 리눅스나 유닉스

  * fork 시스템콜

    * 자원을 공유함
      * 파일을 자식과 부모가 공유
      * cpu time, 메모리는 공유하지 않음

    * 동시에 실행
    * 주소 공간
      * 복제하지만 주소 공간을 분리(일반적으로 새 프로그램을 덮어씌움)
      * 처음에는 각 프로세스가 동일한 스택, 로컬 변수, 힙, 프로그램을 갖는다.

    * 한번 호출되고 두번 리턴(pid == 0 -> 자식)
    * 자식 프로세스 종료시까지 기다림

* 프로세스 종료

  * 마지막 명령문 실행하고 운영체제에 삭제 요청(exit)
    * 자녀로부터 부모 데이터 산출
    * 프로세스 자원이 할당해제

  * 프로세스는 자식 프로세스 실행을 종료할 수 있음
    * 자식프로세스가 할당 된 자원 초과시
    * 자식프로세스의 작업이 더 이상 필요 X
    * 부모 종료 시 
      * 일부 운영체제는 허용 X ( cascading termination)
      * 고아 프로세스

## IPC(프로세스 간 통신)

* 독립프로세스는 서로 영향 X
* 협력 프로세스는 영향 O
  * 파일 공유
  * 계산 속도 향상(병렬 컴퓨터)
  * 모듈화
  * 편의성

* IPC
  * message passing
  * shared memory

* 생산자 소비자 문제 - 동기화 필요

* shared memory
  * 프로세스B가 공유 리전 생성
  * 프로세스A가 영역을 자체 주소공간에 연결
  * 프로세스 A,B가 읽고 씀

* message-passing 

  * 공유변수 사용하지 않고 서로 통신
  * 두가지 작업
    * send
    * receive

  * 통신 링크를 세우고 메시지를 교환

* 링크 설정

  1. 직접 통신
     * 프로세스는 명시적으로 서로 이름을 지정해야한다.
       * send(p, message)
       * receive(q, message)
     * 링크 자동으로 설정
     * 각 쌍사이에 하나만 존재
     * 이름을 알수 있는 방법이 있을까(결함)

  2. 간접 통신
     * mailbox(포트라고 부름)를 통해 직접적으로 메시지 송,수신
       * 각각의 mailbox 는 유니크 id 존재
       * mailbox 공유 시에만 통신가능
     * mailbox 공유시에만 링크 설정
     * 링크가 많은 프로세스와 연관
     * 단방향 혹은 양방향

* mailbox 공유 이슈
  * p1,p2,p3 공유
  * p1 send, p2-p3 receive
  * 누가 받을것인가
  * 해결책
    * 최대 두개의 프로세스 링크 공유
    * 한번에 한 프로세스만 receive
    * 전부다 받기
    * 송신자가 수신자 선택 가능

* mailbox 동기화
  * blocking / non-blocking
  * blocking - 동기로 간주
    * mailbox에 의해 메시지 받았을때까지 송신자 정지(or 큐에 메세지 가득차있으면)
    * 이용 가능한 메시지 있을때까지 수신자 정지
  * non blocking - 비동기
    * 송신자는 보내고 다른 작업처리
    * 수신자는 유효메시지 받던가 혹은 null 을 받음

* shared vs message
  * message passing
    * 컴퓨터간 통신에 유용
    * 소량의 데이터 교환에 유용함
    * 시스템콜을 사용해서 구현하므로 시간을 더 많이 소요함
    * 프로그래밍이 더쉽다.
  * shared memory
    * 빠르다.
    * 보호 메커니즘이 필요함

# Chapter 4

* single vs multi-thread
* 이점
  1. 응답성
     * 프로그램의 일부가 차단되거나 장시간 작업 수행 중이여도 계속 실행
  2. 자원 공유
     * 쓰레드는  code, data, file을 공유(register, stack 은 각각) ->쓰레드마다 독립적인 실행흐름을 주기위해
  3. 경제적
     * 프로세스 생성을 위한 메모리 및 리소스 할당은 비용이 더 많이 듬
     * 쓰레드 context-switch는 캐시메모리 비울필요가 없어 더 빠름(캐시메모리에 프로세스 코드 명령이 들어있는데 쓰레드는 코드를 공유)
  4. 다중프로세스 아키텍처의 활용
     * 스레드가 다른 프로세스에서 병렬로 실행

* multicore programming
  * 데이터 병렬 - 전체 데이터를 쪼개 병렬 처리
  * 작업 병렬성 - 서로 다른 작업 처리

* 커널 쓰레드
  * 커널에 의해 필요에 따라 생성, 파괴
  * 프로세스가 각각 연관 필요 x
  * os에서 관리
* 사용자 쓰레드
  * 커널위에 지원되며thread library에 의해 관리
  * 커널 포함 x

* many to one model
  * 하나의 커널 쓰레드에 여러개의 유저 쓰레드
  * 빠르고 오버헤드 작음
* one-to-one model
  * 다중프로세서에서 다중쓰레드가 병렬로 실행되도록 허용
* many-to-many
  * 필요시에 많은 사용자 쓰레드 생성 가능
  * 병렬 수행 가능
* two - level
  * many-to-many + one-to-one

* thread library
  * 쓰레드 생성 및 관리를 위한 api제공
  * 두가지 방법
    * 사용자 공간에 완전히 제공
      * 라이브러리에서 함수 호출 시 시스템 콜이 아닌 사용자 공간에서 로컬 함수 호출
    * 운영체제가 직접 지원하는 커널 레벨 라이브러리
      * api 호출 시 시스템콜

* fork와 exec
  * fork 시 exec()이 즉시 호출되면 해당 쓰레드만 복제
  * 아니면 모든 쓰레드가 복제됨

* thread cancellation
  * 비동기식 취소
    * 취소시 target thread가 바로 종료
  * 지연된 취소
    * 취소시 주기적으로 종료싲점 검사하여 적절한 시기에 종료

* signal handling
  * 유닉스에선 특정 사건이 일어났음을 process에게 통보
    * 동기식 - 자신에 의해 생성된 신호(divided by zero)
    * 비동기식 - 외부에 의해 생성된 신호(ctrl z)
  * signal handler
    * default signal handler: 모든 신호마다 그것을 처리하는 handler 존재, 커널이 수행
    * user defined handler

* thread pools
  * 제한된 수의 스레드만 시스템에 허용
  * 작업을 기다리는 풀에 많은 스레드를 생성해놓음
  * 장점
    * 요청 시 생성보다 더 빠르다
    * 응용프로그램 thread 수를 제한할 수 있음

# Chapter 5

* Dispatcher
  * short-term scheduler 가 선택한 프로세스에게 cpu의 제어를 넘겨주는 모듈
    * switching context
    * switching to user mode
    * 프로그램 재시작을 위해 해당 주소로 이동
  * dispatcher latency - cpu제어권을 다른 프로세스에게 넘기는데 걸리는 시간

* 스케쥴링 기준
  * cpu utilization
  * throughput
  * turnaround time
  * waiting time
  * response time

## multi-processor scheduling

지금까진 단일 처리 시스템 스케줄방식

* symmetric multiprocessing - 각 처리기가 독립적으로 수행
* asymmetric multiprocessing - 하나의 마스터서버라는 처리기가 모든 스케쥴링과 입출력 다른 시스템 활동을 처리

* processor affinity
  * 프로세스를 다른 처리기로 이동하면 처리기의 캐시 메모리 내용또한 이주
  * smp시스템은 각 처리기에서 다른 처리기로 이동 피함
* load balaancing
  * smp에서 처리기가 하나 이상인 것을 활용하려면 부하를 균등하게 배분
  * push와 pull 방식으로 접근

### 스케쥴링

- cpu utilization
- throughput 시간당 완료되는 프로세스 수
- turnaround time
- waiting time : 준비완료 큐에서 대기한 시간(첫 프로세스 실행 시 다시 대기한다면 그것도 포함시켜야됌)
- responste time: 서비스 요청 후 첫 실행까지 시간

#### FCFS(First Come First Served)

- 먼저 온 고객을 먼저 서비스해주는 방식, 즉 먼저 온 순서대로 처리.
- 비선점형(Non-Preemptive) 스케줄링
- convoy effect
  소요시간이 긴 프로세스가 먼저 도달하여 효율성을 낮추는 현상이 발생한다.

### SJF(Shortest - Job - First)

- 다른 프로세스가 먼저 도착했어도 CPU burst time 이 짧은 프로세스에게 선 할당
- 비선점형(Non-Preemptive) 스케줄링
- 평균 대기시간에서 최적
- starvation

#### SRT(Shortest Remaining time First)

- 새로운 프로세스가 도착할 때마다 새로운 스케줄링이 이루어진다.
- 선점형 (Preemptive) 스케줄링
  현재 수행중인 프로세스의 남은 burst time 보다 더 짧은 CPU burst time 을 가지는 새로운 프로세스가 도착하면 CPU 를 뺏긴다.
- starvation
- 새로운 프로세스가 도달할 때마다 스케줄링을 다시하기 때문에 CPU burst time(CPU 사용시간)을 측정할 수가 없다.

#### Priority Scheduling

- 우선순위가 가장 높은 프로세스에게 CPU 를 할당하겠다. 우선순위란 정수로 표현하게 되고 작은 숫자가 우선순위가 높다.
- 선점형 스케줄링(Preemptive) 방식
  더 높은 우선순위의 프로세스가 도착하면 실행중인 프로세스를 멈추고 CPU 를 선점한다.
- 비선점형 스케줄링(Non-Preemptive) 방식
  더 높은 우선순위의 프로세스가 도착하면 Ready Queue 의 Head 에 넣는다.
- starvation
- aging
  아무리 우선순위가 낮은 프로세스라도 오래 기다리면 우선순위를 높여주자.

#### Round Robin

- 현대적인 CPU 스케줄링
- 각 프로세스는 동일한 크기의 할당 시간(time quantum)을 갖게 된다.
- 할당 시간이 지나면 프로세스는 선점당하고 ready queue 의 제일 뒤에 가서 다시 줄을 선다.
- `RR`은 CPU 사용시간이 랜덤한 프로세스들이 섞여있을 경우에 효율적
- `RR`이 가능한 이유는 프로세스의 context 를 save 할 수 있기 때문이다.
- `Response time`이 빨라진다.
  즉, 어떤 프로세스도 (n-1)q time unit 이상 기다리지 않는다.

설정한 `time quantum`이 너무 커지면 `FCFS`와 같아진다. 또 너무 작아지면 스케줄링 알고리즘의 목적에는 이상적이지만 잦은 context switch 로 overhead 가 발생한다. 그렇기 때문에 적당한 `time quantum`을 설정하는 것이 중요하다.

#### 다중레벨 큐

- 준비 큐를 여러개의 큐로 나누어 사용
- 각 큐는 독자적인 스케쥴링 알고리즘 사용
- time slice방법으로 starvation 해결

#### 다중레벨 피드백 큐

- 큐간 스레등 가능

# Chapter 7

* race condition 

  * 여러 프로세스가 동일한 데이터에 동시에 엑세스하고 조작

* critical section
  * 병렬컴퓨팅에서 둘 이상으 스레드가 동시에 접근해서는 안되는 공유 자원을 접근하는 코드
  * 해결방법
    1. mutual exclusion
       * 하나의 프로세스가 임계영역안에있으면 다른 프로세스는 진입 불가
    2. progress
       * 임계영역을 사용하고 있지 않다면, 다른 프로세스가 접근 가능
    3. bounded waiting
       * 임계영역 진입 횟수에 한계가 있어서 같은 프로세스가 계속 독점 사용 못하게 함

* peterson's solution

  * turn == i 이면  Pi 가 임계영역에서 실행 차례라는것

  * flag[i] == true 이면 Pi는 임계구역 진입 준비가 되었다는것

  * 단점은 busy waiting, 구현 어렵다.

  * ```
    do {
        flag[i] = TRUE;
        turn = j //j가 먼저 쓰고싶은지 확인하기 위해
        while (flag[j] && turn == j); //spin lock
         critical
        flag[i] = false;
    }while(1)
    ```

* swap사용

  * ```
    while(1){
        key = true;
        while(key == true)
        	swap(&lock,&key);
        //critical
        lock = false;
    }
    ```

## 세마포어

* semaphore S - 정수값

* wait, signal 함수 사용

* 덜 복잡하다

* ```
  wait (S) {
  	while S <= 0; // no-op	
  	S--; // s 0으로 만들어 락검
  }
  ```

* ```
  signal (S) {
  S++;
  }
  ```

* ```
  Semaphore S; // initialized to 1
  wait (S);
  	Critical Section
  signal (S);
  ```

* 단점: spin lock, busy waiting -> context switch를 줄이지만 긴 시간동안 lock 얻지 못하면 잠시 sleep 하는 알고리즘이 더 좋다.(while을 통해 값을 확인도 cpu 자원 낭비)

* busy waiting 없는 세마포어

  * waiting queue 와 연계. value 와 다음 리스트에 대한 포인터를 가진 큐존재

  * 두가지 연산

    * block - 호출한 프로세스를 정지시킴. waiting queue에 넣음
    * wake-up - 프로세스를 reqdy queue 에 넣음

  * ```
    wait (semaphore *S)
    	S->value--;
    	if (S->value < 0) {
    		add this process to S->list;
    		block();
    	}
    }
    ```

  * ```
    signal (semaphore *S)
    	S->value++;
    	if (S->value <= 0) {
    		remove a process p from S->list;
    		wakeup(P);
    	}
    } 
    ```

* dead lock - 두개 이상의 프로세스가 대기중인 프로세스 중 하나에서만 발생할수 있는 이벤트롤 무기한 대기중.

* Starvation – 일시 중단된 세마포어 대기큐에서 프로세스 제거 불가능.

* 식사하는 철학자

  1. 왼쪽 포크 -> 오른쪽 포크 -> 왼쪽 내림 -> 오른쪽 내림
     * 모두가 왼쪽을 들면 데드락
  2. 왼쪽 포크 -> 오른쪽 포크 들수있나 확인 -> 못들면 왼쪽도 포기 
     * 동시 왼쪽들면 다 다시 내리고 다시 왼쪽
     * 기아문제 발생
  3. 왼쪽포크 -> 오른쪽 포크 있나 확인 -> 못들면 랜덤시간 기다림
     * 낮은 확률 starvation
     * 완벽한 프로그램에 사용불가
  4. 이진 세마포어로만 포크를 드는 행위를 감싼다. 어느 한 순간에는 한 프로세스만이 포크 듬 
     * 반대편은 포크 못든다
     * 각 프로세스별로 세마포어를 따로 두어 최대한 많은사람들이 식사하게끔 만듬

# Chapter 8

* 데드락 필요 조건
  * mutual exclusion
  * hold and wait - 프로세스 할당된 자원가진 상태에서 다른 자원 기다림
  * no preemption - 프로세스가 어떤 자원 사용 끝날때까지 그 자원 선점 불가능
  * circular wait - 프로세스는 순환적으로 다른 프로세스가 요구하는 자원 가지고 있음

## Deadlock 핸들링

* 데드락 피하거나 예방
* 데드락 허용 후 회복
* 자주 발생하지 않는 현상이며 위에 방법은 비용이 많이 들기 때문에 무시

## Deadlock 예방

* mutual exclusion 부정
  * 꼭 같이 써야하는 리소스가 아니라면 공유되는 리소스를 hold 하지 않는다.
* hold and wait 부정
  * 프로세스가 어떤 리소스 요청시 다른 리소스 hold 하지 않은 상태여야 한다.또는 필요한 요청과 할당이 완료된 다음 실행. 속도느리고 starvation 발생
* no preemtion 부정
  * 어떤 프로세스가 리소스 점유 상태에서 지금 당장 할당 될 수 없는 리소스를 요청 하는 경우 리소스 해제 해버린다. 필요 리소스를 리스트에 추가하고 프로세스는 wait 상태로 감
* circular wait 부정
  * 모든 리소스 타입에 번호를 메겨 순서대로 할당. 높은 순서의 리소스를 받았을 경우 이전 순서 요청 x해버리면 됨

## Deadlock 회피

시스템이 unsafe  상태로 안가면됨. 프로세스가 리소스 요청 시 해당 리소스 즉시 할당 해 줄 수있는 상태가 safe 상태. 하지만 unsafe 하다고 deadlock이 무조건 발생하는것은 아니다.

* single instance 일때는 Resource allocation graph 이용
* banker's algorithm

## Deadlock 탐지

* single instance 일 때는 resource allocation graph 이용
* multi 일 때는 뱅커스 알고리즘과 유사한 알고리즘 이용

## Deadlock 회복

* 희생자 선점, rollback, starvation 고려 필요

1. 프로세스 중지
   * 교착상태 프로세스 모두 중지
   * 교착 상태 풀릴 때까지 하나씩 중지
2. 자원 우선순위 할당

# Chapter 8

* address binding
  * 프로그램을 작성할때 프로그래머는 기호 주소를 사용. 변수를 선언하고 변수 이름으로 접근.
  * 프로그램은 실행전 이런 기호주소를 실제 주소로 바인딩
  * symbolic -> relocatable address -> absolute address
  * symbolic address(address in source code) -> count variable
  * relocatable addrss(compiler) -> 14 byte from the beginning of this module
  * absolute addresss(oinkage editor) -> 74014

* 주소 바인딩 시기
  * 컴파일 시간(Compile time)
      * 컴파일러가 프로세스가 어디에 적재될지 알고 있으면 컴파일할 때 주소를 바인딩
      * 물리적인 메모리가 많이 비어있어도 주소 변경x
      * 변경할 수 없으므로 컴파일된 코드를 absolute address라고 한다
  * 적재 시간(Load time)
      * 컴파일할 때 프로세스가 어디에 적재될지 모르면 컴파일러는 재배치 가능 코드를 생성
      * 재배치 가능 코드라고 해서 relocatable address
  * 실행 시간(Execution time)
      * 실행 도중에 프로세스의 적재 위치가 바뀔 수 있으면 바인딩은 실행될 때 이루어진다.
      * MMU라는 하드웨어 지원이 필요

* MMU(Memory Management Unit)
  * h/w 기기로 논리주소를 물리주소에 매핑
  * 두가지 레지스터를 이용하여 매핑
    * relocation register
      * 접근할 수 있는 물리적 메모리 최솟값
    * limit register
      * 논리적 주소가 존재할 수 있는 범위(벗어나는 주소를 요청시 trap)

* dynamic loading
  * 호출 시까지 루틴 적재 x
    * 메모리 공간 효율이 좋다
  * 에러 루틴과 같은 희귀한 상황이 발생하여 이를 통제하기 위해 많은 코드가 필요한 경우 유용
  * os에서 특별한 지원이 필요없다. library 형태로 지원
* dynamic linking
  * 프로그램 실행 시 까지 linking 미룸
  * 작은 코드조각을 stub이라 부름
  * stub이 라이브러리가 필요한 부분에 있다가 stub이 실행되면 라이브러리부분을 링킹
  * os지원필요
    * os는 루틴이 다른 프로세스가 사용중인지 체크
  * shared library 사용
    * 라이브러리가 빌드될 때 포함 x
    * 다시 빌드하지 않고 라이브러리 업데이트 가능

## Contiguous Allocation

* 주 메모리
  * os 올림
  * 사용자 프로세스
* 메모리 매핑과 보호
  * relocation register
  * limit register
  * mmu

* 다중파티션 allocation
  * hole
    * 가용 메모리의 블록
    * 크기 다양
  * 프로세스 도착시, 충분히 받아들일 수 있는 크고 비어있는 hole에 할당
  * os는 아래의 정보를 유지
    * 할당 부분
    * 비어있는 부분(hole)
* 동적 저장소 배당
  * first-fit: 처음 hole
  * best-fit: 할당 가능한 가장 작은 hole. 리스트한번 탐색해야함
  * worst-fit: 가장 큰 hole

* 단편화
  * 외부 단편화 - 유휴 공간들을 합치면 충분한 공간이 되지만 작은 조각들로 여러곳에 분산
  * 내부 단편화 - 메모리 할당시 필요 메모리보다 조금 더 크게 할당. 내부에 쓰지않고 남는 공간이 생김
  * compaction(압축) - 메모리 공간들을 재배치하여, 분산되있는 메모리 공간들을 하나로 합침

## paging

* non-contiguous
* 물리적 주소를 고정된 주소인 frame 단위로 잘라 넣는다.(2의 지승, 512~8192byte)
* 논리적 주소를 페이지라는 똑같은 크기의 블럭으로 분할
* 페이지테이블을 이용하여 논리적주소를 물리적주소로 변환
* 내부단편화 발생
* paging
  * page number - 페이지 테이블의 인덱스로 사용. 물리 메모리에서의 각각 페이지의 기본 주소로 포함
  * page offset - 기본 주소와 결합되어 메모리 장치로 전송되는 물리적 메모리 주소 정의
  * logical address가 2의 m승, physical address가 2의 n승이면, m-n비트가 페이지 넘버구분, 나머지 n 비트가 offset
* frame table
  * 어떤 프레임이 할당되고 할당되지 않았는지
  * 총 몇개의 프레임이 존재하는지
* 하드웨어 지원
  * 레지스터 사용
    * 페이지 테이블은 주메모리에 존재
    * page table base register 은 페이지테이블 주소를 레지스터에 보관
    * page table length register은 페이지 테이블 크기를 가르킴
    * 프로그램에 의한 메모리 접근은 실제 주소를 얻기 위한 페이지 테이블 접근 + 데이터를 얻기 위한 접근 총 2가지
  * TLB
    * 고속 캐쉬인 tlb를 이용하여 두번 접근 문제 막음
    * 최근 사용되었던 page table entry 저장
    * tlb hit면 frame number가 검색
    * hit 안되면 페이지 테이블 다시 검색하고 tlb 업데이트

* 메모리 protection
  * read/write 비트가 있으며 i/o작업 시 read only로 표시 가능.
  * valid-invalid 비트. 잘못된 접근이 있으면 트랩 발생.
* shared page
  * 중복 코드가 있을 경우 sharing 하는 것이 가능. pure code라고 한다. 2개 이상의 프로세스가 같은 코드에 동시에 실행 되지만 data프레임은 공유 x

* two level page table
  * 페이지 테이블 두개필요
  * 메모리 사이즈 줄여짐
  * 접근 시간 늘어남
* inverted page table
* segmentation
  * 프로세스를 세그먼트의 집합으로 생각함
  * 논리적 내용의 단위로 자르기 때문에 크기가 같지 않다.
  * segment-table base register
  * segment-table length register
  * <segment-number, offset>
  * segment table
    * base - 물리적 주소의 시작점을 포함
    * limit - 특정 세그먼트의 길이

# Chapter 9

## Demand paging

* 오직 필요할 때만 페이지를 메모리로 가져옴

* lazy swapper - 필요하지 않은 페이지는 메모리에 swap하지 않는다.

* 다중 page faults를 일으킬 수 있다.

* swapper vs pager

  * swapper는 전체 프로세스 관리
  * pager는 각각의 페이지와 연관

* valid & invalid bits

  * page table에는 bit가 결합되있음
  * v이면 메모리에 존재 i이면 존재x

* page-fault trap

  1. 페이지 테이블 확인 후 i 이면 트랩 발생

  2. 디스크에 있는 페이지에 대한 참조인지 아닌지 확인. 후자이면 종료.

  3. 비어있는 페이지 프레임을 찾는다.

  4. 프레임에 해당 페이지 로드 후 , 테이블 업데이트(valid bit =  v)

## Page Replacement

* replacement
  * 목표 - 페이지 폴트 최소화
  * 중요한 페이지를 하면 성능 나빠짐
  * victim 설정
  * 원리
    1. 디스크에서 요구된느 페이지 위치 찾음.
    2. 비어있는 프레임 있으면 사용
    3. 없으면 victim 프레임 선택
    4. 프레임에 페이지 올린후, 업데이트
    5. 프로세스 재시작

* FIFO
  * 메모리에 적재된 시간이 가장 오래된 페이지 교체
  * 구현 간단, 성능 보장 X
  * Belady의 모순: 프레임 갯수가 많아지더라도 페이지 부재율이 높아지는 현상
* 최적의 알고리즘
  * 앞으로 가장 오랜시간 사용되지 않을 페이지 찾아 교체
  * belady 모순 발생 x.하지만 어려움
* LRU
  * 가장 오래전에 참조한 페이지가 victim
  * 최적 알고리즘에 근사한 알고리즘. 각 페이지마다 마지막 사용시간 유지
  * 구현
    * counter
      * 모든 페이지 마다 카운터 존재.
      * 교체가 필요시, 모든 카운터들을 봄
    * stack
      * 더블링크드리스트를 이용하여 페이지 스택 유지
      * 페이지 참조 시
        * top에서 삭제
        * 바꾸기 위해 포인터 6개 필요
      * 서치 필요 x
* LRU - approximation
  * reference bit 사용 - 하드웨어 지원 없이 제공하기 위해 bit형태 지원
  * 페이지 마다 reference bit(8bit)를 두어 일정 간격마다 접근 되었던 페이지들 비트를 오른쪽으로 shift하는 연산
  * 가장 큰 bit를 가진 페이지가 최근 access
  * second chance algorithm
    * fifo 기반
    * 페이지 마다 1비트 reference bit 존재 초기값 모두 0, 접근 시 1
    * fifo 기반 이므로 bit 가 1이여도 선택됨
    * bit 가 1일 경우 최근 access 되었다고 판단하여 0으로 변경 후 다른 페이지 찾음
  * enhanced second-chance algo
    * (refernce bit, modify bit) -> 참조 됬는지 , 내용 수정 됐는지.
    * 1 class (0,0)
    * 2 class (0,1)
    * 3 class (1,0)
    * 4 class (1,1)
    * 낮은 번호의 클래스 부터 교체
* counting-based page
  * 참조 횟수
  * lfu - 참조 적
  * mfu - 참조 많
  * 비용 많이 들고 , 최적에 근사하지 않아서 사용x

## Thrashing

* 프로세스가 충분한 페이지를 가지고 있지 않으면, 페이지 부재율이 매우 높음 -> 페이지 교체에 시간을 많이 사용
  * cpu utilizaion 낮음
* 멀티프로그래밍 정도에 따라 cpu utilization이 높아지다가 확낮아지는 부근 쓰레싱!
* locality model
  * 쓰레싱 막기 위해 프로세스가 필요한 만큼 프레임 제공
  * 측정하는 방법은 locality model 사용

## Allocationg kernel memory

* user memory랑 처리 다름
* 주로 free-memory pool 에서 할당
  * 커널은 다양한 사이즈 요청
  * 어떤 커널은 연속된 메모리가 필요
* buddy system
  * 물리적으로 인접한 페이지로 구성된 고정 크기 세그먼트 메모리를 할당
  * 2의 제곱 할당자를 사용하여 할당된 메모리
    * 요청은 2의 제곱으로 된 단위
    * 각 리스트는 1, 2, 4, 8~~~ 개로 구성된 그룹을 담음
    * 256 요청했는데 1024-피이지-프레임 밖에 남는 곳이 없다면 256개 쓰고 나머지 768개중 512를 512 리스트에 남은 256개를 256리스트에 넣음
    * 외부단편화 막음
* slab allocation
  * slab은 하나 혹은 여러 물리적 연속된 페이지
  * 캐쉬는 하나혹은 여러 슬랩들의 구성
  * 두가지 상태
    * 캐쉬 생성시 , 객체를 free로 마크
    * 저장시, used로 마크
    * 모두 used이면, 다음 슬랩으로 이동 -> 없으면 새로운 슬랩 생성
  * 내부단편화 없음.

# 기타

## 자바

* 특징
  * 객체지향언어
  * 자동 메모리 관리
  * 멀티쓰레드 지원 
  * 동적 로딩 지원

* jvm
  * java byte code를 os에 맞게 해석해줌
  * 자바 컴파일러 -> .java를 .class 라는 byte code로 변환 -> jvm이 os가 이해하도록 해석
  * 해석을 거치기 때문에 느렸지만 JIT(JUST IN TIME)컴파일러를 통해 극복
  * 특징
    * os에 독립적인 플랫폼
    * 프로그램의 메모리를 알아서 관리해줌

## 안드로이드

* 4가지 구성요소
  * 액티비티
    * 사용자 인터페이스 구성하는 기본 단위. 프래그먼트나 뷰로 구성
  * 서비스
    * 백그라운드에서 무한히 실행되는 컴포넌트(미디어 플레이어 노래)
    * ui가 없기 때문에 액티비티와 연결되서 사용
  * 브로드캐스트 수신기
    * 시스템범위의 브로드캐스트 알림에 응답하는 구성요소(베터리 부족, 네트워크 전송 완료, 사진캡쳐)
    * 격리된 실행 환경에서 컴포넌트 끼리 통신
  * 콘텐츠 제공
    * 공유된 앱 데이터 집합 관리.
    * 적절한 권한을 가진 앱이라면 콘텐츠 제공자의 일부를 쿼리하여 특정 정보 읽고 쓰기 가능
  * 인텐트
    * 컴포넌트간의 메시지 주고 받는 전달자 역할
    * 각 컴포넌트를 호출, 실행 가능
* 안드로이드 생명주기
  1. oncreate()
     * 액티비티 처음 생성시 호출
     * 주로 view를 만들거나 data to list등 담당. 이전 상태정보 담고있는 bundle 제공
  2. onstart()
     * 액티비티가 사용자에게 보여지기 직전에 호출
  3. onresume()
     * 액티비티가 화면에 보여지게 되며 사용자로부터 어떠한 동작도 받지 않았을 때 호출
  4. onpause()
     * 해당 액티비티를 다른 액티비티를 전환 시킬 때 보내는 첫번째신호. 전환 전에 저장 되지 않은 데이터를 다시 돌아오지 않을 것을 우려하여 이 메소드 호출될 때저장
  5. onstop()
     * 액티비티가 더이상 사용자에게 보이지 않을 때 호출되는 메소드. 다른 액티비티로 전환 시 스택에 다른 액티비티가 쌓여 가려지게 되면 호출됨
  6. ondestroy()
     * 액티비티 종료 시 호출

## 유니티

* 리지드바디
* 뷰포리아

### MVC

mvc 이전의 전통적인 방법

- 개발 속도가 빠르고 개발자의 스킬이 낮아도 배우기 쉽다.
- 한 페이지가 너무 복잡해진다.
- 개발자와 디자이너의 분리작업이 어려워진다.
- 유지보수 어렵다.

mvc 는 각각의 역할을 나누어 작업하고자 하는 일을 분담.

- controller - 클라이언트 요청을 받았을 때 그 요청에 대해 실제 업무 수행하는 컴포넌트 호출. 클라이언트 보낸 데이터를 모델에 전달하기 쉽게 가공. 모델이 업무를 마치면 그 결과를 뷰에 전달
- model - 컨트롤러 호출 시, 요청에 맞는 역할 수행. 비즈니스 로직 구현 영역으로 데이터 처리하는 부분.
- view - 결과갑을 통해 사용자에게 출력할 화면 생성

## JS

JS엔진은 stack, task queue, heap 영역으로 나뉨. js 엔진은 javascript로 작성한 코드 해석하고 실행하는 인프리터

- call - stack : 자바스크립트는 단 하나의 호출 스택을 사용.(하나 함수 실행시 다른 task 수행 불가)
- heap - 동적으로 생성된 객체는 힘에 할당
- queue - 처리해야 하는 task들 임시 저장

### hoisting

변수의 정의가 그 범위에 따라 선언과 할당으로 분리, 즉 변수가 함수 내에 정의 되었을 경우, 선언이 함수의 최상위로. 함수 바깥에서 정의되었을 경우, 전역 컨텍스트의 최상위로 변경이 됨.



js 대부분 작업이 비동기로 이루어짐.

-> async/await 비동기 코드를 작성하는 새로운 방법

기존엔 promise 사용 but 규모가 커지면 어려워짐

### Arrow function

간결하게 함수를 표현. 항상 익명이며 자신의 this, super등을 바인딩하지 않기 때문에 사용자로서 사용 x

## Front-end

### 브라우저 동작원리

1.html 마크업 처리, dom 트리 빌드(무엇을 그릴지 결정)

2.css 마크업 처리하고 cssos트리 빌드(어떻게 그릴지 결정)

3.dom및 cssom결합 렌더링 트리 형성(화면에 그려질 것만 결정)

### CORS

리소스 요청시 해당 리소스는 cross-origin http요청에 의해 요청된다.

### 클라이언트 사이드 렌더링 & 서버 사이드 렌더링

웹 페이지, 모바일 웹에 대한 기능 -> single page web app

spa는 브라우저에 로드되고 난 뒤 페이지 전체를 서버에 요청하는 것이아니라, 한번 페이지 전체 로딩 후 데이터만 변경하요 사용하는 웹앱. 전통적인 웹 방식(서버 사이드) 보다 성능 좋음.

spa는 트래픽을 감소시키고 더 나은 경험 제공. 서버는 단지 json 파일 보내주는 역할을 했고, html은 클라이언트 측에서 자바스크립트가 수행하게 된것. 클라이언트 쪽이 느려지자 이에 반대로 view 만 관리하자는 철학으로 react가 등장.

## NOSQL

현재 not only sql로 설명. 기존의 관계형 db특성 뿐만 아니라 다른 특성도 부가적으로 지원. 융통성있는 데이터 모델 사용하고 저장 및 검색을 위한 특화된 메커니즘 제공. 단순 검색 및 추가작업에 있어서 키 값 저장을 통해 빠른 응답속도와 처리효율 보임

## React

ui를 만드는 자바스크립트 라이브러리.

가장 큰 특징은 UI를 여러 컴포넌트로 쪼갠다.여러 화면에서 재사용 가능

**DOM**: document object model. <html><body> 같은 html 문서 태그들을 객체로 만듬. document 객체와 관련된 객체의 집합

html 파일을 웹브라우저에서 오픈 -> dom 생성 -> 브라우저에서 표시. => 보통 dom을 조작하여 웹을 동적으로 구성 => 조작시 dom 재시작으로 시간도 오래걸리고 자원도 많이 먹음

=> react는 가상의 dom을 만들고 변경사항이 있을때마다 전체가 아닌 부븐의 dom에만 반영.

react는 view 의 값을 view에서 변경하지 못하고 state를 거쳐서 다시 와야하는 구조

## Docker

컨테이너 기반 오픈소스 가상화 플랫폼

기존의 os 가상화: host os 위에 guest os를 두어 성능에 문제가 있음 

호스트와 OS자원 공유. host os와 컨테이너의 os 의 다른 부분만 container안에 같이 패킹됨. container 내 명령어 수행시 실제로는 host os에서 명령어 수행. 즉 host os의 process공간 공유.

계층화된 파일 시스템 사용하기 때문에 가상화된 컨테이너 변경사항 모두 축적하고 관리. 따라서 필요시 언제 어디서나 실행 가능

도커파일: DSL언어 이용하여 생성. 서버에 프로그램 설치위해 의존성 패키지 설치 필요없이 dockerfile로 관리

이미지: 컨테이너 실행에 필요한 파일과 설정값 (유니온 파일시스템을 통한 레이어)

## KUBERNETES

### kubernetes란

컨테이너 운영환경을 돕는 솔루션

### 마스터와 노드

마스터: 쿠버네티스 클러스터 전체를 컨트롤하는 시스템 api 서버, 스케쥴러, 컨트롤러 매니져, etcd로 구성

노드: 마스터에 의해 명령을 받고 실제 워크로드를 생성하여 서비스하는 컴포넌트. kubelet, kube-proxy,cAdvisor 등이 포함

kubelet - 마스터의 api서버와 통신하며, 노드가 해야할 명령 수행하고 노드 상태등을 마스터로 전달

kube-proxy - 노드로 들어오는 트래픽을 적절한 컨테이너로 라우팅. 로드밸런싱등 노드로 들어오고 나가는 트래픽을 프록시하고 노드-마스터 간의 통신 관리

### 오브젝트

가장 기본적인 pod, service, volume, namespace 4가지가 있다.

#### pod

가장 기본적인 배포단위로 컨테이너를 포함하는 단위. 여러 컨테이너 포함.

파드내의 컨테이너는 ip와 포트 공유. 또한 디스크 볼륨 공유

#### volume

pod가 기동할때 디폴트로, 컨테이너마다 로컬 디스크를 생성해서 기동. but 영구적이지 못함. 그래서 파일을 영속적으로 저장하기 위한 스토리지를 두는데 그것을 볼륨이라고 한다.

#### service

pod를 서비스로 제공할때, 여러개의 pod를 서비스 하면서, 로드밸런서를 이용하여 하나의 ip와 port로 묶어 서비스 제공. 파드는 장애시 재시작되고, 동적으로 생성되서 ip가 변하기 때문에 로드밸런서에서 pod지정시 ip로하긴 어려움. 그래서 label, label selector 이용

- emptyDir : pod 생성시 생성, 삭제시 삭제되는 임시볼륨.
- hostPath : 로컬디스크의 경로를 pod에서 마운트해서 사용. pod 재시작하여 다른 노드 기동시, 그노드 hostpath 사용하기 때문에 액세스 불가.
- persistentVolume and persitentVolumeClaim: 시스템 관리자가 실제 물리디스크 생성 후 이 디스크를 pv라는 이름으로 쿠버네티스에 등록.개발자는 pvc를 지정하여 pv에 연결

#### namespace

한 쿠버네티스 클러스터의 논리적인 분리단위. 사용자별로 네임스페이스별 접근 권한 달리 운영가능. 리소스의 할당량 지정 가능. 리소스 (파드, 서비스)등을 나눠서 관리할 수 있다.

논리적인 단위이므로 다른 네임스페이스간 pod라도 통신 가능

### 라벨

라벨은 쿠버네티스의 리소스 선택하는데 사용이 됨. 리소스는 라벨을 가질 수 있고, 라벨검색 조건에 따라 특정 리소스만 선택가능. 여러개의 라벨 동시적용 가능.

### 컨트롤러

#### replica controller

pod 관리해주는 역할, 지정된 숫자로 pod 실행,관리.

- selector: 라벨을 기반으로, rc가 관리한 pod 가지고오는데 사용
- replica 수: rc에 관리되는 pod의 수
- 어떻게 pod를 만들지 pod에 대한 정보를 pod template 부분에 정의

#### replicaSet

rc의 새버전.

큰 차이는 없고 Replication Controller 는 Equality 기반 Selector를 이용하는데 반해, Replica Set은 Set 기반의 Selector를 이용

#### Deployment

위의 2개 보다 좀더 상위 추상화 개념.

블루그린 배포: 블루버전 서비스를 그린버전으로 새롭게 배포후 트래픽을 한번에 돌리는 방식

롤링업그레이드: 파드를 하나씩 업그레이드 해나가는 방식

#### DaemonSet

pod가 각 노드에서 하나씩만 돌게하는 형태로 관리하는 컨트롤러. 주로 서버 모니터링이나 로그 수집용도로 사용

#### Job

배치나 한번실행되고 끝나는 형태의 작업에 사용.job에 의해 관리되는 pod는 job종료시 같이 종료

#### StatefulSet

데이터베이스와 같이 상태를 가지는 애플리케이션 관리를 위해 사용.

loadbalancing: 하나의 서비스가 발생하는 트래픽이 많을때 여러 대의 서버가 분산처리하여 해결해주는 서비스

### SERVICE TYPE

- loadbalancer: 외부 ip를 가지고 있는 로드밸런서 할당.
- cluserIP: 디폴트 설정으로, 서비스에 클러스터 ip(내부 ip) 할당. 외부에서 접근 불가.
- nodeport: 노드의 ip와 port를 통해서 접근.
- externalname: 외부서비스를 쿠버네티스 내부에서 호출시 사용 가능.

### INGRESS

서비스 앞에 붙어서 다른 서비스로 라우팅해줌. 사용하려면 nodeport 타입으로 배포

### 헬스체크

- liveness probe: 컨테이너 생존 여부 체크
- readiness probe: 서비스 가능 상태 체크

probe types

- command probe: 쉘 명령을 수행후 여부 체크
- http probe: http get을 이용하여 상태체크
- tcp probe: tcp 연결 시도후 판단

### 모니터링

#### cAdvisor

각 노드마다 설치되서 노드에 대한 정보를 수집하여 kubelet으로 전달

#### heapster

수집된 지표는 heapster라는 시스템에 모이게되고, heapster는 수집된 지표를 백엔드에 저장.

모티터링 대시보드는 쿠버대스보드 or 프로메테우스 + 그라파나

# 객체

OOP
	프로그래밍 패러다임중의 하나로 프로그래밍에 필요한 데이터를 추상화시켜 객체를 만들고 그 객체들 간의 상호작용을 통해 로직을 구성하는 프로그래밍 방법입니다.

**클래스** : 어떤 문제를 해결하기 위한 데이터를 만들기기 위해 추상화를 거쳐 집단에 속하는 **속성**(attribute)과 **행위**(behavior)를 **변수**와 **메서드**로 정의한 것

**인스턴스(객체)** : 클래스에서 정의한 것을 토대로 실제 메모리상에 할당된 것으로 실제 프로그램에서 사용되는 데이터

추상화<br>	객체에서 공통된 속성과 행위를 추출

캡슐화
	불필요한 정보는 숨기고 중요한 정보만 표현
	내부의 구현은 감추고 모듈 내에서 응집도를 높임
	외부로의 노출을 최소화하여 모듈간의 결합도를 떨어뜨려 유연함과 유지보수성을 높임

상속
	부모의 특성과 기능을 그대로 물려받는 것
	기능의 일부를 변경 - 오버라이딩
	캡슐화를 유지하면서도 클래스의 재사용이 가능

다형성
	하나의 변수명, 함수명 등이 상황에 따라 다른 기능을 수행하는 것
	오버로딩 오버라이딩

객체지향 프로그래밍의 장점
	코드 재사용 용이 - 남이 만든 클래스를 가져와서 이용할 수 있고 상속을 통해 확장하여 사용할 수 있음
	유지보수가 쉬움
	대형 프로젝트에 적합 - 모듈화시켜서 업무 분담 후 개발

객체지향 프로그래밍의 단점
	처리속도가 상대적으로 느림
	객체가 많으면 용량이 커짐
	설계시 많은 시간과 노력이 필요

const
	const int a - 상수
	const int* a - 포인터가 가르키는것 상수
	int* const a - 포인터 자체 상수
	

```
void aaa() const - 멤버 값 변경 불가능한 함수
const AAA aaa(10) - 멤버변수 접근 불가 상수함수만 접근 가능
```

static
	static int a - 전역
	멤버변수 static int a - 클래스에서만 접근 가능한 전역
	int AAA::a=1; 전역변수 초기화 문법
	
virtual function
	virtual 키워드를 함수 앞에 붙임으로써 만들어지는 함수. 

가상함수 생성시 자식 클래스에게 vPtr을 맴버로 (몰래) 생성. vTable에 가상 함수와 함께 등록

단점

- 클래스 크기에 4바이트가 더 들어간다(가상 함수 포인터)
- memset 등 메모리 초기화 함수 사용 불가

순수가상함수

` void func() = 0` 형태로 생김

순수가상함수가 부모에게 있을시 자식클래스에서는 무조건 정의해주어야한다. 순수가상함수가 하나라도 있는 클래스는 추상클래스로 객체화 불가

**c++ vs java**

- c++ 다중 상속지원, java는 x

- friend(은닉성 파괴)키워드 지원 여부

- java는 interface 지원 => 다중 상속 흉내

- 메모리 처리

  - c++은 stack, heap에 모두 할당 가능
  - java는 only heap
  - 메모리 해제 자동 여부(Garbage collector vs destructor)

- 문법 및 기능

  - c++은 연산자 오버로딩 지원

  - java는 익명클래스 지원

  - 자바는 동적바인딩, c++ 정적바인딩

    but c++은 virtual 키워드 통해 동적바인딩도 지원

# 자구

## 배열

같은 타입을 갖는 요소들의 모임

## 링크드 리스트

노드들이 선형적으로 순서화된 형태의 집합체

각 노드들은 데이터와 next를 저장

head, tail로 처음과 끝을 가리킴

## 스택

자료를 차곡차곡 쌓아올린 형태의 자료구조

LIFO 구조 (top으로 정한 곳에서만 접근가능)

**예시**

- text 편집기 undo(ctrl + z)
- 함수 호출시 메모리 상태변화
- 예전 뒤로가기

## 큐

자료가 뒤에서 들어오고 앞에서 빠져나가는 형태의 자료구조

FIFO(front, rear)

작업 스케쥴링

## 트리

부모 자식관계로 이루어진 노드의 집합

### 순회

- 전위 순회 : 자기 자신 방문 후, 자식 노드

  ```
  preorder(a)
  	visit(a)
  	for each child of a:
  		preorder(child)
  ```

  

- 후위 순회: 자식 노드 방문후, 자신 방문

  ```
  postorder(a)
  	for each child of a:
  		postorder(child)
  	visit(a)
  ```

  

## Map, Dictionary

(key, value)쌍으로 저장되는 자료구조

- hash table 로 구현

  o(n) worst case

  o(1) best case

- 레드블랙트리

## Heap

힙(heap)은 완전 이진 트리의 일종으로 부모 노드와 자식 노드간에 항상 대소관계가 성립하는 자료구조. 최대 최소 찾기 편한 자료구조

max-heap: 부모가 더 큼

min-heap: 부모가 더 작음

- 삽입: 맨 아래 오른쪽에 삽입 후 up-heap
- 삭제: down-heap

### 구현

- 완전 이진 트리는 `배열로 구현`합니다.
- 구현을 쉽게 하기 위해 배열을 사용할 때 인덱스는 `1`부터 사용합니다.
- 특정 노드의 배열 인덱스가 `current`라고 한다면 `부모 노드`는 `current / 2`를 통해 찾아갈 수 있고 `자식 노드`는 `current * 2`(좌측 자식 노드) 또는 `current * 2 + 1`(우측 자식 노드)을 통해서 찾아갈 수 있습니다.
- 현재 노드 인덱스 : `current`
- 부모 노드 인덱스 : `current / 2`
- 자식 노드들 인덱스 (순서 대로 좌우) : `current * 2`, `current * 2 + 1`

## Priority Queue

들어간 순서에 상관없이 우선 순위에 따라 결과가 달라지는 자료구조

- 배열로 구현 : 삽입, 삭제 둘중 하나가 o(n) 정렬됬는지 안됐는지에 따라 달라짐
- 링크드 리스트: 삽입 o(1), 삭제 o(n)
- heap 구현: 삽입,삭제가 lg n

## BST

이진탐색트리란 이진탐색(binary search)과 연결리스트(linked list)를 결합한 자료구조의 일종입니다. 이진탐색의 효율적인 탐색 능력을 유지하면서도, 빈번한 자료 입력과 삭제를 가능하게끔 고안.

