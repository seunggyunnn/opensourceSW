# 오픈소스SW개론 과제
20194573오승균

---

## 1) 리눅스 명령어 : top, ps, jobs, kill 조사하기

---

## ***top 명령어***

top 명령어는 현재 OS의 상태를 나타내주는 CLI 어플리케이션입니다. 메모리 사용량, CPU 사용량 등을 나타내주며 top를 실행하는 동안에는 주기적인 업데이트로 실시간에 근접한 내용을 보여줍니다. 리눅스에서 top 명령어를 실행하면 아래와 같이 노출됩니다. 위에는 전체의 요약이 있으며 아래에는 각 프로세스마다 구체적인 내용을 포함하고 있습니다.

![top명령어](https://user-images.githubusercontent.com/106795349/171995669-9f5a29a9-2fde-467e-8573-5b4b280387a1.png)

## ***요약 영역***

요약 영역은 상단에 위치하고 있습니다. 이 요약영역은 전체 프로세스가 OS에 대해서 리소스를 어느정도 차지하고 있는지를 알려줍니다. 요약 영역에 나타나는 대표적인 값은 시간, 유저, 로드 에버리지(Load Average), 테스크(Tasks), CPU, 메모리(memory)로 아래의 이미지를 보시면 각 영역에 대해 나태내느 값이 어디에 위치하는지 알 수 있습니다.

![top 명령어2](https://user-images.githubusercontent.com/106795349/171995698-704d9675-d9d1-4196-bd16-d793f5fb5e1e.png)

+ 시스템 현재 시간, OS가 살아있는 시간, 유저 세션수(System time, uptime and user sessions)

이미지의 가장 왼쪽 위를 보시면 시스템 현재 시간, OS가 살아있는 시간, 그리고 유저의 세션수가 표시되는 영역이 있습니다. 가장 먼저 보이는 숫자가 시스템의 현재 시간입니다. 이 시간은 GMT 기준으로 표시됩니다. 위 예제 기준으로 GMT 16:58:55 이라는 것입니다. 이것은 한국시간으로 보면 +9를 한 00시 58분 55초와 동일합니다. 다음으로 표시되는 것이 OS가 얼마나 살아있는지 나타냅니다. days와 시간으로 표시되며 위 예제로보면 7일과 1시 15분 동안 서버가 살아있었다는 것을 알 수 있습니다. 그리고 다음 나타나는것이 현재 접속중인 유저 세션 수입니다.

+ 로드 애버리지(Load Average)

2번째 영역은 로드 애버리지 영역입니다. 해당 영역은 CPU Load의 이동 평균를 표시합니다. 앞에서 부터 1분, 5분, 그리고 15분에 대한 평균값입니다. CPU Load란 CPU가 수행하는 작업의 양 입니다. 리눅스에서는 실행되거나 대기중인 프로세스의 평균입니다. 싱글 코어일 경우 1.0의 값이 CPU 100%를 사용하고 있다는 의미입니다. 멀티 코어라면 해당 코어수 만큼 * N을 한 값이 CPU 100%를 사용한다는 의미가 됩니다. 만약 100%를 넘어간다면 CPU에서 처리하지 못하고 대기하고 중인 프로세스가 있다고 보시면됩니다.

+ Tasks

2번째 줄에는 Tasks에 관한 내용이 출력됩니다. Tasks는 현재 프로세스들의 상태를 나태내주는 영역입니다. Total은 전체 프로세스, running은 running 상태인 프로세스, sleeping은 대기상태인 process, stopped는 종료된 프로세스, zombies는 좀비상태인 프로세스의 수를 나타냅니다

+ CPU 사용량

Tasks 아래 %Cpu(s)라는 영역이 있습니다. 이 영역은 CPU가 어떻게 사용되고 있는지 그 사용율을 보여주는 영역입니다. 모든 값의 총 합은 100% 이며 이를 퍼센테이지로 나누어서 보여줍니다. 각 요소는 아래와 같습니다.

+ 메모리 사용량

%Cpu(s) 영역 아래에 메모리와 관련된 영역이 있습니다. 첫번째 줄은 RAM의 메모리 영역으로 Mem이라 표시되어있는 부분입니다. 그리고 아랫줄은 디스크를 메모리 처럼 이용하는 Swap 메모리 영역입니다. 일반적으로 Mem의 사용량이 거의 가득 찼을때 Swap 메모리 영역을 사용합니다. 이 영역은 디스크이기 때문에 RAM 메모리보다 속도가 많이 느린 단점을 가집니다.

## ***디테일 영역***

지금부터는 top 명령어의 디테일 영역에 대해서 알아보도록 하겠습니다. 디테일 영역에는 각 프로세스에 대한 상세한 내용이 나옵니다. 위 예제에서는 아래의 이미지 부분이 디테일 부분입니다. 각 요소에 대해서 하나씩 보도록하겠습니다.

![top 3](https://user-images.githubusercontent.com/106795349/171995841-7f19f7c1-1bf2-4dcb-a0ed-427547685a49.png)

***ID***

+ PID는 프로세스 ID이며 프로세스를 구분하기 위한 겹치지않는 고유한 값입니다.

***USER***

+ 해당 프로세스를 실행한 USER 이름 또는 효과를 받는 USER의 이름입니다.

***PR & NI***

+ PR : 커널에 의해서 스케줄링되는 우선순위입니다.

+ NI : PR에 영향을 주는 nice라는 값입니다.

***VIRT, RES, SHR, %MEM***

+ 해당 필드들은 프로세스의 메모리와 관련있습니다.

+ VIRT : 프로세스가 소비하고 있는 총 메모리입니다. 프로그램이 실행중인 코드, heap, stack과 같은 메모리, IO buffer 메모리를 포함합니다.

+ RES : RAM에서 사용중인 메모리의 크기를 나타냅니다.

+ SHR : 다른 프로세스와의 공유메모리(Shared Memory)를 나타냅니다.

+ %MEM : RAM에서 RES가 차지하는 비율을 나타냅니다.

***S***

+ 프로세스의 현재 상태를 나타냅니다.

***TIME+***

+ 프로세스가 사용한 토탈 CPU 시간

***COMMAND***

+ 해당 프로세스를 실행한 커맨드를 나타냅니다.

## ***top 실행 후 명령어***

|명령어|설명|
|:---|---|
|shift + p|cpu 사용률이 높은 프로세스 순서대로 표시|
|shift + m|메모리 사용률이 높은 프로세스 순서대로 표시|
|shift + t|프로세스가 돌아가고 있는 시간 순서대로 표시|
|-k|프로세스 kill -k입력 후 종료할 PID 입력 signal을 입력하라고 하면 kill signal인 9를 입력|
|-a|메모리 사용량에 따라 정렬|
|-b|Batch 모드 작동|
|-c|명령행/프로그램 이름 토글|
|-d|지연 시간 간격은 다음과 같다. -d ss. tt (seconds.tenths)|
|-h|도움말|
|-H|스레드 토글|
|-i|유휴 프로세스 토글|
|-m|VIRT/USED 토글|
|-M|메모리 유닛 탐지|
|-n|반복 횟수 제한 : -n number|
|-p|PID를 다음과 같이 모니터 : -pN1 -pN2...or -pN1,N2[,...]|
|-s|보안 모드 작동|
|-S|누적 시간 모드 토글|
|-u|사용자별 모니터링 : -u somebody|
|-U|사용자별 모니터링 : -U somebodoy|
|-v|version|
|space bar|refresh|
|-u|입력한 유저의 프로세스만 표시|
|숫자 1|CPU Core별로 사용량을 보여준다|

## ***참조***

<https://ironmask84.tistory.com/355>

<https://sabarada.tistory.com/146>



---

## ***ps 명령어***

ps 명령어는 현재 실행중인 프로세스 목록과 상태를 보여줍니다. ps의 옵션은 전통적인 유닉스인 System V, BSD, GNU에 따라 결과가 다르게 나타나고 표기법에도 차이를 보입니다. 옵션 사용 시 System V 계열은 대시(dash, -)를 사용하고 BSD 계열은 대시(-)를 사용하지 않습니다. GNU에서의 옵션 표기는 두 개의 대시(--)를 사용합니다. 따라서 원하는 프로세스의 상태를 출력하려면 정확한 옵션 사용이 중요합니다.

## ***ps 사용법***

$ ps [option]

## ***ps 주요옵션***

리눅스 버전애 따라 옵션에 차이가 있을 수 있습니다. 이외에도 많은 옵션이 있지만 실제로는 grep명령어와 함께 사용하기 때문에 잘 사용하지 않습니다. (ex. ps -ef|grep ~)

|옵션|설명|
|:---|---|
|-e|모든 프로세스를 출력해 준다|
|-f|풀 포맷으로 보여준다(UID, PID 등)|
|-ㅣ|긴 포맷으로 보여준다.|
|p,-p|특정 PID의 프로세스를 보여준다|
|-u|특정 사용자의 프로세스를 보여준다|

## ***사용예시 및 사용화면***

+ ps

![ps 1](https://user-images.githubusercontent.com/106795349/171997901-6768f6bf-c317-4814-a603-56abed844fdd.jpeg)

pid,cmd 등 기본적인 내용만 출력된다. 옵션 없이는 잘 사용하지 않는다.

+ ps -f(풀 포맷으로 출력)

![ps 2](https://user-images.githubusercontent.com/106795349/171997935-8bf5d15d-3e89-45e9-8e77-4256eadf8ee6.jpeg)

uid(user ID), pid(process ID), ppid(parent ID), TTY(프로세스와 연결된 터미널)등을 표시해준다.

+ ps -l(긴 포맷으로 출력)

![ps 3](https://user-images.githubusercontent.com/106795349/171998012-74b1a182-935f-4c9c-afbb-765588ba3336.jpeg)

풀 포맷정보 외에 F(프로세스 플래그), S(프로세스 상태), PRI(우선순위) 등 더 많은 정보를 보여준다.

+ ps -p 1(프로세스 번호가 1인 프로세스 출력)

![Ps 4](https://user-images.githubusercontent.com/106795349/171998054-f6653d98-9e1d-4176-b27b-cca2e39baf9d.jpeg)

프로새스 번호가 1인 프로세스를 출력해준다. -e옵션과는 같이 사용할 수 없고 ps도 주로 grep과 함께 사용하므로 잘 사용되지 않는 옵션이다.

+ ps -u apache(계정이 apache인 프로세스들을)

![ps 5](https://user-images.githubusercontent.com/106795349/171998112-cab94a4e-fc3c-44f9-ba87-f82f42cf947b.jpeg)

apache 계정의 프로세스정보를 출력해주고 있다.

+ ps -e(모드 프로세스를 출력)

![ps 6](https://user-images.githubusercontent.com/106795349/171998138-0f2775a4-773c-4dd2-8f3d-5394f0a3a129.jpeg)

숨겨진 프로세스까지 모두 보여준다. 매우 많이 나오기 때문에 more명령어를 이용하여 보면 좋다.

+ ps -ef | more(모든 프로세스를 풀 포맷으로 보여준다, more명령어를 줘서 페이지단위로 출력)

![ps 7](https://user-images.githubusercontent.com/106795349/171998188-dfdf55bc-f620-4ad7-a891-9f6d0c71f230.jpeg)

프로세스가 매우 많이 때문에 파이프라인을 이용하여 more명령을 줘서 출력하였다. 보통 grep으로 찾을 수 없을때 수동으로 전체 프로세스를 보고자 하는경우 사용한다.

+ ps -ef | gerp apache(모든 프로세스의 출력값을 grep을 이용하여 apache가 포함된 라인들을 출력)

![ps 8](https://user-images.githubusercontent.com/106795349/171998227-a8932d41-e1cb-4816-960c-734ccfa73ecf.jpeg)

가장 많이 사용되는 형태이다. 파이프라인을 이용하여 특정 패턴이 있는 프로세스를 찾아 낼 수 있다. 주로 oracle 프로세스가 올라와있는지, apache 프로세스가 올라와 있는지 등 특정 프로세스가 정상적으로 올라와 있는지 확인하는데 사용된다.

## ***참조***

<https://jhnyang.tistory.com/268>

<https://arer.tistory.com/150>
