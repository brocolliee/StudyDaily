# Class gnu.getopt.Getopt

- java.lang.Object  
   |  
   +----gnu.getopt.Getopt  

- Java port of getopt
- command line argument를 파싱하기 위한 클래스
- C getopt()함수 기반

### How to Use Getopt ( 기본 방법 ) 
1. Getopt object 만들기 ( main method argv array 넘겨주기 ) 
2. getopt() method를 loop안에서 부르기
	- getopt()는 command line으로부터 option character를 전달해준다.
	- 더 이상 전달해줄 option이 없으면 -1 return
### Option
- 전통적인 Unix 방법으로 command line option이 전달된다. ‘-‘ character를 사용
	- “-abc”는 “-a -b -c”와 동일하다. 
- 만약 옵션이 argument가 필요하다면, option character뒤에 즉시 따라오거나 다음 argv 요소로 표현되어야 한다.
- “-cfoo”는 option ‘c’가 argument를 필요한다면 “-c foo”와 동일
- “-cfoo”는 option ‘c’가 argument를 필요하지 않다면 foo는 첫번째 non-option argv 요소
- 사용자는 getopt()를 멈출 수 있다. “--”를 사용 ( 스페셜 argument )
	- “-a -- -d”는 ‘a’의 옵션 return, --로 getopt를 통해 스캐닝 멈춤 , -d는 첫번째 non-option argv 요소

### Option Argument

- option이 argument가 있다면, argument의 값이 optarg 인스턴스 변수에 저장된다. 
- optarg 변수는 getOptarg() 함수를 사용하여 접근한다.
- argument가 있어야 하는데 없다면 error메시지를 프린트하고 getopt()는 ‘?’을 반환한다.

### Invalid Option
- invalid한 option이 나온다면 error메시지를 프린트 하고 getopt()는 ‘?’를 반환 한다. 
- invalid한 option 값은 getOptopt() method를 사용하여 볼 수 있는 인스턴스 변수 optopt에 저장 된다. 
- setOpterr method를 사용하여 opterr 인스턴스 변수의 값을 설정 할 수 있다.
- getopt()가 불리는 중간에 인스턴스 변수 optind가 어디를 파싱하고 있는지를 기록하기 위해(추적하기 위해 사용), 모든 옵션이 반환 되었을 때 optind는 첫번째 non-option argv 요소를 인덱스를 나타낸다.getOptind() method로 optind 변수에 접근 가능하다.

[Class gnu.getopt.Getopt 자세히 알아보기](https://www.aaronrenn.com/arenn/hacking/getopt/gnu.getopt.Getopt.html)  

** 음성 처리 분석 과제 중 정리 - OscillatorFile (jsresources) **
