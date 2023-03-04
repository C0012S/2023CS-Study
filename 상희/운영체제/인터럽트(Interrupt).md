# 💡 인터럽트(Interrupt)

# ✅ 인터럽트란?
CPU가 프로그램을 실행하고 있을 때, 입출력 하드웨어 등의 장치나 예외 상황이 발생하여 처리가 필요할 경우에 마이크로프로세서에게 알려 처리할 수 있도록 하는 것을 말한다.  
우선적으로 처리해야 할 일이 발생하였을 때 그것을 처리하고 원래 동작으로 돌아온다.  
인터럽트는 크게 하드웨어 인터럽트와 소프트웨어 인터럽트로 나뉜다.

<br/>

- 컴퓨터가 작업을 수행하던 도중 예기치 못한 특수한 상황이 발생하여 작업을 중단하고, 특수한 상황을 먼저 처리한 후, 원래의 작업으로 되돌아가 나머지 작업을 계속 수행하게 되는 일련의 과정이다.
- 인터럽트 당한 시점의 레지스터와 PC(Program Counter : 다음 번에 실행할 명령어 주소)를 PCB(Process Control Block)에 저장해두고 CPU의 제어를 인터럽트 서비스 루틴(Interrupt Service Routine)에 넘긴다.
- 명령어의 실행 단계를 마칠 때마다 CPU는 반복적으로 인터럽트 요청이 있는지 계속해서 확인한다.

<br/>

## 인터럽트 분류
어떤 사람은 외부 인터럽트, 내부 인터럽트로 나누고, 다른 사람은 외부 인터럽트, 내부 인터럽트, 소프트웨어 인터럽트로 나누고, 인터럽트랑 예외랑 혼용하여 말하는 사람들도 있다.  
인터럽트가 어디서 발생하느냐로 구분하면, 비동기적 인터럽트(= 하드웨어 인터럽트), 동기적 인터럽트(= 소프트웨어 인터럽트)로 구분할 수 있다.

<br/>

### 하드웨어 인터럽트
> Asynchronous Interrupt(비동기적 인터럽트) = Interrupt = Hardware Interrupt
> 

<br/>

일반적으로 인터럽트를 이르는 말이다.  
하드웨어가 발생시키는 인터럽트로, CPU가 아닌 다른 하드웨어 장치가 CPU에 어떤 사실을 알려 주거나 CPU 서비스를 요청해야 할 경우 발생시킨다.  
Maskable interrupt, Non-maskable interrupt가 있다. (Interrunpt Mask가 가능)  
- Maskable Interrupt
    - Interrupt Mask가 가능
        - Interrupt Mask : 인터럽트가 발생하였을 때 요구를 받아들일지 말지 지정하는 것
    - 인텔 CPU에서 **INTR pin**으로 신호가 들어온다.
    - CLI/STI instruction 에 의해서 무시될 수 있는 interrupt 이다.
    - 입출력 장치가 제기하는 인터럽트 요청과 거의 대부분의 인터럽트가 여기에 해당된다.
- Non Maskable Interrupt(NMI)
    - Interrupt Mask가 불가능
    - 거부, 무시할 수 없음 = 매우 중요한 인터럽트
    - 정전, 하드웨어 고장 등 어쩔 수 없는 오류
    - 인텔 CPU에서 **NMI pin**으로 신호가 들어옴

<br/>

### 소프트웨어 인터럽트
> Synchronous Interrupt(동기적 인터럽트) = Exception = Software Interrupt
> 

<br/>

소프트웨어가 발생시키는 인터럽트이다. 소프트웨어(사용자 프로그램)가 스스로 인터럽트 라인을 세팅한다.
종류 : 예외 상황, System Call

<br/>

인터럽트를 발생시키기 위해 하드웨어/소프트웨어는 CPU내에 있는 `인터럽트 라인`을 세팅하여 인터럽트를 발생시킨다.
CPU는 매번 명령을 수행하기 전에 인터럽트 라인이 세팅되어 있는지를 검사한다.

