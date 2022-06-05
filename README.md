### 20194585 양준석의 리눅스 명령어와 vim에디터 매크로 사용법의 정리 
---
|리눅스명령어|top|ps|jobs|kill|
|---|---|---|---|---|


  와 vim에디터 매크로의 사용법에 대해서 정리를할건데요 지금부터 차근차근 시작하겠습니다.
  
---

## 리눅스 명령어들

#### 1) top명령어

일단 터미널에 들어가서 `top`을 입력하면
!<img src="https://user-images.githubusercontent.com/51511042/172042669-af9c762e-e82f-4224-be54-f8ead3dfd992.PNG" width="80%" height="80%"/>

와 같은 화면을 확인할수있는데

시스템의 상태를 전반적으로 **가장 빠르게** 파악 가능(CPU, Memory, Process등등)이 가능하다.

**옵션 없이** 입력하면 interval 간격(기본 3초)으로 화면을 갱신하며 정보를 보여준다.

> top 실행 전 옵션으로는 순간의 정보를 확인할수 있는 `-b`  (batch 모드) 와 `-n` (top 실행 주기 설정) 이 있다


top 실행 후 명령어로는
* shift + p : CPU 사용률 내림차순
* shit + m : 메모리 사용률 내림차순
* shift + t : 프로세스가 돌아가고 있는 시간 순
* k : kill. k 입력 후 PID 번호 작성. signal은 9
* f : sort field 선택 화면 -> q 누르면 RES순으로 정렬
* a : 메모리 사용량에 따라 정렬
* b : Batch 모드로 작동
* 1 : CPU Core별로 사용량 보여줌

이 있다.

---

#### 2) ps명령어

`ps`는 Process Status의 줄임말인 명령어이고 ps명령어는 **현재 실행중인 프로세스 목록**을 보여준다. 

주로 파이프라인, `grep`명령어와 함께 사용하여 특정 프로세스를 확인하는데 많이 사용된다.

> 주요 옵션들과 설명을 보자면 다음과같다.

|옵션|설명|
|---|---|
|-e|모든 프로세스를 출력해 준다.|
|-f|풀 포맷으로 보여준다.(UID, PID 등)|
|-l|긴 포맷으로 보여준다.|
|-p|특정 PID의 프로세스를 보여준다.|
|-u|특정 사용자의 프로세스를 보여준다.|

다음사진은 각각의 사용화면이다

![2](https://user-images.githubusercontent.com/51511042/172044013-c1d7ff52-6a5a-43d0-b748-cb31cbf93d96.PNG)

---

#### 3 jobs 명령어

`jobs`명령어는 **작업의 상태**를 표시하는 명령어이다.
```
geesehoward@DESKTOP-1IQCS3C:~$ jobs
[1]   Stopped                 top
[2]-  Stopped                 top
[3]+  Stopped                 top
```
실험을 하기위해 top을 실행하고 ctrl+z로 이용해 빠져나온후 jobs를 실행시킨 모습이다.

사용법은 다음과같다.
`jobs [옵션] [job ID]`

> 그리고 그에따른 옵션들


|옵션|설명|
|---|---|
|-l| 프로세스 그룹 ID를 state 필드 앞에 출력|
 |-n|프로세스 그룹 중에 대표 프로세스 ID를 출력|
 |-p|각 프로세스 ID에 대해 한 행씩 출력|
|command|지정한 명령어를 실행|



jobs로 출력되는 백그라운드 작업들의 상태값은 다음과 같다.

 * Running -작업이 일시 중단되지 않았고 종료하지 않고 계속 진행 중임

 * Done -작업이 완료되어 0을 반환하고 종료 했음을 의미

 * Done(code) -작업이 정삭적으로 완료되었으며, 0이 아닌 코드를 반환 했음을 의미

 * Stopped -작업이 일시 중단
 
 * Stopped(SIGTSTP) -SIGTSTP 신호가 작업을 일시 중단

 * Stopped(SIGSTOP) -SIGSTOP 신호가 작업을 일시 중단

 * Stopped(SIGTTIN) -SIGTTIN 신호가 작업을 일시 중단

 * Stopped(SIGTTOU) -SIGTTOU 신호가 작업을 일시 중단 

---

#### 4 kill 명령어


kill 명령어는 대개 프로세스를 죽일 때 사용한다. 하지만 내부적으로는 프로세스에 시그널을 보내 원하는 작업을 하게 하는 명령어이다. 

이 툴을 사용하려면 다음 구문을 사용한다.

`$ kill [options] <pid>`

-l 옵션을 이용해서 signal의 종류들을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/51511042/172045301-89e1730d-e713-4eaa-998b-9e7c0e50bbe7.png)

이를 이용해 종료되지 않은 프로세스를 종료시킬수있다.


---

####  vim 에디터에서 매크로 활용방법

먼저 메크로를 실행시키는방법은 명령모드에서 `q[Name]`이런식으로 사용한다 가령 qa, qq, qt, 등등 이런식으로 입력하면

![image](https://user-images.githubusercontent.com/51511042/172045512-86eda567-ca2d-46b9-840c-5240f0aa14ce.png)

위 이미지처럼 기록중 이라는 글자가 뜨게된다. 그리고 무언가를 하여 매크로가 어떻게 동작할지를 정할것이다.

![image](https://user-images.githubusercontent.com/51511042/172045606-33ea84ee-eef4-4016-b2c1-7aa0c0c1ff8f.png)

나는 간단하게 위에 줄을 생성하고 cut이라는 단어를 입력하는 매크로를 만들었다. 다만들고나서 다서 `q`를 입력하면된다 그러면 이제 `a`라는 매크로가 만들어진것이다.

이제 등록된 매크로를 실행시키기위해서는 `@[Name]` 을 입력하면된다.

![image](https://user-images.githubusercontent.com/51511042/172045674-3b8fc92f-8465-434d-a848-cfb4a4738214.png)

잘 작동되는 모습이다.
 
또한 매크로를 여러번 실행시키고싶다면 `[Number]@[Name]` 이런식으로 숫자만큼 반복시킬수있다.


이런식으로 같은 입력을 필요로하는 작업에서 매크로는 작업의 시간을 단축시켜주니 익혀주는 편이 좋을거라 상객한다!

