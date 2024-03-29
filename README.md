# gradle-starter

## gradle
### 용어 정리
> 컴파일(compile): 소스 코드를 바이너리 파일로 변환하는 과정(예: .java -> .class 파일로 변경)  
> 
> 빌드(build): 프로젝트의 소스, 리소스 파일들을 컴퓨터에서 실행할 수 있는 독립적인 형태로 변환하는 과정과 그 결과.  
> 빌드 과정에서 소스 코드에 대한 컴파일이 진행됨으로 컴파일은 빌드 과정 중 하나이다.  
> 
> 빌드 툴(build tool): 빌드에서는 컴파일, 테스트, 배포 등 과정이 포함될 수 있고, 빌드 과정을 도와주는 도구를 빌드 툴이라 합니다.    
> 일반적으로 빌드 툴이 제공해주는 기능으로는 다음과 같은 기능들이 있습니다.  
> 전처리(preprocessing), 컴파일(Compile), 패키징(packaging), 테스팅(testing), 배포(distribution)  
> 빌드 툴로는 Ant, Maven, Gradle 등이 있습니다.   
> 
> 컴파일 타임(compile time):   
> 런타임(Runtime)과 컴파일타임(Compiletime)은 소프트웨어 프로그램개발의 서로 다른 두 계층의 차이를 설명하기 위한 용어이다. 
> 프로그램을 생성하기 위해 개발자는 첫째로 소스코드를 작성하고 컴파일이라는 과정을 통해 기계어코드로 변환 되어 실행 가능한 프로그램이 되며, 
> 이러한 편집 과정을 컴파일타임 이라고 부른다.   
>
> 런타임(run time):   
> 컴파일과정을 마친 프로그램은 사용자에 의해 실행되어 지며, 이러한 응용프로그램이 동작되어지는 때를 런타임(Runtime)이라고 부른다.  
> "런타임"과 "컴파일 타임"이라는 용어는 종종 서로다른 두 가지 타입의 에러를 나타내기 위해 사용되어지곤 하는데, 
> 컴파일 타임 에러는 프로그램이 성공적으로 컴파일링되는 것을 방해하는 신택스에러(Syntax error)나 파일참조 오류와 같은 문제를 말하며, 
> 이런 경우 컴파일러는 컴파일 타임 에러를 발생시키고 일반적으로 문제를 일으킨 소스코드 라인을 지시해준다.
> 만약, 어떤 소스코드가 이미 실행가능한 프로그램으로 컴파일 되었다 할지라도 이것은 여전히 프로그램의 실행중에 버그를 일으킬 수 있다. 
> 예를 들자면, 예상치 못한 오류 또는 충돌로 동작하지 않을 수 있는데 이렇게 프로그램이 실행중에 발생하는 형태의 오류를 런타임오류 라고 한다.  
> 
> 컴파일타임 오류의 유형
> * 신택스 오류
> * 타입체크 오류
> 
> 런타임 오류의 유형
> * 0나누기 오류
> * 널(Null)참조 오류
> * 메모리 부족 오류
>  
> 참조사이트  
> [런타임(Runtime)과 컴파일타임(Compiletime)의 차이점은 무엇인가?](https://spaghetti-code.tistory.com/35)

### 개요
> JVM 빌드 도구.

### 설치
> macOS: `brew install gradle`    
> 
> 버전 확인: `gradle -version`  

### 프로젝트 초기화
> 1.Gradle 프로젝트를 생성할 디렉터리로 이동.  
> 2.`mkdir <프로젝트 명>` 명령어로 프로젝트 디렉터리 생성 후 해당 디렉터리로 이동.  
> 3.`gradle init` 명령어 실행.  
> 3-1.java application 으로 미리 정해서 생성하려면 다음 명령어 실행: `gradle init --type java-application`

### 프로젝트 구조
> ```shell
> ├── .gradle
> ├── build.gradle
> ├── gradle
> │   └── wrapper
> │       ├── gradle-wrapper.jar
> │       └── gradle-wrapper.properties
> ├── gradlew
> ├── gradlew.bat
> └── settings.gradle
>```
> .gradle 디렉터리  
> Gradle 이 사용하는 디렉터리. 작업(Task) 로 생성된 파일이 저장됨. 사용자가 직접 편집하지 않음.
> 
> build.gradle  
> Gradle 프로젝트에서 기본 빌드 설정 파일: 의존성(Dependencies) 관리 및 플러그인 등의 설정을 한다.  
> 
> app/src 디렉터리  
> 프로젝트 소스 및 리소스 파일들이 위치한 디렉터리.  
> 
> gradlew, gradlew.bat  
> Gradle 프로그램 파일로 해당 프로젝트를 clone 한 PC 에 Gradle 이 설치되어 있지 않더라도 프로젝트를 Gradle 로 빌드시킬 수 있게 하기 위해서
> 프로젝트 내에 존재하는 Gradle 프로그램 파일로 보면됨.  
> PC 에 Gradle 이 설치되어 있는 경우 다음과 같이 테스크를 실행하면 된다: `gradle build`  
> PC 에 Gradle 이 설치되어 있지 않은 경우 다음과 같이 테스크를 실행한다: `./gradlew build`  
> 
> settings.gradle  
> 프로젝트에 대한 설정 정보를 작성한 파일.  
> MSA(Micro Service Architecture) 구조로 프로젝트를 구성할 경우 root 프로젝트 하위로 모듈을 추가할 경우 settings.gradle 파일에 모듈을 추가한다고 명시한다.

### 참조사이트
> [Gradle 기본사용법](https://velog.io/@franc/Gradle-%EA%B8%B0%EB%B3%B8%EC%82%AC%EC%9A%A9%EB%B2%95)

---

## 그레이들과 빌드
### 스크립트 종류
> 그레이들의 스크립트는 3가지 종류로 나누어 볼 수 있다. 가장 먼저 실행되는 `초기화 스크립트`, 해당 프로젝트의 빌드 관련 설정을 정의하는 `설정 스크립트`,
> 그레이들의 빌드 수행과 관련한 내용이 기술되는 `빌드 스크립트`가 있다.

### 초기화 스크립트
> 초기화 스크립트는 주로 `init.gradle` 로 파일 이름이 명명되고, 사용자 정보, 실행 환경, 초기 선언 값 설정 등 초기 설정 정보를 기술하고 정의하여 설정하는데
> 사용한다.

### 설정 스크립트
> 설정 스크립트는 `settings.gradle` 로 명명되며, 빌드의 대상이 되는 프로젝트를 정의하고 해당 프로젝트가 싱글 프로젝트인지, 멀티 프로젝트인지를 결정하게 되고
> 프로젝트의 인스턴스를 생성할 수 있다.

### 빌드 스크립트
> 빌드 스크립트는 그레이들의 핵심 스크립트이다. 빌드 수행과 관련된 의존 관계 정의, 태스크 정의 등의 내용이 기술되고 기본 파일 이름은 `build.gradle` 로,
> 이 파일만 있어도 빌드를 수행하기에 필요충분한 요소라고 할 수 있다. 또한 build.gradle 스크립트 파일은 settings.gradle 스크립트 파일이나 init.gradle
> 스크립트 파일을 참조하거나 상호작용하여 빌드 수행이 이루어지게 된다.

### 속성 파일
> 속성 파일은 `gradle.properties` 로 명명되며 해당 프로젝트에 gradle.properties 파일이 있다면 빌드 수행 시 자동으로 참조하여 해당 파일의 내용을 
> 확인하게 된다. 속성 파일인 gradle.properties 에는 빌드 스크립트에 기술하지 않은 환경의 변화에 따른 속성 정보 및 내용 등이 기술된다.

### 그루비(Groovy)
> 그루비는 스크립트 언어로 JVM 에서 동작하는 JVM 언어 중 하나이고 DSL 에 의한 확장성이 좋은 언어라고 할 수 있다.  
> 그루비의 가장 큰 특징 중 하나는 그루비 문법이 자바와 호환된다는 것이다. 즉, 자바 코드를 그대로 그루비 코드로 활용할 수 있다.  
> 또한, 자바 라이브러리를 호출할 수 있다. 하지만 그부리만의 문법적인 특징과 형식이 있으므로 이 부분을 알고 있어야한다.  
>
> **def 형 사용**  
> 자바와 같은 형을 지정해서 사용할 수도 있지만, 그부리에서 형 지정을 하지 않을 때에는 def 를 사용한다.  
> ```groovy
> // 자바와 같이 형 지정
> String id = 'gradle'
> 
> // 형 지정 생략
> def id = 'gradle'
> println id.toUpperCase()  // 속성 참조 가능
> ```
> 
> **문자열 사용**  
> 그루비는 문자열을 표기할 때 작은따옴표와 큰따옴표를 사용하며 각각은 서로 스 쓰임이 다르다.
> 작은따옴표는 문자열을 지정할 때 사용하며, 큰따옴표는 문자열에 $기호를 사용하여 동적으로 내용을 지정할 때 사용한다.  
> ```groovy
> def id = "ID : ${project.id}"
> String id = "ID: $id" // {} 생략 가능
> ```
> 또한 작은따옴표와 큰따옴표는 중첩되게 세 개를 이용하여 여려 개의 문자열을 사용할 수도 있다.
> ```groovy
> def id = """
>   hello 
>   world
> """
> def id = '''
>   hello
>   world
> '''
> ```
> 
> **괄호의 생략**  
> 그루비는 메서드를 호출 할 때 괄호를 생략할 수 있다. 단, 모든 경우에 생략할 수 있는 것은 아니다.
> ```groovy
> println('hello')
> println 'hello'
> ```
> 
> **클로저의 사용**  
> 클로저는 중괄호를 이용하여 정의하고 해당 클로저를 call() 속성이나 일반 메서드처럼 호출하여 실행할 수 있다.  
> ```groovy
> def id = { closer -> println "id, $closer" }
> // call() 이용한 사용
> id.call('gradle')
> // 일반 메서드 호출 방식 사용
> id('gradle')
> // 괄호를 생략하고 사용
> id 'gradle'
> ```
> 
> **명령문**  
> 명령문 뒤에 세미콜론은 생략할 수 있다. 
> 
> **리스트와 맵**  
> 리스트는 배열처럼 사용하고 배열처럼 접근할 수 있다.  
> ```groovy
> def id = ['gradle', 'Groovy']
> id[1] = 'script'
> assert id[1] == 'script'
> ```
> 
> 맵도 리스트처럼 대괄호를 이용하여 정의하고 접근할 수 있다.  
> ```groovy
> def id = ['a':'gradle', 'b':'Groovy']
> assert id['a'] == 'gradle'
> ```
> 
> **비교**  
> 자바의 equals 와 동일하게 그루비는 == 를 이용하여 문자열 등을 비교하게 된다. 그러나 객체가 같은지 비교하려면 is() 를 사용하여 비교해야 한다.  

### 그레이들의 스크립트 파일 구조
> 그레이들의 스크립트 파일은 두 가지 요소로 구성되는데, `처리문(Statement)` 영역과 `스크립트 블록(script block)` 영역이다.  
> 처리문은 일반적인 프로그래밍에서의 지역 변수, 속성 정의 및 설정, 메서드 등이고, 스크립트 블록은 특정한 그레이들의 프로젝트를 빌드하기 위한 부분으로
> 그레이들에서 사용되는 개념이다.    
> 그레이들의 주요 스크립트 불록은 다음과 같다.  
> * repositories: 저장소 설정
> * dependencies: 의존 관계 설정
> * buildscript: 빌드 스크립트 클래스 패스 설정
> * initscript: 초기화 스크립트 설정
> * configurations: 환경 구성 설정
> * allprojects: 서브 프로젝트 포함 전체 프로젝트 설정
> * subprojects: 서브 프로젝트 설정
> * artifacts: 빌드 결과에 대한 설정

### 변수
> **지역 변수**  
> 선언된 부분에서 영향력 있는 변수  
> 
> **시스템 속성**  
> 시스템 관련 정보를 저장하는 변수.  
> 명령어 인수로 사용하려면 -D 옵션이나 --system-prop 옵션을 사용하여 그 뒤에 속성명과 속성값을 설정하면 된다.  
> build.gradle
> ```groovy
> tasks.register('hello') {
>   println System.properties['message']
> }
> ```
> 
> shell
> ```shell
> gradle -Dmessage=hello hello
> ```
> 
> **확장 속성**  
> ext 라는 예약어를 사용하여 스크립트 파일에서 도메인 객체의 속성을 추가할 때 사용한다.  
> ```groovy
> // 확장 속성 지정
> ext {
>   extPro1 = 'pro1'
>   extPro2 = 'pro2'
> }
> 
> // 사용
> println '속성값 1 : ' + ext.extPro1
> println '속성값 2 : ' + ext.extPro2
> ```
> 
> **프로젝트 속성**  
> 속성 파일인 gradle.properties 에 '속성명=속성값' 형식으로 정의하게 되면 프로젝트 속성의 변수가 선언되어 속성을 추가할 수 있다.  
> gradle.properties
> ```properties
> msg=Hi, Gradle!
> ```
> build.gradle
> ```groovy
> tasks.register('hello') {
>   println msg
> }
> ```
> 다만 gradle.properties 와 build.gradle 파일이 동일한 경로에 있어야한다.

---

## Task
### 기본 Task
> 현재 프로젝트에서 지원하는 Task 종류 확인: `gradle tasks`
>
> 프로젝트 빌드  
> `gradle build` 태스크를 통해서 프로젝트 빌드를 실행한다.  
> build.gradle 에 `apply plugin: 'java'` 가 추가된 경우 .jar 파일로 패키징까지 해준다.  
> 컴파일된 파일들은 app/build 디렉터리 안에 생성되며, .jar 파일은 `build/libs` 에 패키징된다.
>
> 프로젝트 실행  
> 일단 Java 애플리케이션인 경우 `gradle run` 으로 실행하며, 스프링부트인 경우 `gradle bootRun` 을 통해서 앱을 구동한다.
>
> 프로젝트 패키징  
> `gradle jar` 명령어로 프로젝트를 .jar 파일로 패키징하며, build.gradle 파일에 `apply plugin: 'java'` 가 추가된 경우 `gradle build` 로
> 패키징까지 할 수 있다.
>
> 프로젝트 클린  
> `gradle clean` 을 통해서 app 밑에 build 디렉터리를 제거하여, 빌드 이전 상태로 되돌린다.

### 커스텀 Task
> build.gradle 에서 다음과 같은 구조로 정의한다.
> ```groovy
> tasks.register('<테스크 명>') {
>   // 내용
> }
> ```
> 예시: 'hello world' 를 화면에 표시하는 테스크 'hello'
> ```groovy
> tasks.register('hello') {
>     println 'Hello world'
> }
> ```
> 터미널에서 `gradle hello` 를 입력하면 Hello world 가 화면에 표시된다.

### doFirst 와 doLast 
> 태스크 내부에서 우선순위 블록을 만들고자 할 때 사용한다.
> ```groovy
> tasks.register('<테스크 명>') {
>     doFirst {
>           // 태스크 내에서 doLast 보다 먼저 처리할 내용
>     }
>     doLast {
>           // 태스크 내에서 doFirst 보다 나중에 처리할 내용
>     }
> }
> ```

### 파라미터 받기
> ```groovy
> tasks.register('<테스크 명>') {
>   def <변수명> = <변수명>   // 변수 값이 문자인 경우
>   def <변수명> = <변수명>.toInteger()   // 변수 값이 숫자인 경우
> }
> ```
> 터미널: `gradle <테스크 명> -P<변수명1>=<변수값1> -P<변수명2>=<변수값2>...`
> 
> 예시
> ```groovy
> tasks.register('calc') {
>   def s = s
>   def x = x.toInteger()
>   def y = y.toInteger()
> 
>   if (s == '+') {
>       println x + '+' + y + '=' + (x+y)
>   } else if (s == '-') {
>       println x + '-' + y + '=' + (x-y)
>   }
> }
> ```

### Task 에서 변수 사용하기
> Task 에서 사용자 정의 변수를 정의해서 사용이 가능하다.   
> ```groovy
> tasks.register('hello') {
>   ext.myProperty = 'hello property'
> }
> 
> tasks.register('helloPrint') {
>   doLast {
>       println hello.myProperty
>   }
> }
> ```

### task chaining
> dependsOn 은 태스크 간에 의존 관계를 지정하는 역할을 한다.   
> finalizedBy 는 종료 태스크를 지정하는데 종료 태스크는 자바의 finally 와 유사한 성격을 가지고 있다. 
> 종료 태스크는 지정된 태스크에서 에러나 예외가 발생하더라도 실행된다. 
> 단 해당 Task 의 doFirst 혹은 doLast 블록에 있는 내용이 dependsOn 및 finalizedBy 에 맞게 실행된다.  
> ```groovy
> tasks.register('exeTask1') {
>     doLast {
>         throw new Exception()
>     }
> }
> 
> tasks.register('exeTask2') {
>     dependsOn: 'exeTask1'
> 
>     doLast {
>         println 'exeTask 2'
>     }
> }
> 
> tasks.register('exeTask3') {
>     dependsOn: 'exeTask2'
> 
>     doLast {
>         println 'exeTask 3'
>     }
> }
> 
> tasks.register('finishTask') {
>     doLast {
>         println 'finish task~~~~~'
>     }
> }
> 
> exeTask1.finalizedBy finishTask
> ```
> 실행
> ```shell
> ./gradlew exeTask3
> ```

### 테스트 제외
> 테스트를 제외하고 싶은 경우 ex. entity, repository 테스트 제외
> ```groovy
> tasks.named('test') {
>     exclude '**/entity/**'
>     exclude '**/repository/**'
>     ...
> }
> ```

### 테스트 하나만 지정해서 실행
> `gradle test --tests "a.b.c.MyTestFile.mySingleTest"`

### 포함된 테스크 제외하며 실행
> `gradle bootJar` 의 경우 test 태스크 및 compileJava 태스트 등의 테스크가 실행된다.    
> gradle bootJar 태스크에서 test 태스크와 compileJava 태스크를 제외하여 실행하고 싶으면 뒤에 `-x <task 명>`를 붙인다.    
> 예시: `gradle bootJar -x test -x compileJava`  

### tasks.named
> **tasks.register**  
> tasks.register 메서드는 새로운 태스크를 정의하고 등록하는 데 사용됩니다.
> 이 메서드는 지연 초기화(lazy initialization)를 지원합니다. 즉, 태스크는 실제로 필요할 때까지 초기화되거나 구성되지 않습니다. 
> 이는 빌드 성능을 향상시키는 데 유용합니다. 태스크가 실행되는 시점까지 태스크의 구성이 연기됩니다.
> 예시:
> ```groovy
> Copy code
> tasks.register("myTask") {
>     doLast {
>         println "This is a new task"
>     }
> }
> ```
> **tasks.named**  
> tasks.named 메서드는 이미 존재하는 태스크를 참조하고 구성하는 데 사용됩니다.
> 이 메서드 역시 지연 초기화를 지원합니다. 태스크의 구성을 변경하고자 할 때까지 실제 태스크 객체가 생성되지 않습니다.
> 이미 정의된 태스크의 구성을 변경하거나 추가 설정을 하고자 할 때 주로 사용됩니다.
> 예시:
> ```groovy
> Copy code
> tasks.named("existingTask") {
>     doLast {
>         println "This is an existing task with new configuration"
>     }
> }
> ```
> tasks.register 는 새로운 태스크를 만들 때 사용되며, tasks.named 는 기존 태스크를 참조하고 그 설정을 변경할 때 
> 사용됩니다. 둘 다 지연 초기화를 통해 Gradle 빌드 성능을 최적화하는 데 도움이 됩니다.

### 참조사이트
> [Gradle task의 초간단 이해](https://sharplee7.tistory.com/7)

---

## Repositories
### 개요
> 의존 라이브러리를 build.gradle 의 `dependencies` 에 명시하면 build.gradle 의 `repositories` 에 명시된 온라인 저장소들에서 명시한 의존 라이브러리들을 다운로드 한다.

### Maven 중앙 저장소
> build.gradle 에 저장소 추가
> ```groovy
> ...
> repositories {
>   ...
>   mavenCentral()
> }
> ...
> ```
> Apache Maven 중앙 저장소를 추가한다.  

### jcenter(현재 미사용 저장소) 
> jcenter 는 Maven 과 Gradle 등 각종 빌드 도구에서 사용할 수 있는 공개 저장소이다.  
> 보통 안드로이드 프로젝트에서 사용되었으며 SpringBoot 프로젝트에서는 maven central 저장소가 주로 사용되었다.  
> 하지만 안드로이드 프로젝트 역시 2022년 2월 11일 이후로는 jcenter 저장소를 지원하지 않으며 모두 maven central 저장소로 이동하였다.  
> build.gradle 에 저장소 추가
> ```groovy
> ...
> repositories {
>   ...
>   jcenter()
> }
> ...
> ```

---

## Dependencies
### compile (3.0 이후 Deprecated)
> `compile` 로 의존 라이브러리를 기술하게 되면 소스 컴파일 시에 해당 라이브러리가 의존하는 상위 라이브러리까지 모두 컴파일 대상이된다.  
> 대신 `implementation` 을 사용하여 소스 컴파일하면 해당 라이브러리만 컴파일 하기 때문에 빌드 시간이 절약된다.  
> 현재는 Deprecated `compile` 대신에 `api` 를 사용한다.  

### classpath
> classpath 는 클래스나 jar 파일이 존재하는 위치이다.  
> classpath 는 `compile-time classpath` 와 `run-time classpath` 로 나누어진다.  
> `compile-time classpath`: 에러 없이 컴파일을 하기 위해 필요한 클래스와 jar 들의 위치.  
> `run-time classpath`: 애플리케이션이 정상적으로 실행하기 위해 필요한 클래스와 jar 들의 위치.
> 
> 예를 들어 main 클래스에서 B 라이브러리를 사용하고, B 는 C 라이브러리에 의존성이 있다고 가정해보자.  
> 컴파일 시점에서는 classpath 에 main 클래스와 B 라이브러리에 대한 정보만 있어도 컴파일에는 문제가 없지만,
> 런타임 시에는 classpath 에 main 클래스와 B 라이브러리 뿐만 아니라
> B 라이브러리가 동작하기 위해서 의존하는 C 라이브러리까지 모두 있어야한다.

### implementation
> 3.0 이후 compile 에서 변경되었으며, implementation 를 통해서 의존하는 라이브러리를 추가하는 경우 해당 라이브러리를 compile-time classpath 와
> run-time classpath 모두에 추가한다.  
> implementation 를 통해서 의존하는 라이브러리를 추가하는 경우 해당 라이브러리만 compile-time classpath 에 추가되어 빌드되게 된다.

### compileOnly
> compileOnly 를 통해 의존하는 라이브러리를 추가하는 경우 해당 라이브러리를 compile-time classpath 에만 추가하게 된다.    
> compileOnly 를 사용하는 주요 라이브러리는 lombok 으로 lombok 애노테이션을 compile 시에만 바이너리 파일로 컴파일하게 되면 그 후로는 lombok 의
> 기능을 runtime 에는 사용할 일이 없다.  

### runtimeOnly
> runtimeOnly 를 통해 의존하는 라이브러리를 추가하는 경우 해당 라이브러리를 run-time classpath 에만 추가하게 된다.  
> runtimeOnly 를 사용하는 주요 라이브러리는 DB 관련이나 로그관련 라이브러리이다.  
> DB 관련 라이브러리를 프로젝트 내에서 직접 사용하지 않고 jdbc 를 사용하기 때문에 compile 시점에는 필요가 없다.

### api
> 3.0 이후 추가되었으며, api 를 통해서 의존하는 라이브러리를 추가하는 경우 해당 라이브러리를 compile-time classpath 와
> run-time classpath 모두에 추가한다.
> api 를 통해서 의존하는 라이브러리를 추가하는 경우 해당 라이브러리 뿐만 아니라 해당 라이브러리가 의존하는 라이브러리까지 모두 
> compile-time classpath 에 추가되어 빌드되게 된다.  

### annotationProcessor
> Gradle 에서는 컴파일 classpath 와 애노테이션 프로세서 classpath 를 분리하여 빌드 성능을 향상시킨다.
> 기본적으로 포함되어 있는 애노테이션이 아니라면 `annotationProcessor` 를 통해 명시적으로 추가를 해줘야 한다.  
> 일반적으로는 lombok 사용시에 사용한다.  

### test
> `implementation` 은 테스트를 포함한 전 범위에 걸쳐서 의존성이 적용된다.    
> `testImplementation` 은 테스트 시에만 의존성이 적용된다.  
> `compileOnly` 은 일반 빌드 시에만 적용되며, 테스트 시에는 적용되지 않아 테스트에도 의존성 적용시에는 testCompileOnly 를 따로 추가해야한다.  
> `runtimeOnly` 는 일반 빌드 및 테스트를 포함한 전 범위에 걸쳐서 의존성이 적용된다.  
> 
> Test 파일에서 lombok 을 사용하는 경우 다음 dependency 추가
> ```groovy
> dependencies {
>     ...
>     testCompileOnly 'org.projectlombok:lombok'
>     testAnnotationProcessor 'org.projectlombok:lombok' 
> }
> ```

### 참조사이트
> [[Spring] Gradle 파일 implementation, api, runtimeOnly, compileOnly... 등에 대해](https://bepoz-study-diary.tistory.com/372)
> [[Gradle] build.gradle의 dependencies 블록 한 번에 정리하기. implementation, testImplementaion의 차이와 라이브러리 구성](https://kotlinworld.com/316)

--- 

## 서비스로 실행 가능한 Jar 파일 생성
### build.gradle
> ```groovy
> ...
> plugins {
>     id 'org.springframework.boot' version '2.6.3'
>     id 'io.spring.dependency-management' version '1.0.11.RELEASE'
>     ...
> }
> ...
> springBoot {
>     executable = true
> }
> ...
> ```

### 서비스 스크립트 등록
> 배포 서버에서 실행할 스크립트 예제이다.
> ```shell
> # 빌드된 프로젝트를 서비스로 등록
> sudo ln -s /home/some-project/some-project.jar /etc/init.d/some-project
> 
> # 등록한 서비스에 실행 권한 부여
> sudo chmod 0755 /etc/init.d/some-project
> 
> # 서비스 실행시 적용될 JVM 옵션 설정
> vi /home/some-project/some-project.conf
> PID_FOLDER='/home/some-project'
> LOG_FOLDER='/dev'
> LOG_FILENAME='null'
> JAVA_OPTS='-server -Xms8g -Xmx8g -XX:MaxMetaspaceSize=512m -Dspring.profiles.active=prod'
> :wq
> ```
> /etc/init.d/ 경로에 빌드된 프로젝트의 .jar 파일의 심볼릭 링크를 생성하고 파일 실행 권한을 부여하는 것 만으로 운영체제 내의 정식 서비스로 작동하게 된다. 
> 이 작업은 최초 1번만 필요하며, 추후 빌드된 파일의 경로와 이름이 변경되지 않는한 자동으로 적용된다.
> 
> 추가적으로 빌드된 프로젝트의 .jar 파일과 동일한 디렉토리에 동일한 파일 이름으로 .conf 파일을 작성하면 서비스 실행시 적용될 다양한 옵션을 자동으로 적용할 수 있다.
> 
> .conf 파일에서 LOG_FOLDER와 LOG_FILENAME 옵션을 사용하면 기본적으로 콘솔에 출력되는 로그를 실시간으로 파일에 남길 수 있다. 
> 하지만 Spring Boot에 기본 내장된 Logback을 이용한 파일 로깅(logback.xml에 로그 처리 정책을 정의하는 방법)이 훨씬 강력하고 다양한 기능을 제공하기 때문에
> 위와 같이 /dev/null을 지정하여 서비스 레벨에서의 로그 기능을 비활성화하는 방법을 추천한다.
>
> 다시 정리하면, 최종적으로 빌드된 some-project.jar, 이와 파일 이름이 동일한 some-project.conf 2개 파일이 존재해야 하고, 
> 해당 some-project.jar에 대한 심볼릭 링크를 /etc/init.d/some-project로 생성하면 해당 애플리케이션의 서비스로서의 실행 준비가 완료되는 것이다.

### 참조사이트
> [Spring Boot 2.0, 리눅스에서 제어 가능한 서비스로 빌드하기](https://jsonobject.tistory.com/453)

---

## Plugins
### Java plugin
> build.gradle 에 플러그인 추가
> ```groovy
> ...
> plugins {
>   id 'java'
>   ...
> }
> ...
> ```
> java 플러그인에 `compileJava` 태스크가 포함되어 있으며 `gradle compileJava` 태스크를 통해서 Java 소스 컴파일을 실행한다.

### Application plugin
> build.gradle 에 플러그인 추가
> ```groovy
> ...
> plugins {
>   id 'application'
>   ...
> }
> ...
> application {
>     // Define the main class for the application.
>     mainClass = 'gradle.java.App'
> }
> ```
> application 플러그인은 main 메서드로 동작하는 애플리케이션 프로그램을 실행하기 위한 플러그인.  
> build.gradle 에 application 에 mainClass 로 <패키지명>.<MainClass> 명을 명시하고 `gradle run` 으로 실행하면 main 메서드를 entrypoint 로 실행된다.   
> 단 springboot 에서는 application 플러그인이 사용되지 않는다.

### QueryDSL plugin
> 주의: 문자열 안에서 외부 선언 변수를 사용하기 위해서는 문자열을 '' 가 아닌 ""로 사용해야한다.  
> ex: `implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"`
> ```groovy
> buildscript {
>     ext {
>         queryDslVersion = '5.0.0'
>         ...
>     }
> }
> 
> plugins {
>     ...
>     id "com.ewerk.gradle.plugins.querydsl" version '1.0.10'
> }
> 
> dependencies {
>     ...
>     implementation "com.querydsl:querydsl-jpa:${queryDslVersion}"
>     implementation "com.querydsl:querydsl-apt:${queryDslVersion}" 
> }
> 
> //querydsl 추가 시작
> def querydslDir = "$buildDir/generated/querydsl"
> querydsl {
>     jpa = true
>     querydslSourcesDir = querydslDir
> }
> sourceSets {
>     main.java.srcDir querydslDir
> }
> configurations {
>     compileOnly {
>         extendsFrom annotationProcessor
>     }
>     querydsl.extendsFrom compileClasspath
> }
> compileQuerydsl {
>     options.annotationProcessorPath = configurations.querydsl
> }
> //querydsl 추가 끝
> ```

### Spring Rest Doc plugin
> adoc 파일은 src/main 아래 asciidoc 디렉터리에 넣는다.
> ```groovy
> plugins {
>     ...
>     id "org.asciidoctor.jvm.convert" version '3.3.2'
> }
> 
> dependencies {
>     ...
>     testImplementation 'org.springframework.restdocs:spring-restdocs-mockmvc:2.0.6.RELEASE'
> }
> 
> ext {
>     snippetsDir = file('build/generated-snippets')
> }
>
> tasks.named('compileJava') {
>     dependsOn copyResources
> }
> 
> tasks.named('bootJar') {
>     layered
>     dependsOn asciidoctor
>     // asciidoctor
>     copy {
>         from '${asciidoctor.outputDir}'
>         into 'BOOT-INF/classes/static/docs'
>     }
>     finalizedBy 'copyDocument'
> }
> 
> tasks.named('asciidoctor') {
>     inputs.dir snippetsDir
>     dependsOn test
>     doFirst {
>         delete file('src/main/resources/static/docs')
>     }
> }
> 
> tasks.register('copyResources', Copy) {
>     from "${projectDir}/src/main/resources"
>     into "${buildDir}/resources/main"
> }
> 
> tasks.register('copyDocument', Copy) {
>     dependsOn bootJar
>     from file("src/main/asciidoc")
>     into file("src/main/resources/static/docs")
> }
> ```

### Maven publish plugin: Deploy - AWS S3
> ```groovy
> import com.amazonaws.auth.profile.ProfileCredentialsProvider
> 
> buildscript {
>     ext {
>         ...
>         awsSdkVersion = '1.12.286'
>     }
>     dependencies {
>         classpath "com.amazonaws:aws-java-sdk-core:${awsSdkVersion}"
>     }
> }
> 
> plugins {
>     ...
>     id 'maven-publish'
> }
> 
> publishing {
>     publications {
>         mavenJava(MavenPublication) {
>             artifact bootJar  // repository 에 fat jar 배포
>         }
>     }
> 
>     repositories {
>         maven {
>             credentials(AwsCredentials) {
>                 def credentials = new ProfileCredentialsProvider().getCredentials()
>                 accessKey credentials.getAWSAccessKeyId()
>                 secretKey credentials.getAWSSecretKey()
>             }
> 
>             if (project.version.endsWith('-SNAPSHOT')) {
>                 url "s3://<s3 repository>/snapshot/"
>             } else {
>                 url "s3://<s3 repository>/release/"
>             }
>         }
>     }
> }
> ```

### SpringBoot plugin
> ```groovy
> plugins {
>     id 'java'
>     id 'org.springframework.boot' version '2.7.14'
>     id 'io.spring.dependency-management' version '1.0.15.RELEASE'
>     ...
> }
> 
> group = 'com.example'
> version = '0.0.1'
> ```
> 
> spring dependency 에서 로깅 라이브러리 제거  
> ```groovy
> configurations {
>     ...
>     all {
>         exclude module: 'spring-boot-starter-logging'
>     }
> }
> ```

### checkstyle plugin
> Checkstyle은 Java 소스 코드에 대해 정적 분석을 수행하는 도구로, 코드 스타일과 코딩 규칙을 강제하는 데 사용됩니다. 
> Gradle에서 Checkstyle 플러그인을 사용하면 프로젝트의 빌드 과정에 자동으로 코드 스타일 검사를 포함할 수 있습니다. 
> 이를 통해 코드가 일관된 스타일을 유지하도록 하며, 잠재적인 오류를 미리 찾아낼 수 있습니다.
> 
> **적용**  
> 1. 프로젝트 Root 에 `checkstyle` 디렉터리를 생성
> 2. checkstyle.xml 파일을 구글링하여 다운로드 후 checkstyle 디렉터리로 이동. 여기선 naver checkstyle 을 다운받아 사용함.  
> 3. build.gradle 에 다음 내용 추가
> ```groovy
> plugins {
>     id 'checkstyle'
> }
> ...
> 
> checkstyle {
>     // 네이버 체크스타일 룰 사용
>     configFile = file("checkstyle/naver-checkstyle-rules.xml")
>     configProperties = ["suppressionFile": "checkstyle/naver-checkstyle-suppressions.xml"]
>     sourceSets = [sourceSets.main] // CompileQuerydsl 오류 해결
> }
> 
> checkstyleMain.source = fileTree('src/main/java')
> 
> // checkstyle 에서 제외 시킬 클래스 지정
> checkstyleMain
>     .exclude('com/example/ExcludeExample1.java')
>     .exclude('com/example/exclude/*.java')
> ```
> 4. `gradle build` 명령어 실행
> 5. `프로젝트 루트/build/reports/checkstyle/main.html` 을 열어서 결과 확인
> 
> **IntelliJ 에 checkstyle 적용하기**  
> Preferences(Command + ,) 이동 -> Editor/Code Style/Java 이동 -> Scheme 옆에 세로 점 3개 아이콘 클릭 후 Import Scheme 
> -> IntelliJ IDEA code style XML 클릭 -> 아래 참조사이트를 통해서 다운받은 naver-intellij-formatter.xml 선택
> 
> **참조사이트**  
> [Gradle Project에 checkstyle 설정하기](https://dukcode.github.io/cicd/setting-checkstyle/)  
> [naver/hackday-conventions-java](https://github.com/naver/hackday-conventions-java)  

### JaCoCo plugin
> JaCoCo는 Java 코드의 커버리지를 체크하는 라이브러리입니다. 
> 테스트코드를 돌리고 그 커버리지 결과를 눈으로 보기 좋도록 html이나 xml, csv 같은 리포트로 생성합니다. 
> 그리고 테스트 결과가 내가 설정한 커버리지 기준을 만족하는지 확인하는 기능도 있습니다.
> 
> **build.gradle**    
> ```groovy
> plugins {
>     id 'jacoco'
> }
> 
> jacoco {
>     // JaCoCo 버전
>     toolVersion = '0.8.5'
>     
>     //  테스트결과 리포트를 저장할 경로 변경
>     //  default는 "$/jacoco"
>     //  reportsDir = file("$buildDir/customJacocoReportDir")
> }
> ```
> 
> **Gradle task 설정 – 테스트 리포트 저장과 커버리지 체크**  
> JaCoCo Gradle 플러그인에는 jacocoTestReport와 jacocoTestCoverageVerification task가 있습니다.
> 
> jacocoTestReport: 바이너리 커버리지 결과를 사람이 읽기 좋은 형태의 리포트로 저장합니다. 
> html 파일로 생성해 사람이 쉽게 눈으로 확인할 수도 있고, SonarQube 등으로 연동하기 위해 xml, csv 같은 형태로도 리포트를 생성할 수 있습니다.
> jacocoTestCoverageVerification: 내가 원하는 커버리지 기준을 만족하는지 확인해 주는 task입니다. 
> 예를 들어, 브랜치 커버리지를 최소한 80% 이상으로 유지하고 싶다면, 이 task에 설정하면 됩니다. test task처럼 Gradle 빌드의 성공/실패로 결과를 보여줍니다.
> 
> ```groovy
> tasks.named('test') {
>     ...
>     finalizedBy 'jacocoTestReport'
> }
> 
> tasks.named('jacocoTestReport') {
>     reports {
>         // 원하는 리포트를 켜고 끌 수 있습니다.
>         html.required = true
>         xml.required = false
>         csv.required = false
>         
>         //  각 리포트 타입 마다 리포트 저장 경로를 설정할 수 있습니다.
>         //  html.destination file("$buildDir/jacocoHtml")
>         //  xml.destination file("$buildDir/jacoco.xml")
> 
>         finalizedBy 'jacocoTestCoverageVerification'
>     }
> }
> 
> tasks.named('jacocoTestCoverageVerification') {
>     violationRules {
>         rule {
>             element = 'CLASS'
>             
>              limit {
>                   counter = 'BRANCH'
>                   value = 'COVEREDRATIO'
>                   minimum = 0.90
>              }
>              // 커버리지 체크를 제외할 클래스들
>              excludes = [
>                 '*.test.*',
>                 '*.Kotlin*'
>              ]
>         }
>     }
> }
> ```
> JaCoCo 플러그인은 자동으로 모든 Test 타입의 task에 JacocoTaskExtension을 추가하고, 
> test task에서 그 설정을 변경할 수 있게 합니다. (JaCoCo specific task configuration) 
> 그래서 아래 설정처럼 test task에서 extension을 설정할 수 있습니다. 
> 아래 설정은 커버리지 결과 데이터를 저장할 경로를 변경하는 것이고, unit test와 integration test 등을 분리할 때 
> 사용하면 유용할 수 있습니다.
> 
> ```groovy
> test {
>     jacoco {
>         destinationFile = file("$buildDir/jacoco/jacoco.exec")
>     }
> }
> ```
> 
> **참조사이트**  
> [Gradle 프로젝트에 JaCoCo 설정하기](https://techblog.woowahan.com/2661/)

### Docker plugin
> TODO

---

## Deploy
### 개요
> Gradle + AWS CodeBuild 를 통하여 스프링부트 프로젝트를 배포하는 과정을 정리하였다.   
> build.gradle 파일에 아래의 추가 작업을 통해서 executable-jar 파일 외에 실행 스크립트 및 외부 application-XXX.yml 을 생성하여 S3 bucket 에 전송한다.     

### buildspec.yml
> AWS CodeBuild 에서 프로젝트 빌드를 위해서 프로젝트에 루트에 `buildspec.yml` 을 위치시킨다.  
> 
> `build`: 프로젝트 빌드에 관한 정보를 담는다.  
> `build.on-failure`: 빌드 중 오류가 발생하여 빌드가 실패한 경우 해야할 작업을 기술한다.(ABORT, CONTINUE 중 택 1)  
> `build.commands`: 빌드 작업 시 실행할 명령어들의 목록  
> 
> `post_build`: 빌드가 성공적으로 완료되면 이후 실행할 프로세스에 대한 정보를 담는다.    
> `post_build.on-failure`: 포스트 빌드 중 오류가 발생하여 포스트 빌드가 실패한 경우 해야할 작업을 기술한다.(ABORT, CONTINUE 중 택 1)  
> `post_build.commands`: 포스트 빌드 작업 시 실행할 명령어들의 목록  
> 
> `artifacts`: 빌드 산출물(artifact)에 대한 정보  
> `files`: S3 에 올릴 파일 목록  
> `discard-paths`: 산출물이 존재하는 경로를 버리고 파일 자체들만 S3 에 위치시킬 경우 yes, 디렉터리 경로를 유지해서 S3 에 넣을 경우 no  
> 
> ```yaml
> version: 0.2
> phases:
>   build:
>       on-failure: ABORT
>       commands:
>           - echo Build Starting on `date`
>           - java -version
>           - chmod +x ./gradlew
>           - ./gradlew bootJar -Pprofile=dev -x test -x asciidoctor
>   post_build:
>       on-failure: ABORT
>       commands:
>           - echo $(basename ./build/libs/*.jar)
>           - echo $(basename ./build/scripts/*.sh)
>           - echo $(basename ./build/resources/main/*.yml)
>           - pwd
> artifacts:
>   files:
>       - build/libs/*.jar
>       - build/scripts/*.sh
>       - build/resources/main/application-dev.yml
>   discard-paths: yes
> ```

### build.gradle
> `afterEvaluate`: 빌드가 완료된 후에 실행하는 태스크, 이 태스크를 통해서 배포 스크립트를 생성한다.
> `-Dspring.config.import=application-dev.yml`: 스프링 프로젝트가 application.yml 을 사용하면서 application-dev.yml 을 같이 사용하려할 때
> import 옵션을 사용한다.  
> 
> ```groovy
> buildscript {
>     ext {
>         ...
>         profile = (!project.hasProperty('profile') || !profile) ? 'local' : profile
>         deployPath = profile.equals("dev") ?
>                 "/home/starter/${rootProject.name}" : "/home/ec2-user/starter/${rootProject.name}"
>     }
> } 
> ...
> afterEvaluate {
>   mkdir "${buildDir}/scripts"
>   def script = "${buildDir}/scripts/start-${rootProject.name}.sh"
>   
>       if (profile.equals("dev")) {
>           file(script).text = "/bin/java -jar -Dspring.config.import=application-dev.yml -Dspring.profiles.active=${profile} ${bootJar.archiveFileName.get()} &"
>       } else {
>           file(script).text = """#!/bin/bash
>               sudo chmod +x ${deployPath}/${bootJar.archiveFileName.get()}
>               sudo ln -sf ${deployPath}/${bootJar.archiveFileName.get()} /etc/init.d/${rootProject.name}
>               sudo service ${rootProject.name} start
>           """
>       }
>       file(script).setExecutable(true)
>   
>       if (profile.equals("prod") || profile.equals("staging")) {
>           mkdir "${buildDir}/conf"
>           def conf = "${buildDir}/conf/${rootProject.name}.conf"
>           file(conf).text = "JAVA_OPTS='-Dspring.profiles.active=${profile}'\nPID_FOLDER='${deployPath}'\n"
>       }
> }
> ```

### 참조사이트
> [Spring Boot 2.0, 리눅스에서 제어 가능한 서비스로 빌드하기](https://jsonobject.tistory.com/453)  
> [[Gradle] Profile 구성하기](https://velog.io/@iniestar/gradle-profile)  
> [에 대한 빌드 사양 참조 CodeBuild](https://docs.aws.amazon.com/ko_kr/codebuild/latest/userguide/build-spec-ref.html)  

---

## 그레이들의 도메인 객체
### Project 객체
> Project 객체의 속성.
> * version
> * description
> * name
> * state: 프로젝트 빌드 상태(NOT EXECUTED, EXECUTING, EXECUTED, FAILED)
> * status: 프로젝트 결과물의 상태(NOT EXECUTED, EXECUTING, EXECUTED, FAILED)
> * path: 프로젝트 경로
> * projectDir: 프로젝트 기준 디렉터리
> * group
> * buildDir: 모든 결과물이 생성되는 디렉터리, 기본값: projectDir/build
> * plugins
> * project: 기준 프로젝트 참조
> * rootProject: 루트 프로젝트 참조
> * parent: 기준 프로젝트의 상위 프로젝트 참조
> * childProject
> * allprojects
> * subproject
> 
> Project 객체의 API.
> * project(path): 지정된 경로의 프로젝트에 대하여 설정
> * project(path, configureClosure): 지정된 경로의 프로젝트에 대하여 클로저를 사용하여 설정
> * absoluteProjectPath(path): 절대 경로를 변환하여 프로젝트 확인
> * apply(closure): 플러그인이나 스크립트를 적용
> * configure(object, configureClosure): 클로저를 통하여 설정된 상태를 이용하여 객체를 구성
> * subprojects(action): 해당 프로젝트의 하위 프로젝트 설정
> * task(name): 주어진 이름으로 태스크를 생성하고 프로젝트에 추가
> * afterEvaluate(action): 프로젝트가 평가된 직후 추가
> * beforeEvaluate(action): 프로젝트가 평가되기 바로 직전 추가

### Task 객체
> Task 객체가 실행될 때 예외가 발생하더라도 빌드의 성공 여부를 실패로 만들지 않고 계속 다음 단계로 진행하게 예외 처리를 할 수 있도록 한다.  
> StopActionException 은 지금 실행되고 있는 태스크를 중단하고 예외를 throw 처리하여 다음에 예정된 태스크를 계속할 수 있도록 해주며,
> StopExecutionException 은 태스크 실행을 중단하고 다음 태스크로 계속 진행할 수 있도록 하여 빌드를 끝까지 수행할 수 있도록 할 수 있다.  

### Settings 객체
> 설정 스크립트를 참조할 수 있게 위임받는 객체로, 주로 멀티 프로젝트를 정의하기 위한 용도로 많이 사용한다.  
> 
> **Settings 객체와 멀티 프로젝트**  
> `include()` 는 루트 프로젝트를 기준으로 계층형 멀티 프로젝트를 구성할 때 사용한다.  
> `includeFlat()` 은 루트 프로젝트와 동일한 레벨의 디렉터리로 프로젝트(딘층형 멀티 프로젝트)를 구성할 때 사용한다.

---

## 그레이들의 파일 처리
### 파일 검증
> ```groovy
> File checkFile = file('/index.html', PathValidation.FILE)
> File checkDirectory = file('src', PathValidation.DIRECTORY)
> ```
> 
> * PathValidation.DIRECTORY: 디렉터리 유무 확인 
> * PathValidation.FILE: 파일 유무 확인
> * PathValidation.EXISTS: 파일 또는 디렉터리 유무 확인
> * PathValidation.NONE: 파일 검증 안함

### FileCollection
> ```groovy
> // 파일 컬렉션 생성
> FileCollection fileCollection = files('settings.txt', 'login.txt', new File('infro.java'), new File('index.html'))
> 
> // 텍스트 파일에 대하여 필터링
> FileCollection txtFilter = fileCollection.filter{collectionFile -> collectionFile.name.endsWith '.txt'}
> ```

### Copy 태스크
> 그레이들은 파일을 복사하기 위해 copy 라는 태스크를 제공한다.  
> ```groovy
> copy {
>     from ('scripts/text1.txt')    // 대상 파일의 경로
>     into file('scripts/text2')    // 목적지 경로(마지막에 디렉터리가 와야함)
> }
> ```
>
> include/exclude 를 통한 복사할 파일 포함 및 제외
> ```groovy
> copy {
>     from ('src')    // 대상 파일의 경로
>     into file('src-copy')    // 목적지 경로(마지막에 디렉터리가 와야함)
>     
>     // 파일 포함 및 제외
>     include '**/*.java'
>     exclude '**/*Dao.java'
>       
>     // 디렉터리 포함 및 제외
>     includeEmptyDirs = true
>     includeEmptyDirs = false
> }
> ``` 
>
> rename: 파일명 변경
> ```groovy
> rename '(.*)Test.java', 'changeName.java'
> ```
> 
> from 클로저와 rename 을 이용한 파일 이름 변경
> ```groovy
> copy {
>     from('src/com/org/file') {
>         rename 'original.java', 'usingCloser.java'
>     }
>     into 'src/com/des/file'
> }
> ```

### 태스크를 이용한 파일 복사
> ```groovy
> // type 에 copy 를 지정해야 한다.
> tasks.register("copyTask", Copy) {
>     // 디렉터리 생성
>     mkdir 'dest'
> 
>     from('scripts') {
>         include '**/*.txt'
>         rename 'text1.txt', 'text2.txt'
>     }
>     into 'dest'
>      
>     // filter 를 이용한 파일 내용 변경
>     filter { line ->
>         line.replaceAll 'text1', 'text2' 
>     } 
> }
> ```

### 파일 삭제
> ```groovy
> tasks.register('delFile', Delete) {
>     delete 'src/com/org/original.java', 'src/com/org/originalDao.java'
>     // 심볼릭 링크 사용 여부 설정
>     followSymlinks = true
> }
> ```
> followSymlinks 는 파일을 삭제할 때 심볼릭 링크를 따라야 하는지 여부를 지정하는 것으로 true 일 경우
> 심볼릭 링크에 의하여 파일 삭제가 이루어진다고 보면 된다.

--- 

## 의존 관계
### 환경 구성
> 그레이들에서 환경 구성을 정의하려면 `configurations` 블록을 사용하면 된다. 메이븐의 scope 와 유사하다.  
> ```groovy
> configurations {
>     conf1
> }
> ```

### 의존 관계 지정 방법
> **외부 모듈 의존 관계 정의**  
> 의존 관계를 정의할 때 많이 사용하는 방법 중 하나가 외부 모듈 의존 관계 지정을 통해 정의하는 것이다.  
> * 외부 모듈 의존 관계 지정: 인터넷 저장소에 대하여 의존 관계 지정  
> 
> ```groovy
> // 저장소 정의
> repositories {
>     mavenCentral()
> }
> 
> // 의존 관계 지정
> dependencies {
>     conf1 'ch.qos.logback:logback-classic:1.0.13'
> }
> ```
> 
> **파일 의존 관계 정의**  
> 파일 의존 관계를 지정하려면 files() 나 fileTree() 를 사용한다.  
> 특정 파일이나 라이브러리를 지정할 때는 files() 를 이용하여 지정한다.  
> 디렉터리에 대하여 해당 디렉터리에 있는 모든 내용을 의존 관계로 정의하기를 원한다면 fileTree() 를 사용한다.  
> 
> ```groovy
> configurations {
>     conf1
> }
> 
> dependencies {
>     // 1. 파일 의존 관계 - 특정 파일이나 라이브러리 지정
>     conf1 files("lib/commonLib.jar")
>     
>     // 2. 파일 의존 관계 - 디렉터리 지정
>     conf1 fileTree(dir:"lib", include:"**/*.jar")
> }
> ```
> 
> **프로젝트 의존 관계 정의**  
> project() 를 이용해 다른 프로젝트를 참조한다. 인수로 참조하고자 하는 프로젝트 경로를 지정한다.
> 프로젝트 경로는 루트 프로젝트를 기준으로 하게 된다. 
> ```groovy
> dependencies {
>     compile project(':subProject')
> }
> ```

### 변경성 모듈 정의
> dependencies 블록에서 의존 관계를 정의할 때 시간이 경과하면서 정의된 모듈 또는 라이브러리의 버전은 새롭게 출시되어
> 변경된다. 이럴 때 참조하고자 지정한 의존 관계의 모듈의 버전을 동적으로 관리하는 방법을 살펴본다.  
> 
> ```groovy
> configurations {
>     confDef
> }
> 
> // 변경성 모듈에 대한 캐시 간격 지정
> configurations.confDef.resolutionStrategy.cacheDynamicVersionsFor 10, 'minutes'
> configurations.confDef.resolutionStrategy.cacheChangingModulesFor 10, 'hours'
> 
> // 저장소 정의
> repositories {
>     mavenCentral()
>     maven {
>         url "https://repository.apache.org/content/groups/snapshots"
>     }
> }
> 
> // 의존 관계 정의
> dependencies {
>     // 1.x 버전 중 최신 버전에 대한 지정
>     confDef 'org.slf4j:slf4j-api:1.+'
>     // 출시 버전 중 최신 버전에 대한 지정
>     confDef 'commons-cli:commons-cli:latest.integration'
>     // 배포된 버전 중 최신 버전에 대한 지정
>     confDef 'junit:junit:latest.release'
> }
> ```
> * `1.+`: 1.x 버전 중 최신 버전에 대한 지정이다.  
> * `latest.integration`: 출시 버전의 안정도 유무에 상관없이 모든 출시 버전 중에서 최신 버전을 참조하도록 지정한다.  
> * `latest.release`: 출시 버전 중에서도 안정성이 검증된 버전 중에서 최신 버전을 참조하도록 지정한다.
> 
> 해당 프로젝트가 사용하는 라이브러리를 확인하는 태스크는 다음과 같다.
> ```shell
> ./gradlew dependencies
> ```
> 
> 다양한 라이브러리를 사용하다 보면 의존 관계에서 사용하고자 하는 라이브러리 또는 해당 라이브러리가 의존 관계에 의해 전이적으로 버전만 다르게
> 최적화되어 참조되어 사용되고 있다면 프로젝트는 라이브러리 A 와 라이브러리 B 중에서 어떤 라이브러리의 버전을 사용해야할지 판단의 문제가 발생한다.  
> 
> * 라이브러리 A: Lib-2.3.1.jar
> * 라이브러리 B: Lib-2.0.5.jar
> 
> 그레이들에서는 이럴 때 기본적으로 가장 최신 버전의 의존 관계를 사용하도록 지정되어 있다. 
> 또한 환경 구성 정의를 통해서 버전 충돌이 일어난 경우 빌드가 실패하도록 할 수도 있다.  
> ```groovy
> configurations {
>     conf1
>     testConf1.extendsFrom conf1
> }
> 
> // Fail 정책 사용
> configurations.testConf1 {
>     resolutionStrategy {
>         failOnVersionConflict()
>           
>         // Fail 정책 사용 시 특정 버전을 강제할 수도 있다.
>         force 'org.codehaus.Groovy:Groovy-all:2.3.1'
>     }
> }
> ```
> 
> 버전 충돌을 피하기 위해 exclude() 사용하여 문제가 되는 그룹에서 관련 라이브러리를 제외할 수 있다.  
> ```groovy
> dependencies {
>     testConf1('org.springframework.boot:spring-boot-starter-web') {
>         exclude module: 'spring-boot-starter-logging'
>     } 
> }
> ```

### 환경 구성 정의
> configurations 블록은 ConfigurationContainer 에 대하여 클로저로 실행되게 되어 있다.  
> ConfigurationContainer 는 해당 프로젝트의 구성을 선언하고 관리하는 역할을 한다.  
> 
> 환경 구성은 다른 환경 구성을 상속할 수 있는데, 이럴 때는 `extendsFrom` 을 사용한다.

---

## 테스트 자동화
### test 태스크
> ```groovy
> tasks.named('test') {
>     outputs.dir snippetsDir
>     // JUnit 사용
>     useJUnitPlatform()
>     
>     // 테스트에서 제외 
>     exclude '**/entity/**'
>     exclude '**/repository/**'
>     
>     // 테스트를 위한 Heap 메모리 셋팅
>     minHeapSize = "128m"
>     maxHeapSize = "512m"
>    
>     // 병렬 테스트를 위한 프로세스 갯수 설정
>     maxParallelForks = 4     
> }
> ```

### Report 웹 페이지
> SpringBoot + JUnit 을 사용하여 테스트 실행이 완료되면 `${projectDir}/build/reports/tests/test/index.html` 파일이 생성된다.  
> 해당 파일을 열면 테스트 결과에 대한 리포트를 볼 수 있다.  

### 병렬 테스트
> ```groovy
> tasks.named('test') {
>     ...    
>     // 1.갯수를 직접 설정
>     maxParallelForks = 4
>     // 2.Gradle 구동 머신의 프로세스 수만큼 설정
>     maxParallelForks = Runtime.runtime.availableProcessors()
>     // 3.구동 머신의 프로세스 수의 1/2 만큼 설정
>     maxParallelForks = Runtime.runtime.availableProcessors().intdiv(2) ?: 1      
> } 
> ```
> 주의: 단위 테스트만 있는 경우에는 gradlew 로 돌리든 인텔리제이로 돌리든 병렬 프로세스 사용보다 단일 프로세스 사용이 성능면에서 더 나았다.

---

## 그레이들 퍼블리싱
### 개요
> 그레이들은 ZIP 형식을 비롯하여 tar, jar, war, ear 등 다양한 압축 방식을 제공한다.

### zip
> zip 압축 파일 생성 스크립트
> ```groovy
> tasks.register('exeTask', Zip) {
>     // 압축 파일 이름 지정
>     baseName = "GradleZip"
>     // 압축파일에 포함시키고자 하는 디렉터리 위치
>     into("script") {
>         from("src") {
>             // 생성 포함 파일
>             include "*.html", "*.js", "*.xml"
>         } 
>     }
>     // 빈디렉터리 포함 여부 설정
>     includeEmptyDirs = false
> 
>     // 압축 파일 생성 위치 지정
>     destinationDir = file("zip")
>     // 압축 파일 이름 지정(baseName 대신 사용 가능)
>     archiveName = "Gradle.zip"
> }
> ```

### jar
> jar 압축 파일 생성을 위해서는 JAR 태스크에서 제공해주는 기능을 이용하게 되며 기본적으로는 앞에서 설명한 것처럼 zip 압축 파일 생성과 동일한 속성들이 
> 사용된다.
> ```groovy
> // 프로젝트 버전 지정
> version = 'Jar 1.0'
> 
> tasks.register('exeTask', Jar) {
>     // [baseName]-[appendix]-[version]-[classifier].[extension] 으로 지정된다. 이는 zip 과 동일하게 적용된다.
>     destinationDir = file("NewJar")
>     baseName = "Gradle"
>     appendix = "file"
>     classifier = "script"
>     version = "1_0"
>     
>     // manifest 설정
>     manifest {
>         attributes("Built-By": "Gradle",
>             "Implementation-Version" : project.version) 
>     }
>     // 압축 방식 지정
>     entryCompression = ZipEntryCompression.STORED
> } 
> ```
> manifest 는 프로젝트 또는 프로그램과 관련된 버전이나 의존성 등 내용을 포함한 부분으로, manifest 파일은 이러한 내용이 기재되어 있는 파일이다.
> manifest 블록을 이용하여 빌드를 수행할 때 manifest 파일을 생성할 수 있다. 빌드를 수행하게 되면 프로젝트에 build 디렉터리가 생성되면서 해당 
> 디렉터리 하위로 manifest 파일이 생성된다.
> 
> jar 압축 파일 생성 시 Jar 태스크를 이용하거나 java 플러그인을 사용하여 만든다.  

### Distribution 플러그인을 이용한 압축
> Distribution 플러그인을 사용하여 zip, tar 압축 파일을 생성하는 방법은 다음과 같다.
> ```groovy
> apply plugin 'distribution'
> 
> distribution {
>     main {
>         baseName = 'arcvName'
>         contents {
>             from { 'src' }
>         }
>     } 
> }
> ```

### 파일 퍼블리싱
> 압축 파일 생성을 통하여 나온 결과물을 로컬 저장소나 원격지로 퍼블리싱하는 방법으로 그레이들은 2가지의 플러그인을 사용한다.  
> `maven-publish` 플러그인과 `ivy-publish` 플러그인이다.  
> 
> 퍼블리싱 작업 순서는 다음과 같다.  
> 모듈 정의 -> 아티팩트 등록 -> 메타 데이터 편집 -> 퍼블리싱

### 메이븐 퍼블리싱 플러그인
> 선언
> ```groovy
> apply plugin 'maven-publish'
> ```
> 퍼블리싱을 수행하기 위하여 그레이들에서는 소프트웨어 컴포넌트(Software Component) 라는 개념을 사용하고 있다. 
> 이 소프트웨어 컴포넌트라는 개념을 이용하여 프로젝트에 추가할 수 있으며 소프트웨어 컴포넌트에는 아티팩트(Artifact)와 의존 관계 관련 정보가 포함되어 있다. 
> 즉, 소프트웨어 컴포넌트 지정을 통하여 그레이들은 메이븐 저장소나 기타 저장소에 퍼블리싱하기 위한 준비를 한다고 보면 된다.  
> 
> build.gradle
> ```groovy
> plugins {
>     id 'java'
>     id 'maven-publish'
> }
> 
> group = 'com.example'
> version = '1.0.0'
> sourceCompatibility = '1.8'
> 
> repositories {
> mavenCentral()
> }
> 
> dependencies {
> // 필요한 경우 의존성을 추가하세요
> }
> 
> publishing {
>     publications {
>         mavenJava(MavenPublication) {
>             from components.java
>     
>             artifactId = 'your-artifact-id' // 아티팩트 ID를 설정하세요
>         }
>     }
> 
>     repositories {
>         maven {
>             url = uri('https://your-maven-repo-url') // Maven 저장소 URL을 설정하세요
>             credentials {
>                 username = project.findProperty("mavenUsername") ?: System.getenv("MAVEN_USERNAME")
>                 password = project.findProperty("mavenPassword") ?: System.getenv("MAVEN_PASSWORD")
>             }
>         }
>     }
> }
> ```
> 프로젝트 루트 디렉토리에서 `./gradlew publish` 명령어를 실행하면 Maven 저장소에 프로젝트가 성공적으로 게시된다.
 
---

## 그레이들로 변환하기
### 그레이들에서 메이븐 사용
> 기본적으로 그레이들의 프로젝트 구조는 메이븐의 프로젝트 구조와 유사하고 이 덕분에 간단한 프로젝트라면 쉽게 그레이들로 변환할 수 있다. 그레이들은 메이븐의 
> 빌드 스크립트인 pom.xml 을 변환하여 build.gradle 파일이 포함된 새로운 그레이들 프로젝트를 생성하는 기능을 제공한다.
> 
> 그레이들에서는 메이븐 플러그인을 사용할 수 없다. 메이븐 플러그인을 사용할 수 없기 때문에 그레이들은 이에 상응하는 기능을 제공하는 그레이들 플러그인을 찾아서
> 적용해야 한다.
> 
> 메이븐 프로젝트를 그레이들 프로젝트로 변환하는 방법은 다음과 같다.
> 1. 메이븐 프로젝트로 이동한다.
> 2. 다음 명령어를 입력한다: `gradle init --type pom`

---

## 그레이들 구조화
### 사용자 정의 태스크
> ```groovy
> tasks.register('userTask', DefaultTask) {
>     ...
> }
> ```
> 위와 같이 태스크 이름 뒤에 DefaultTask 클래스를 지정하였다. 만약 저 부분을 지정하지 않았다면 내부적으로 DefaultTask 가 지정된다.
> 위의 형식을 이용하여 빌드 수행 시 추가로 사용자 정의 객체를 type 으로 지정하여 사용할 수 있다.
> 
> ```groovy
> // 사용자 정의 태스크
> tasks.register('calcuTask', CalcuGradle) {
>     msg = "Customer Task Test"
>     printMsg(msg)
> 
>     def a = 5
>     def b = 10
> 
>     plus(a, b)
>     minus(a, b)
>     multi(a, b)
>     div(a, b)
> }
> 
> // 태스크 클래스 정의
> class CalcuGradle extends DefaultTask {
> // 변수 선언
> @Input
> String msg
> 
>     // 클래스 생성자
>     CalcuGradle() {
>         doLast {
>             println "Calcu Start, $msg!"
>         }
>     }
> 
>     void printMsg(String str) {
>         doLast {
>             println "Alzio Contents: $str"
>         }
>     }
> 
>     void plus(int a, int b) {
>         doLast {
>             println "a+b = " + (a+b)
>         }
>     }
>     void minus(int a, int b) {
>         doLast {
>             println "a-b = " + (a-b)
>         }
>     }
>     void multi(int a, int b) {
>         doLast {
>             println "a*b = " + (a*b)
>         }
>     }
>     void div(int a, int b) {
>         doLast {
>             println "a/b = " + (a/b)
>         }
>     }
> } 
> ```
> calcuTask 태스크에 type 속성으로 CalcuGradle 클래스가 지정된 것을 확인할 수 있다.

### 사용자 정의 플러그인
> 사용자 정의 플러그인은 다음 같은 경우에 사용할 수 있다.
> * 다른 프로젝트에서 작성한 사용자 정의 태스크를 공유하여 사용할 때
> * 여러 개의 태스크를 조합하여 사용할 때
> * 파일, 설정 방법 등 새로운 규칙 및 방법을 정의하여 빌드 수행에 적용하고자 할 때
> 
> 플러그인을 만들어 사용하려면 `Plugin` 인터페이스를 구현하여 사용자 정의 플러그인을 작성해야 한다.
> ```groovy
> apply plugin: GradleUserPlugin
> 
> // 사용자 정의 플러그인
> class GradleUserPlugin implements Plugin<Project> {
> 
>     // 플러그인 적용시 호출
>     @Override
>     void apply(Project target) {
>         // 태스크 추가 정의
>         target.tasks.register("exeTask1") {
>             doLast {
>                 println "This is Customer Plug-in -exeTask1"
>             }
>         }
>         target.tasks.register("exeTask2") {
>             doLast {
>                 println "This is Customer Plug-in -exeTask2"
>             }
>         }
>     }
> }
> 
> tasks.register("myExeTask") {
>     dependsOn "exeTask1"
> 
>     doLast {
>         println "This is Customer Plug-in -myExeTask"
>     }
> }
> ```
> 
> 그레이들은 플러그인의 설정 정보를 세팅할 수 있게 관련 블록을 제공한다. 예를 들어 java 플러그인을 사용한다면
> jar 블록을 이용하여 자바와 관련된 속성을 지정할 수 있다.
> ```groovy
> apply plugin "java"
> 
> jar {
>     // java 플러그인 apply 시 자바 관련 속성 지정
>     ...
> }
> ```
>
> ```groovy
> // 사용자 정의 플러그인 적용
> apply plugin: GradleUserPlugin
> 
> // 사용자 정의 블럭을 통한 속성값 지정
> prop {
>     outPutContents("www.gradle.org", "10.1.1.152")
> }
> 
> // 사용자 정의 플러그인
> class GradleUserPlugin implements Plugin<Project> {
> 
>     // 플러그인 적용시 호출
>     @Override
>     void apply(Project target) {
>         target.extensions.create('prop', GradleProperties)
> 
>         // 태스크 추가 정의
>         target.tasks.register("exeTask1") {
>             doLast {
>                 println "${project.prop.domain}, ${project.prop.ipAddr}"
>             }
>         }
>     }
> }
> 
> class GradleProperties {
>     String domain
>     String ipAddr
> 
>     void outPutContents(domain, ipAddr) {
>         this.domain = domain
>         this.ipAddr = ipAddr
>     }
> }
> 
> tasks.register('showResult') {
>     doFirst {
>         println '========== showResult Task ========='
>     }
>     finalizedBy 'exeTask1'
> }
> ```

---

## 스프링 부트와 그레이들
### 스크립트 파일 종류
> gradle 디렉터리 하위에 다양한 스크립트 파일을 위치시킬 수 있는데 다음과 같다.
> * default.gradle: 프로젝트 공통적인 설정 정보
> * archive.gradle: Resource 자원 관리 및 아카이브 관련 설정 정보 등
> * versioning.gradle: 버전과 관련된 내용
> * maven.gradle: 프로젝트 결과물 또는 관련 라이브러리 업로드 위한 메이븐 정보
> * sonar.gradle: Sonar 접근 정보
> * environment.gradle: 환경 변수 관련 정보
>
> default.gradle 을 build.gradle 에 적용하는 방법
> ```groovy
> apply from: "./gradle/default.gradle"
> ```

---