<br/>

트랩(Trap)이라고도 하며 프로그램 내부에서 일어나는 인터럽트이다. 예외와 시스템 콜이 있다.

<br/>

> **Trap**  
> 
> 트랩(trap)은 실행 중인 프로그램 내에 테스트를 위해 특별한 조건을 걸어 놓은 것을 말한다.  
> Interrupt 이든, System call 이든, Exception 이든 발생이 되면 Trap에 의해 catch가 되고,  
> Trap handler가 각 상황에 맞게 처리하도록 알맞게 매핑해 주어서 각 서비스 루틴 또는 핸들러에서 처리를 시킨다.  
> 
> 트랩은 발생하는 시점이 프로그램의 일정한 지점이다.  
> 하드웨어에 의해 자동적으로 미리 알려진 위치에 조건적으로 점프하는 것.  
> 
> Interrupt → Interrupt Service Routines(ISR) 을 실행하도록 처리  
> System Call → System Services 을 실행하도록 처리  
> Exception → Exception Handler 을 실행하도록 처리
> 

<br/>

## 인터럽트 종류
### 하드웨어 인터럽트(= 외부 인터럽트(External Interrupt)) 종류
- 입출력 인터럽트 (I/O interrupt) : 입출력 작업의 종료나 입출력 오류에 의해 CPU의 기능이 요청됨
- 정전, 전원 이상 인터럽트(Power fail interrupt) : 전원 공급의 이상
- 기계 착오 인터럽트(Machine check interrupt) : CPU의 기능적인 오류
- 외부 신호 인터럽트(External interrupt) : I/O 장치가 아닌 오퍼레이터나 타이머에 의해 의도적으로 프로그램이 중단된 경우

<br/>

### 소프트웨어 인터럽트(= 내부 인터럽트(Internal Interrupt)) 종류
- 프로그램 검사 인터럽트(Program Check Interrupt)
    - 0으로 나누는 경우
    - OverFlow/UnderFlow
    - 페이지 부재
    - 부당한 기억 장소의 참조
    
    > 예외 상황에 따라 인터럽트를 크게 외부 인터럽트, 내부 인터럽트, 소프트웨어 인터럽트로 나눌 수 있다. 이럴 경우, 프로그램 검사 인터럽트는 내부 인터럽트에 속한다. 내부 인터럽트는 Exception Interrupt 혹은 Trap이라고 부른다.  
    > 
    > Exception : 예외 상황에 대한 의미로, 소프트웨어 내부에서 예외 상황을 처리하는 것을 두고 소프트웨어 인터럽트를 Exception으로 보는 경우도 있다.  
    > Trap : 특별한 조건을 걸어 두고 조건에 부합하는 경우, 상황에 맞는 Service Routine이나 Handler가 실행되도록 하는 것을 의미한다. 따라서 이 경우에는 ISR(Interrupt Service Routines) 혹은 인터럽트 핸들러(Interrupt Handler)가 되겠다.  
    > 
    > Exception과 Trap은 프로그래밍 전반적으로도 사용되는 용어이니 단어를 어떻게 해석하느냐의 차이다. 너무 단어에 매몰되지 않고 개념을 잘 익히는 것이 중요하다.
    > 
- SVC(SuperVisor Call : 감시 프로그램 호출) 인터럽트
    - 사용자가 프로그램을 실행시키거나 Supervisior을 호출하는 동작을 수행하는 경우
    - 프로그래머에 의해 코드로 짜인 감시 프로그램을 호출하는 방식
    - 운영체제가 제공하는 서비스에 대한 프로그래밍 인터페이스가 System Call이고, System Call을 실행시키기 위한 CPU 명령어가 SVC이다.

<br/>

