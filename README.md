# gradle-starter

### spring dependency 에서 로깅 라이브러리 제거
> ```groovy
> configurations {
>     ...
>     all {
>         exclude module: 'spring-boot-starter-logging'
>     }
> }
> ```

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

## Deploy
### AWS S3
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

## Test
### lombok
> Test 파일에서 lombok 을 사용하는 경우 다음 dependency 추가   
> ```groovy
> dependencies {
>     ...
>     testCompileOnly 'org.projectlombok:lombok'
>     testAnnotationProcessor 'org.projectlombok:lombok' 
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

