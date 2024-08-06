# 운영체제


## 운영 체제란 무엇인가?
- 하드웨어를 관리하고, 컴퓨터 시스템의 자원들을 효율적으로 관리하며, 응용 프로그램과 하드웨어 간의 인터페이스로써 다른 응용 프로그램이 유용한 작업을 할 수 있도록 환경을 제공해준다.

## [운영체제의 역할]
### 1. 프로세스 관리
- 프로세스, 스레드
- 스케쥴링
- 동기화
- IPC 통신
### 2. 저장장치 관리
- 메모리 관리
- 가상 메모리
- 파일 시스템
### 3. 네트워킹
- TCP/IP
- 기타 프로토콜
### 4. 사용자 관리
- 계정 관리
- 접근권한 관리
### 5. 디바이스 드라이버
- 순차접근 장치
- 임의접근 장치
- 네트워크 장치
## [각 역할에 대한 자세한 설명]
### 1. 프로세스 관리
운영체제에서 작동하는 응용 프로그램을 관리하는 기능이다.
어떤 의미에서는 프로세서(CPU)를 관리하는 것이라고 볼 수도 있다. 현재 CPU를 점유해야 할 프로세스를 결정하고, 실제로 CPU를 프로세스에 할당하며, 이 프로세스 간 공유 자원 접근과 통신 등을 관리하게 된다.

### 2. 저장장치 관리
1차 저장장치에 해당하는 메인 메모리와 2차 저장장치에 해당하는 하드디스크, NAND 등을 관리하는 기능이다.

- 1차 저장장치(Main Memory)
  - 프로세스에 할당하는 메모리 영역의 할당과 해제
  - 각 메모리 영역 간의 침범 방지
  - 메인 메모리의 효율적 활용을 위한 가상 메모리 기능
- 2차 저장장치(HDD, NAND Flash Memory 등)
  - 파일 형식의 데이터 저장
  - 이런 파일 데이터 관리를 위한 파일 시스템을 OS에서 관리
### 3. 네트워킹
네트워킹은 컴퓨터 활용의 핵심과도 같아졌다.
TCP/IP 기반의 인터넷에 연결하거나, 응용 프로그램이 네트워크를 사용하려면 운영체제에서 네트워크 프로토콜을 지원해야 한다. 현재 상용 OS들은 다양하고 많은 네트워크 프로토콜을 지원한다.
### 4. 사용자 관리
하나의 PC로도 여러 사람이 사용하는 경우가 많다. 그래서 운영체제는 한 컴퓨터를 여러 사람이 사용하는 환경도 지원해야 한다.
사용자 별로 프라이버시와 보안을 위해 개인 파일에 대해선 다른 사용자가 접근할 수 없도록 해야 한다. 이 밖에도 파일이나 시스템 자원에 접근 권한을 지정할 수 있도록 지원하는 것이 사용자 관리 기능이다.
### 5. 디바이스 드라이버
운영체제는 시스템의 자원, 하드웨어를 관리한다. 시스템에는 여러 하드웨어가 붙어있는데, 이들을 운영체제에서 인식하고 관리하게 만들어 응용 프로그램이 하드웨어를 사용할 수 있게 만들어야 한다.
따라서, 운영체제 안에 하드웨어를 추상화 해주는 계층이 필요하다. 이 계층이 바로 디바이스 드라이버라고 불린다. 하드웨어의 종류가 많은 만큼, 운영체제 내부의 디바이스 드라이버도 많이 존재한다.

## 프로세스 & 스레드
- 프로세스: 프로그램을 메모리 상에서 실행중인 작업
- 스레드: 프로세스 안에서 실행되는 여러 흐름 단위
- 기본적으로 프로세스마다 최소 1개의 스레드 소유(메인 스레드 포함)
`프로세스는 각각 별도의 주소공간 할당(독립적)`
- **Code**: 코드 자체를 구성하는 메모리 영역(프로그램 명령)
- **Data**: 전역변수, 정적변수, 배열 등
  - 초기화 된 데이터는 data 영역에 저장
  - 초기화 되지 않은 데이터는 bss 영역에 저장
- **Heap**: 동적 할당 시 사용
- **Stack**: 지역변수, 매개변수, 리턴 값(임시 메모리 영역)
스레드는 Stack만 따로 할당 받고 나머지 영역은 서로 공유
하나의 프로세스가 생성될 때, 기본적으로 하나의 스레드 같이 생성
프로세스는 자신만의 **고유 공간과 자원을 할당받아 사용**하는데 반해, **스레드는 다른 스레드와 공간, 자원을 공유하면서 사용**하는 차이가 존재함
**멀티프로세스**
하나의 프로그램을 여러개의 프로세스로 구성하여 각 프로세스가 병렬적으로 작업을 수행하는 것
**장점**: 안전성(메모리 침범 문제를 OS 차원에서 해결)
**단점**: 각각 독립된 메모리 영역을 갖고 있어, 작업량 많을 수록 오버헤드 발생. Context Switching으로 인한 성능 저하
**Context Switching이란?**
프로세스의 상태 정보를 저정하고 복원하는 일련의 과정
즉, 동작 중인 프로세스가 대기하면서 해당 프로세스의 상태를 보관하고, 대기하고 있던 다음 순번의 프로세스가 동작하면서 이전에 보관했던 프로세스 상태를 복구하는 과정을 말함
-> 프로세스는 각 독립된 메모리 영역을 할당받아 사용되므로, 캐시 메모리 초기화와 같은 무거운 작업이 진행되었을 때 오버헤드가 발생할 문제가 존재함
**멀티 스레드**
하나의 응용 프로그램에서 여러 스레드를 구성해 각 스레드가 하나의 작업을 처리하는 것
스레드들이 공유 메모리를 통해 다수의 작업을 동시에 처리하도록 해줌

**장점**: 독립적인 프로세스에 비해 공유 메모리만큼의 시간, 자원 손실이 감소 전역 변수와 정적 변수에 대한 자료 공유 가능
**단점**: 인전성 문제. 하나의 스레드가 데이터 공간 망가뜨리면, 모든 스레드가 작동 불능 상태(공유 메모리를 갖기 때문)
- 멀티스레드의 안전성에 대한 단점은 Criticial Section 기법을 통해 대비함
하나의 스레드가 공유 데이터 값을 변경하는 시점에 다른 스레드가 그 값을 읽으려 할 때 발생하는 문제를 해결하기 위한 동기화 과정
상호 배제, 진행, 한정된 대기를 충족해야함