## 인터럽트 우선 순위
여러 장치에서 인터럽트가 동시에 발생하거나 인터럽트 서비스 루틴 수행 중 인터럽트가 발생했을 경우 우선 순위를 따져서 처리한다.  
전원 이상(Power Fail) > 기계 착오(Machine Check) > 외부 신호(External) > 입출력(I/O) > 명령어 잘못 > 프로그램 검사(Program Check) > SVC(SuperVisor Call)  
일반적으로 하드웨어 인터럽트가 소프트웨어 인터럽트보다 우선 순위가 높고, 내부 인터럽트보다 외부 인터럽트가 우선 순위가 높다.

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bXN8JO/btrcrNOCdrX/p9yBaxaFeCQKL7VleUPKWk/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bXN8JO/btrcrNOCdrX/p9yBaxaFeCQKL7VleUPKWk/img.png)

<br/>

## 인터럽트 우선 순위 판별 방법
### 소프트웨어적인 방법(Polling)
인터럽트 요청 플래그를 차례로 비교하여 우선 순위가 가장 높은 인터럽트 자원을 찾고, 이에 해당하는 인터럽트 서비스 루틴을 수행한다.  
속도가 따른 장치에 높은 등급을 부여한다.  
우선 순위 변경이 쉽다.  
많은 인터럽트가 있을 경우 하드웨어 적인 방법에 비해서 우선 순위 판단 속도가 느리다.  
회로가 간단하고 융통성이 있으며, 별도의 하드웨어가 필요 없다.

<br/>

### 하드웨어적인 방법(Vectored Interrupt)
인터럽트를 요청할 수 있는 장치와 CPU사이에 장치 번호를 식별할 수 있는 버스를 직렬/병렬로 연결한다.  
인터럽트 벡터는 인터럽트를 발생한 장치가 분기할 곳에 대한 정보이다.  
소프트웨어적인 방법에 비해 비경제적이다.  
회로가 복잡하고 융통성이 없으나, 별도의 소프트웨어가 필요 없이 하드웨어로 처리되므로 속도가 빠르다.  
하드웨어적인 방법은 아래 2 가지로 나뉜다.

<br/>

- Daisy Chain ★
    - 인터럽트가 발생하는 모든 장치를 하나의 직렬 회선으로 연결한다.
    - 우선 순위가 높은 장치를 상위에 두고 우선 순위 차례대로 배치한다.
- 병렬(Parallel) 우선 순위 부여 방식
    - 인터럽트가 발생하는 모든 장치를 하나의 직렬 회선으로 연결한다.
    - 각 장치별 우선 순위를 판별하기 위한 Mask register에 bit를 설정한다.
    - Mask register상 우선 순위가 높은 서비스 루틴 수행 중 우선 순위가 낮은 bit들을 비활성화 시킬 수 있다.
    - 반대로 우선 순위가 높은 인터럽트는 낮은 인터럽트 수행 중에도 우선 처리된다.

<br/>

인터럽트 서비스 루틴을 실행할 때 인터럽트 플래그(IF)를 1로 하면 인터럽트 발생을 방지할 수 있다.

<br/>
<br/>

# ✅ 인터럽트 처리 과정
![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bpgPHt/btq5NcPlGTH/BRIMZzBQQMUDm6ojSqgK00/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/bpgPHt/btq5NcPlGTH/BRIMZzBQQMUDm6ojSqgK00/img.png)

<br/>

