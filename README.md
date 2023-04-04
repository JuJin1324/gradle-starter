# gradle-starter

## gradle
### 용어 정리
> 컴파일(compile): 소스 코드를 바이너리 파일로 변환하는 과정(예: .java -> .class 파일로 변경)  
> 
> 빌드(build): 프로젝트의 소스, 리소스 파일들을 컴퓨터에서 실행할 수 있는 독립적인 형태로 변환하는 과정과 그 결과  
> 빌드 과정에서 소스 코드에 대한 컴파일이 진행됨으로 컴파일은 빌드 과정 중 하나이다.  
> 
> 빌드 툴(build tool): 빌드에서는 컴파일, 테스트, 배포 등 과정이 포함될 수 있고, 빌드 과정을 도와주는 도구를 빌드 툴이라 합니다.    
> 일반적으로 빌드 툴이 제공해주는 기능으로는 다음과 같은 기능들이 있습니다.  
> 전처리(preprocessing), 컴파일(Compile), 패키징(packaging), 테스팅(testing), 배포(distribution)  
> 빌드 툴로는 Ant, Maven, Gradle 등이 있습니다.   

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
> PC 에 Gradle 이 설치되어 있지 않은 경우 다음과 같이 테스크를 실행한다: `gradlew build`  
> 
> settings.gradle  
> 프로젝트에 대한 설정 정보를 작성한 파일.  
> MSA(Micro Service Architecture) 구조로 프로젝트를 구성할 경우 root 프로젝트 하위로 모듈을 추가할 경우 settings.gradle 파일에 모듈을 추가한다고 명시한다.

### 참조사이트
> [Gradle 기본사용법](https://velog.io/@franc/Gradle-%EA%B8%B0%EB%B3%B8%EC%82%AC%EC%9A%A9%EB%B2%95)

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
> task <테스크 명> {
>   // 내용
> }
> ```
> 예시: 'hello world' 를 화면에 표시하는 테스크 'hello'
> ```groovy
> task hello {
>     println 'Hello world'
> }
> ```
> 터미널에서 `gradle hello` 를 입력하면 Hello world 가 화면에 표시된다.

### doFirst 와 doLast 
> 태스크 내부에서 우선순위 블록을 만들고자 할 때 사용한다.
> ```groovy
> task <테스크 명> {
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
> task <테스크 명> {
>   def <변수명> = <변수명>   // 변수 값이 문자인 경우
>   def <변수명> = <변수명>.toInteger()   // 변수 값이 숫자인 경우
> }
> ```
> 터미널: `gradle <테스크 명> -P<변수명1>=<변수값1> -P<변수명2>=<변수값2>...`
> 
> 예시
> ```groovy
> task calc {
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
> task hello {
>   ext.myProperty = 'hello property'
> }
> 
> task helloPrint {
>   doLast {
>       println hello.myProperty
>   }
> }
> ```

### 다른 task 호출
> ```groovy
> task <태스크 명> {
>   tasks.<다른 테스크 명>
> }
> 
> task <다른 테스크 명> {
>   // 내용
> }
> ```
> 예시
> ```groovy
> task hello {
>   println 'Hello gradle'
>   tasks.otherTask
> }
> 
> task otherTask {
>   println 'do other task'
> }
> ```

### task chaining
> dependsOn 은 특정 Task 실행 이전에 수행되도록 만들고, finalizedBy 는 특정 Task 실행 이후 수행되도록 만드는 Task 객체의 프로퍼티이다.  
> 단 해당 Task 의 doFirst 혹은 doLast 블록에 있는 내용이 dependsOn 및 finalizedBy 에 맞게 실행된다.  
> ```groovy
> task <태스크 명> {
>   // 내용
> }
> 
> task <다른 태스크 명1> {
>   // 내용
> }
> 
> > task <다른 태스크 명1> {
>   // 내용
> }
> 
> <태스크 명>.dependsOn <다른 태스크 명1>
> <태스크 명>.finalizedBy <다른 태스크 명2>
> ```
> 예시
> ```groovy
> task hello(dependsOn: 'otherTask') {
>   println 'Hello gradle'
> }
> 
> task otherTask {
>   println 'Other task'
> }
> ```

### type: Copy
> TODO

### tasks.named
> TODO

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

## buildscript
### ext 
> TODO

### dependencies
> TODO

---

## configurations
### compileOnly
> TODO

### all
> TODO

### extendsFrom
> TODO

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
> bootJar {
>     layered
>     dependsOn asciidoctor
>     copy {
>         from '${asciidoctor.outputDir}'
>         into 'BOOT-INF/classes/static/docs'
>     }
>     finalizedBy 'copyDocument'
> }
> 
> task copyDocument(type: Copy) {
>     dependsOn bootJar
>     from file("src/docs/asciidoc")
>     into file("src/main/resources/static/docs")
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
> asciidoctor {
>     inputs.dir snippetsDir
>     dependsOn test
> }
> 
> asciidoctor.doFirst {
>     delete file('src/main/resources/static/docs')
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
> group: TODO  
> version: TODO  
> sourceCompatibility: TODO
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

---

## Deploy
### TODO
> TODO
