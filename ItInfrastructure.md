# 그림으로 공부하는 IT인프라 구조

## 차례
- [인프라 아키텍처를 살펴보자](#인프라-아키텍처를-살펴보자)  
- [서버를 열어 보자](#서버를-열어-보자)
- [3계층형 시스템을 살펴보자](#3계층형-시스템을-살펴보자)

## 인프라 아키텍처를 살펴보자
인프라는 '기반'이란 뜻으로, 바탕이나 토대를 의미한다.  
아키텍처는 '구조'를 의미하며, 공통화되어 있다.  
다양한 이용 방법과 사용자가 다르지만 인프라 아키텍처는 거의 같은 구조를 가지고 있다.  

### 집약형 아키텍처
집약형은 하나의 대형 컴퓨터로 모든 처리를 하는 것으로 '범용 장비', '호스트', '메인 프레임' 등으로 불렸다.  
컴퓨터를 구성하는 주요 부품은 모두 다중화되어 있어서 하나가 고장 나더라도 업무를 계속할 수 있다.  
복수의 서로 다른 업무 처리를 동시에 실행할 수 있도록 유한 리소스 관리를 한다. 하나의 처리가 다른 처리에 영향을 주지 않도록 되어 있다.  

**장점**  
- 한 대의 대형 컴퓨터만 있으면 되므로 구성이 간단하다.  
- 대형 컴퓨터의 리소스 관리나 이중화에 의해 안정성이 높고 고성능이다.

**단점**  
- 대형 컴퓨터의 도입 비용과 유지 비용이 비싸다.
- 확장성에 한계가 있다.

### 분할형 아키텍처
여러 대의 컴퓨터(서버)를 조합해서 하나의 시스템을 구축하는 구조다.  
여러 대의 소형 컴퓨터를 이용해 한 대가 고장 나도 안정성을 담보하고 있다.  
분할형 아키텍처는 표준 OS나 개발 언어를 이용하기 때문에 '오픈 시스템'이라고도 부른다.  

**장점**  
- 낮은 비용으로 시스템을 구축할 수 있다. 
- 서버 대수를 늘릴 수 있어서 확장성이 높다.

**단점**  
- 대수가 늘어나면 관리 구조가 복잡해진다.
- 한 대가 망가지면 영향 범위를 최소화하기 위한 구조를 검토해야 한다.  

### 서버
서버라는 용어는 컴퓨터 자체(하드웨어)를 가리키는 경우도 있고, 컴퓨터에서 동작하고 있는 소프트웨어를 가리키는 경우도 있다.  
컴퓨터 자체를 가리키는 경우는 '물리 서버'라고 부르고 웹 서버나 DB 서버와 같이 컴퓨터 내부에서 여러 소프트웨어 서버가 동작하고 있는 것을 '논리 서버'라고 부른다.  

### 수직 분할형 아키텍처
분할형에서는 서버 분할 방식, 즉 역할 분담을 고려해야 한다.  
수직형이라고 표현하는 것은 역할에 따라 '위' 또는 '아래' 계층으로 나뉘기 때문이다.  

#### *클라이언트-서버형 아키텍처*
애플리케이션, 미들웨어, 데이터베이스 등의 소프트웨어를 '물리 서버' 상에서 운영하고, 이들 소프트웨어에 '클라이언트' 또는 '단말'이라 불리는 소형 컴퓨터가 접속해서 이용하는 형태다.  
클라이언트-서버형의 특징은 클라이언트 측에 전용 소프트웨어를 설치해야 한다는 것이다.  

**장점**  
- 클라이언트 측에서 많은 처리를 실행할 수 있어서 소수의 서버로 다수의 클라이언트를 처리할 수 있다.  

**단점**  
- 클라이언트 측의 소프트웨어 정기 업데이트가 필요하다.
- 서버 확장성에 한계가 발생할 수 있다.  

#### *3계층형 아키텍처*
클라이언트-서버형을 발전시킨 것으로 프레젠테이션 계층, 애플리케이션 계층, 데이터 계층의 3층 구조로 분할되어 있어서 3계층형이라고 부른다.  
프레젠테이션 계층은 사용자 입력을 받고 웹 브라우저 화면을 표시한다.(웹 서버)  
애플리케이션 계층은 사용자 요청에 따라 업무 처리를 한다.(AP 서버)  
데이터 계층은 애플리케이션 계층의 요청에 따라 데이터 입출력을 한다.(DB 서버)  
3계층 시스템에서는 사용자가 웹 브라우저를 통해 시스템에 접속한다.  
모든 처리가 AP 서버나 DB 서버를 이용하지 않아도 된다.  

**장점**  
- 서버 부하 집중 개선
- 클라이언트 단말의 정기 업데이트가 불필요
- '처리 반환'에 의한 서버 부하 저감 

**단점**  
- 구조가 클라이언트-서버 구성보다 복잡하다.

### 수평 분할형 아키텍처
수평 분할형 아키텍처는 용도가 같은 서버를 늘려나가는 방식이다.  
서버 대수가 늘어나면 한 대가 시스템에 주는 영향력이 낮아져서 안정성이 향상된다.  
처리를 담당하는 서버 대수가 늘어나면 전체적인 성능 향상도 실현할 수 있다.  
수직 분할형과 수평 분할형은 배타적인 관계가 아니다.  
수평 분할을 'sharding'이나 'partitioning'이라 부르기도 한다.

#### *단순 수평 분할형 아키텍처*
이 구성에서는 시스템이 둘로 분할됨으로써 시스템 전체 처리 성능을 두 배로 향상시킬 수 있다.  
이 구조는 거래상으로 멀리 떨어진 시스템에 자주 이용되거나 각 거점이 완전히 독립된 운영을 하고 있는 경우에 적합하다.  

**장점**  
- 수평으로 서버를 늘리기 때문에 확장성이 향상된다.
- 분할한 시스템이 독립적으로 운영되므로 서로 영향을 주지 않는다.

**단점**  
- 데이터를 일원화해서 볼 수 없다.
- 애플리케이션 업데이트는 양쪽을 동시에 해 주어야 한다.
- 처리량이 균등하게 분할되어 있지 않으면 서버별 처리량에 치우침이 생긴다. 

#### *공유형 아키텍처*
공유형에서는 단순 분할형과 달리 일부 계층에서 상호 접속이 이루어진다.  
데이터가 각지에 흩어져 있는 것보다 한 곳에서 집중적으로 관리하는 것이 보안이나 관리상 유리한 경우가 있다.  

**장점**  
- 수평으로 서버를 늘리기 때문에 확장성이 향상된다.
- 분할한 시스템이 서로 다른 시스템의 데이터를 참조할 수 있다.  

**단점**  
- 분할한 시스템 간 독립성이 낮아진다.
- 공유한 계층의 확장성이 낮아진다.  

> **엣지 컴퓨팅(Edge Computing)**  
> 가상화를 사용해 데이터 센터를 통합하거나, 클라우드로 이전하면서 네트워크 대역과 비용이 크게 증가했다.  
> 이런 이유로 지리적으로 가까운 위치에 있는 서버로 처리를 분산하고 처리 결과만 중앙으로 보내는 아키텍처가 등장했다.  
> 엣지 컴퓨팅에서는 관리를 위한 수고를 줄이면서 서버를 분산하는 것이 중요한 과제다.  

### 지리 분할형 아키텍처
업무 연속성 및 시스템 가용성을 높이기 위한 방식이다.  

#### *스탠바이형 아키텍처*
스탠바이 구성, HA(High Availability) 구성, 액티브-스탠바이 구성 등으로 불리는 형태다.  
물리 서버를 최소 두 대를 준비하여 한 대가 고장 나면 가동 중인 소프트웨어를 다른 한 대로 옮겨서 운영하는 방식이다. 이때 소프트웨어 재시작을 자동으로 하는 구조를 페일오버(Failover)라고 한다.  
이 방식에서는 물리 서버 고장에 대처할 수 있지만, 보통 때는 페일오버 대상 서버(스탠바이)가 놀고 있는 상태가 되기 때문에 리소스 측면에서 낭비가 발생한다.  
스탠바이를 따로 두지 않고, 양쪽 서버를 동시에 교차 이용(한쪽 이 고장 나면 다른 한쪽이 양쪽을 처리)하는 경우도 많다.  
물리 서버가 아닌 가상화 서버를 이용하고 있는 경우는 서버상의 소프트웨어뿐만 아니라 가상 서버별로 다른 물리 서버에 페일오버하는 방식도 선택될 수 있다.  

#### *재해 대책형 아키텍처*
특정 데이터 센터(사이트)에 있는 상용 환경에 고장이 발생하면 다른 사이트에 있는 재해 대책 환경에서 업무 처리를 재개하는 것을 가리킨다.  
서버 장비를 최소 구성 및 동시 구성으로 별도 사이트에 배치하고, 소프트웨어도 상용 환경과 동일하게 설정한다.  
특히 데이터는 매일 갱신되기 때문에 어느 정도 실시간성을 유지해서 사이트 간 동기 처리를 해야 한다.  

## 서버를 열어 보자
### 물리 서버
서버는 랙(Rack)이라는 것에 장착된다.  
랙에는 서버 외에도 저장소나 네트워크 스위치 등도 탑재되어 있다.  
랙의 규격은 폭 19인치, 높이 한 칸(1U)에 약 4.5cm로 40~46개 칸으로 이루어져 있다.  
서버 설치 시에 중요한 정보는 서버 크기(U), 소비 전력(A), 중량(Kg)이다.  
서버 내부는 다수의 컴포넌트들로 구성되어 있고 그 컴포넌트들은 버스(연결하는 선)로 연결된다.  

### CPU
CPU는 Central Processing Unit의 약자로 서버 중심에 위치해서 연산 처리를 실시한다.  
뒷면에 있는 대량의 핀이 버스에 연결되어 있어서 메모리나 디스크와 데이터를 교환한다.  
CPU는 명령을 받아서 연산을 실행하고 결과를 반환한다. 명령과 데이터는 기억 장치나 입출력 장치를 통해 전달된다.  
CPU는 코어(core)라고 하며, 하나의 CPU에 여러 개의 코어가 존재하고 각자가 독립된 처리를 할 수 있다.  
OS에서 동작하는 프로세스와 사용자를 통한 입력으로 CPU에 명령을 내린다.  

### 메모리
CPU 옆에 위치하며, CPU에 전달하는 내용이나 데이터를 저장하거나 처리 결과를 받는다.  
메모리에 저장되는 정보는 영구성이 없지만 액세스가 매우 빠르게 이루어진다.  
CPU 자체도 메모리를 가지고 있다. 이것은 레지스터나 L1/L2 캐시라고 불리며 메모리보다 더 빠르고 용량은 메모리에 비해 매우 작다.  
메모리를 이용하려면 메모리 컨트롤러를 경유해서 CPU 밖으로 나가야 한다. 메모리 컨트롤러에는 채널들이 있는데 채널은 메모리와 CPU 간 데이터 경로를 말한다.  
고속 CPU는 처리 지연(Latency)조차 허락하지 않기 때문에 가장 자주 사용하는 명령/데이터를 코어 가까운 곳에 배치해야 한다.  
메모리 영역이 여러 단계로 나누어져 있는 이유는 액세스 속도 때문이다.  
일반적으로 캐시 메모리가 커질수록 액세스 속도가 느려진다. 하지만 가능한 CPU 가까운 곳에 많은 캐시를 두고 싶기 때문에 여러 단계로 배치해서 초고속으로 액세스하고 싶은 데이터는 L1 캐시에, 준고속으로 액세스하고 싶은 데이터는 L2 캐시에 두는 형태로 만든 것이다.  
메모리에는 미리 데이터를 CPU에 전달해서 처리 지연을 줄이는 메모리 인터리빙(Memory Interleaving)이라는 기능이 있다. 이 기능을 활용하기 위해서는 모든 채널의 동일 뱅크에 메모리를 배치해야 한다.  

### I/O 장치
#### *하드 디스크 드라이브(HDD)*
서버에서는 메모리에 비해 CPU에서 떨어진 곳에 HDD가 배치된다.  
주로 장기 저장 목적의 데이터 저장 장소로 사용한다.  
전기가 없어도 데이터가 사라지지 않는다.  
내부에는 자기 원반이 여러 개 들어 있으며, 이것이 고속으로 회전해서 읽기/쓰기 처리를 한다.  
SSD(Solid State Disk, 반도체 디스크)는 물리적인 회전 요소를 사용하지 않는 디스크이다.  
서버와 I/O 시에는 HDD가 직접 데이터 교환을 하는 것이 아니라 캐시를 통해서 한다.  
대형 저장소와 연결할 때는 파이버 채널(Fibre Channel, FC)이라는 케이블을 사용해서 SAN이라는 네트워크를 경유한다.  
쓰기 I/O에는 라이트 백과 라이트 스루가 있다.

#### *네트워크 인터페이스*
네트워크 인터페이스는 서버와 외부 장비를 연결하기 위한 것으로 외부 접속용 인터페이스다.  
서버 외부 장비로는 네트워크에 연결된 다른 서버나 저장소 장치가 있다.  

#### *I/O 제어*
칩셋은 처리 속도가 비교적 늦어도 용서되는 I/O 제어를 담당하고 있다.(ex: PCH)  
CPU 외에도 다양한 컨트롤러나 칩이 존재하는 이유는 CPU가 해야 할 연산에 더 집중하기 위한 것이라 할 수 있다.  
CPU와 칩셋의 관계는 역할 분담을 위한 것이다.  

### 버스
버스(Bus)는 서버 내부에 있는 컴포넌트들을 서로 연결시키는 회선을 가리킨다.  
버스에서 중요한 것은 어느 정도의 데이터 전송 능력을 가지고 있는가, 즉 대역이 어느 정도인가이다.  

#### *대역*
IT 인프라에서 대역은 데이터 전송 능력을 의미한다.  
대역은 '한번에 데이터를 보낼 수 있는 데이터 폭(전송폭)' × '1초에 전송할 수 있는 횟수(전송 횟수)'로 결정된다. 전송 횟수는 '1초 ÷ 1처리당 소요 시간(응답 시간)'으로 표현할 수 있다.  
대역은 스루풋(Throughput, 처리량)이라고도 부른다.  

#### *버스 대역*
CPU에 가까운 쪽이 1초당 전송량이 크다는 것을 알 수 있다.  
버스 흐름에서 중요한 것은 CPU와 장치 사이에 병목 현상이 없어야 한다는 것이다.  
시스템 설계 시에 특히 놓치기 쉬운 것이 외부 장치 연결 시의 버스 대역에 관한 것이다.  

> **SSD 규격**  
> SATA(Serial ATA) -> SAS(Serial Attached SCSI) -> NVMe(NVM Express) 순으로 속도가 빠르다.  

### 처리 흐름
CPU가 PCI 컨트롤러 역할을 하고 있어서 그림이 약간 복잡하지만, 아래 구조도 시간이 지남에 따라 바뀔 것이다.  
![cpu_to_storage](https://user-images.githubusercontent.com/40534414/224868346-f90b3239-789f-45dd-af32-c432644ba9ef.png)

## 3계층형 시스템을 살펴보자
주요 구성 요소는 웹 서버, AP 서버, DB 서버이다.  
각 서버의 CPU와 메모리 영역에는 논리 구성이 되어 있는데 이 부분은 OS 영역을 가리킨다.  
OS를 이해하는 데 있어서 필수 개념인 프로세스와 스레드, 커널이 있다.  

### 프로세스와 스레드
프로세스 및 스레드는 프로그램 실행 파일 자체가 아니라 OS상에서 실행돼서 어느 정도 독립성을 가지고 동작하는 것이다.  
프로세스나 스레드가 시작되는 것은 마치 사람이 숨을 쉬기 시작하면서 활동하는 것과 같은 의미다.  
프로세스 및 스레드가 활동하려면 메모리 공간이 필요하다. 이것은 커널에 의해 메모리상에 확보된다.  
프로세스의 내부에 하나 이상의 스레드가 메모리 공간을 점유해서 동작한다.  
프로세스는 전용 메모리 공간을 이용해서 동작한다.  
스레드는 다른 스레드와 메모리 공간을 공유하고 있는 운명 공동체다.  
프로세스 간의 공유하고 싶은 데이터는 공유 메모리상에 둔다.   

||프로세스|스레드|
|:---:|:---|:---|
|장점|개별 처리 독립성이 높다|생성 시 부하가 낮다|
|단점|생성 시 CPU 부하가 높다|메모리 공간을 공유하기 때문에 의도하지 않는 데이터 읽기/쓰기가 발생할 수 있다|  

### OS 커널
커널은 OS의 본질이며, 커널 자체가 OS의 '인프라'라고 생각하면 된다.  
커널은 다양한 역할을 갖지만, 가장 중요한 것은 '뒤에서 하는 일은 은폐하면서도 편리한 인터페이스를 제공하는 것'이다.  
OS 처리는 원칙적으로 커널을 통해 이루어지며 커널의 역할은 아래와 같다.  

#### *시스템 콜 인터페이스*
프로세스/스레드에서 커널로 연결되는 인터페이스다.  
애플리케이션이 OS를 통해서 어떤 처리를 하고 싶으면 시스템 콜이라고 하는 명령을 이용해서 커널에 명령을 내린다.  
데이터 I/O, 네트워크 I/O, 또는 새로운 프로세스 생성을 시스템 콜을 호출하면 기능을 이용할 수 있다.  

#### *프로세스 관리*
언제, 어떤 프로세스가 어느 정도의 CPU 코어를 이용할 수 있는지, 처리 우선순위를 어떻게 결정할 것인지 등을 관리하는 기능의 역할을 한다.  
이 기능이 없다면 OS가 성립되지 않기 때문에 OS에게 있어 가장 중요한 기능이라 할 수 있다.  

#### *메모리 관리*
메모리 관리에서는 물리 메모리 공간의 최대치를 고려한다.  
프로세스가 이용하는 독립 메모리 공간을 확보하거나 상호 간의 참조 영역을 지키기 위해 독립성을 관리하는 등의 메모리 관리 역할을 한다.  
이 기능이 없으면 각 프로세스는 자신 이외의 프로세스가 사용하고 있는 메모리 영역 범위를 파악해야 한다.  

#### *네트워크 스택*

#### *파일 시스템 관리*
파일 시스템은 OS 기능의 하나로서 물리 디스크에 제공된 데이터를 관리하는 기능이다.  
물리 디스크에 기록된 데이터는 2진수의 집합에 불과하며 구분 표시도 없기 때문에 파일 시스템을 이용하여 애플리케이션을 파일 단위로 데이터를 작성하거나 삭제할 수 있다.  
주요 관리 기능으로는 디렉터리 구조 제공, 액세스 관리, 고속화, 안정성 향상 등이 있다.  

#### *장치 드라이버*
디스크나 NIC 등의 물리 장치용 인터페이스를 제공한다.  
물리 장치는 제조사마다 독자 제품을 제공하기 때문에 커널은 장치 드라이버를 이용해서 그 아래에 있는 물리 장치를 은폐한다.  
각 장치 제조사는 OS에 대응하는 장치 드라이버를 제공해서 해당 OS의 표준 장치로서 커널을 경유해 이용할 수 있게 하는 것이다.  

> **커널 설계 및 구현 방식**  
> 모놀리식(Monolithic) 커널: OS의 주요 구성 요소를 모두 하나의 메모리 공간을 통해 제공한다.  
> 마이크로(Micro) 커널: 최소한의 기능만 커널이 제공하고 그 외 기능은 커널 밖에서 제공한다.  