![https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/9h8PF/btq5L4qJsN9/J1dii0rfe0jqtRen1IaNS0/img.png](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https://blog.kakaocdn.net/dn/9h8PF/btq5L4qJsN9/J1dii0rfe0jqtRen1IaNS0/img.png)

<br/>

인터럽트 원천인 하드웨어에서 또는 예외 상황이 발생하거나 소프트웨어 인터럽트가 걸리면 (명령어 실행 단계를 마칠 때마다 중앙 처리 장치는 반복적으로 인터럽트 요청이 있는지 확인한다.) :
- 현재 진행 중인 기계어 코드를 완료한다. (명령어 사이클인 인출과 실행 단계를 일단 마친다.)
- CPU의 특수레지스터 중, 하이로 인터럽트 마스크 비트를 보고 마스크 되면 인터럽트 무시 한다.
- 인터럽트 벡터를 읽고
- ISR(인터럽트 서비스 루틴, 인터럽트 핸들러) 주소 값을 얻는다.
- ISR로 점프 한다. 이때 PC(Program Counter, IP) 값은 자동 대피 저장된다.
- 현재 진행 중인 프로그램의 레지스터를 대피한다.
- 해당 코드를 실행한다.
- 해당 일을 다 처리하면, 대피시킨 레지스터를 복원한다.
- ISR의 끝에 IRET 명령어에 의해 인터럽트가 해제 된다.
- IRET 명령어가 실행되면, 대피시킨 PC 값을 복원하여 이전 실행 위치로 복원한다.

<br/>

보통 ISR로 들어가면서 CPU코어의 인터럽트 마스크 비트를 자동 설정하고 시작되기 때문에 다른 인터럽트 처리는 대기 상태로 되는 경우가 일반적이다. 따라서 ISR 내에서 다른 인터럽트를 처리하고 싶을 경우 이 마스크 비트를 해제 해야 한다.

<br/>
<br/>

# ✅ 인터럽트와 특권 명령
## 명령어의 종류
CPU가 수행하는 명령에는 `일반 명령`과 `특권 명령`이 있다.  
**일반 명령**은 메모리에서 자료를 읽어오고, CPU에서 계산을 하는 등의 명령이고 모든 프로그램이 수행할 수 있는 명령이다.  
**특권 명령**은 보안이 필요한 명령으로 입출력 장치, 타이머 등의 장치를 접근하는 명령이다. 특권 명령은 항상 운영체제만이 수행할 수 있다.

<br/>

## Kernel Mode vs User Mode
운영체제는 하드웨어적인 보안을 유지하기 위해 기본적으로 두가지 operation을 지원한다.  
**Kernel Mode**는 운영체제가 CPU의 제어권을 가지고 명령을 수행하는 모드로 `일반 명령`과 `특권 명령`  모두 수행할 수 있다.  
하지만 **User Mode**는 일반 사용자 프로그램이 CPU제어권을 가지고 명령을 수행하는 모드이기 때문에 `일반 명령`만을 수행할 수 있다.

<br/>
<br/>

# ✅ 인터럽트 관련 용어
## 인터럽트 벡터(Interrupt Vector)
여러 가지 인터럽트에 대해 해당 인터럽트 발생 시 처리해야 할 루틴(ISR)의 주소를 보관하고 있는 공간이다.  
대부분의 CPU들은 인터럽트 벡터 테이블을 가지고 있다.  
인텔 x86에서는 이를 IDT(Interrupt Descriptor Table)라고 한다.

<br/>

## 인터럽트 서비스 루틴(Interrupt Service Routine(ISR))
인터럽트 핸들러 Interrupt Handler라고도 한다.  
인터럽트가 접수되면 각각의 인터럽트에 대응하여 특정 기능을 처리하는 기계어 코드 루틴(커널이 실행)  
ex : 키보드 자판을 눌러 키보드 인터럽트가 발생하면 이에 해당하는 인터럽트 서비스 루틴이 실행됨

<br/>

## 인터럽트 핸들러(Interrupt Handler)
실제 인터럽트를 처리하기 위한 루틴으로 인터럽트 서비스 루틴이라고도 한다.  
운영체제의 코드 영역에는 인터럽트별로 처리해야 할 내용이 이미 프로그램되어 있다.  

<br/>

## PCB(Process Control Block)
커널의 데이터 영역에 존재하며 각각의 프로세스마다 고유의 PCB가 있다.  
인터럽트 발생 시 프로세스의 어느 부분이 수행 중이었는지를 저장한다. (수행 중이던 Memory 주소, 레지스터 값, 하드웨어 상태, ...)

<br/>
<br/>

# 🗣 면접 예상 질문
## Q1. 인터럽트가 무엇이며, 실행 흐름은 어떻게 되나요?
- CPU 하드웨어는 인터럽트 요청 라인(Interrupt Request Line)이라는 한 선을 갖는데, CPU는 각 명령어를 끝내고 다음 명령어를 수행하기 전에 항상 이 선을 검사한다.
- 인터럽트는 입출력 컨트롤러가 인터럽트 요청 라인에 신호를 보내면 CPU가 알아차리고 각종 레지스터 값과 상태 정보를 저장한 다음, 인터럽트 핸들러 함수로 분기하는 행위를 말한다.
- CPU가 인터럽트 되면, 하던 연산까지는 마치고 중단한 채 인터럽트 핸들러 루틴을 실행한다. 인터럽트 핸들러의 실행이 완료되면, CPU는 인터럽트 되었던 연산을 재개한다. 프로그램 카운터는 다음 명령어의 주소가 들어가 있다.

<br/>

## Q2. 컨트롤러가 입력을 얻는 방법에 대해 설명해 주세요.
컨트롤러가 입력을 받는 방법은 두 가지가 있다.  
첫 번째 방법으로는 폴링 방식이 있다. 폴링 방식은 사용자가 명령어를 입력하여 입력 핀의 값을 계속 읽어 변화를 알아내는 방식이다.  
두 번째 방법으로는 인터럽트 방식이 있다. 인터럽트는 MCU 자체가 하드웨어적으로 그 변화를 체크하여 변화 시에만 일정한 동작을 하는 방식이다.

<br/>

## Q3. 폴링 방식에 비해 인터럽트 방식이 갖는 장점을 말씀해 주세요.
인터럽트 방식으로 입력을 받을 경우, 폴링 방식에 비해 신속하게 대응할수 있으며 컨트롤러는 주기적으로 핀의 값을 읽지 않아도 되기 때문에 원래 일에 집중할 수 있다.

<br/>
<br/>

# 🗂 참고
- [[OS기초] 인터럽트 제대로 이해하기 (velog.io)](https://velog.io/@adam2/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8)
- [[OS] Interrupt 인터럽트란? :: DOHAN's iOS (tistory.com)](https://doh-an.tistory.com/31)
- [[컴퓨터구조] 인터럽트(Interrupt)란? (tistory.com)](https://whatisthenext.tistory.com/147)
- [인터럽트 종류와 처리과정과 우선순위. 인터럽트(Inerrupts) | by 수연이 | Medium](https://medium.com/@lazypanda43/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8-%EC%A2%85%EB%A5%98%EC%99%80-%EC%B2%98%EB%A6%AC%EA%B3%BC%EC%A0%95%EA%B3%BC-%EC%9A%B0%EC%84%A0%EC%88%9C%EC%9C%84-c95c26909472)
- [운영체제 · 인터럽트, 트랩 — PROJECT REBAS](https://rebas.kr/862)
- [3. 인터럽트 (Interrupt) :: JustZino (tistory.com)](https://justzino.tistory.com/4)
- [인터럽트(interrupt), 예외(exception), 트랩(trap)의 비교 - Easy is Perfect (melonicedlatte.com)](https://melonicedlatte.com/computerarchitecture/2019/02/12/213856.html)
- [인터럽트(Interrupt)의 개념과 종류 (tistory.com)](https://raisonde.tistory.com/entry/%EC%9D%B8%ED%84%B0%EB%9F%BD%ED%8A%B8Interrupt%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%A2%85%EB%A5%98)
- [인터럽트(Interrupt)의 종류와 처리과정 (tistory.com)](https://oizys.tistory.com/4)
- [[면접 예상 질문] 운영체제(3/3) - 무성이의 공부 블로그 (ddb8036631.github.io)](https://ddb8036631.github.io/question/%EC%9A%B4%EC%98%81%EC%B2%B4%EC%A0%9C-3/)
- [인터럽트 (tistory.com)](https://gona.tistory.com/36)
