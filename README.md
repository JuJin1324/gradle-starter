# gradle-starter

## gradle
### 개요
> JVM 빌드 도구.

### 설치
> macOS: `brew install gradle`    
> 
> 버전 확인: `gradle -version`  

### 프로젝트 생성
> 1.Gradle 프로젝트를 생성할 디렉터리로 이동.  
> 2.`mkdir <프로젝트 명>` 명령어로 프로젝트 디렉터리 생성 후 해당 디렉터리로 이동.  
> 3.`gradle init` 명령어 실행.  
> 3-1.java application 으로 미리 정해서 생성하려면 다음 명령어 실행: `gradle init --type java-application`

### build.gradle
> Gradle 프로젝트에서 의존성(Dependencies) 관리 및 플러그인 등의 설정 관리 파일.

### 프로젝트 task 확인
> 1.Gradle 프로젝트 디렉터리 안으로 이동.  
> 2.`gradle tasks` 명령어 실행.

### 프로젝트 빌드
> `gradle build` 명령어를 통해서 실행한다.  
> build.gradle 에 `apply plugin: 'java'` 가 추가된 경우 .jar 파일로 패키징까지 해준다.  
> 컴파일된 파일들은 app/build 디렉터리 안에 생성되며, .jar 파일은 `build/libs` 에 패키징된다.  

### 프로젝트 실행
> 일단 Java 애플리케이션인 경우 `gradle run` 으로 실행하며, 스프링부트인 경우 `gradle bootRun` 을 통해서 앱을 구동한다.  

### 프로젝트 패키징
> `gradle jar` 명령어로 프로젝트를 .jar 파일로 패키징하며, build.gradle 파일에 `apply plugin: 'java'` 가 추가된 경우 `gradle build` 로 
> 패키징까지 할 수 있다.  

### 프로젝트 클린
> `gradle clean` 을 통해서 app 밑에 build 디렉터리를 제거하여, 빌드 이전 상태로 되돌린다.  

### gradle-wrapper
> 새로운 환경에서 gradle 설치 없이 gradle 을 사용할 수 있게 하기위해 gradle 프로젝트 생성시 프로젝트 안에 포함되어 있다.  
> 사용법은 기존 `gradle <Task 명>` 에서 `gradlew <Task 명>` 로 사용하면 된다. 

### 참조사이트
> [Gradle 기본사용법](https://velog.io/@franc/Gradle-%EA%B8%B0%EB%B3%B8%EC%82%AC%EC%9A%A9%EB%B2%95)

---

## Task
### 커스텀 테스크
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

## 라이브러리 설정
### querydsl
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

### Spring Rest Doc
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

### Deploy - AWS S3
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

---

## Dependency
### Lombok Test Dependency
> Test 파일에서 lombok 을 사용하는 경우 다음 dependency 추가
> ```groovy
> dependencies {
>     ...
>     testCompileOnly 'org.projectlombok:lombok'
>     testAnnotationProcessor 'org.projectlombok:lombok' 
> }
> ```

---

## spring
### spring dependency 에서 로깅 라이브러리 제거
> ```groovy
> configurations {
>     ...
>     all {
>         exclude module: 'spring-boot-starter-logging'
>     }
> }
> ```
