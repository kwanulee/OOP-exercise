# Kotlin/Java 시작하기 실습

## 0. 시작하기 전에

이 Codelab에서는 IntelliJ IDEA IDE를 사용하여 Kotlin 및 Java 언어로 첫 프로그램을 작성해 보고, IntelliJ IDEA IDE의 기초적인 유용한 기능을 활용해봅니다.

### 실습 준비

- 최신 버전의 JDK와 IntelliJ IDEA IDE가 설치된 컴퓨터

### 학습할 내용

- IntelliJ IDEA IDE환경에서 Kotlin 및 Java 프로젝트를 생성하는 방법을 알아봅니다.
- 메시지를 표시하는 간단한 Kotlin/Java 프로그램을 생성, 변경, 이해, 실행하는 방법을 알아봅니다.
- 기존 Kotline 및 Java 프로젝트를 여는 방법을 알아봅니다.
- 기타 IntellJ IDEA IDE 환경의 유용한 기능에 대해서 알아봅니다. 

## 1. Java 및 Kotlin 프로젝트 생성하기

1. 다음과 같은 설정의 Java 프로젝트와 Java Class를 생성하고, Java 프로젝트를 실행해보세요
   
   - Java 프로젝트 
     
     - 이름: *FirstJavaApplication*
     - 위치: 사용자 홈 디렉토리 하위의 *OOPWorkspace* 폴더
   
   - Java Class 
     
     - 위치: ~/OOPWorksapce/FirstJavaApplication/src/HelloJava.java
       
       - 코드 :
         
         ```java
         public class HelloJava {
                 public static void main(String[] args) {
                     System.out.println("Hello");
                     System.out.println("This is my First Java Application");
                 }
         }
         ```
   
   - 실행결과:
     
     ```
     Hello
     This is my First Java Application
     ```

2. 다음과 같은 설정의 Kotlin 프로젝트와 Kotlin 파일를 생성하고, Kotlin 프로젝트를 실행해보세요
   
   - Kotlin 프로젝트 
     
     - 이름: *FirstKotlinApplication*
     - 위치: 사용자 홈 디렉토리 하위의 *OOPWorkspace* 폴더
   
   - Kotlin 파일 
     
     - 위치:~/OOPWorksapce/FirstKotlinApplication/src/main/kotlin/HelloKotlin.kt
       
       - 코드 :
         
         ```kotlin
         fun main() {
                 println("Hello");
                 println("This is my First Kotlin Application");
         }
         ```
   
   - 실행결과:
     
     ```
     Hello
     This is my First Kotlin Application
     ```

## 2. 명령행 메시지를 함께 출력하는 프로그램 작성하기

앞서 작성한 프로그램에 대해서, 프로그램 실행 시에 프로그램 인자(Program Arguments)로 받은 결과를 출력하도록 수정해 보고, 이를 테스트해 보세요.

### 2.1 Java 프로그램 사례

- 코드:
  
  ```java
  public class HelloJava {
      public static void main(String[] args) {
           System.out.println("Hello");
           System.out.println(args[0]);
          System.out.println("This is my First Java Application");
       }
  }
  ```

- 실행 방법
  
  - IntelliJ IDEA IDE 상단 아이콘 메뉴에서 **Run with Parameters**를 선택한 후, **Program arguments** 란에 인자를 입력한 후, **[OK]** 를  눌러 실행한다.
    
      ![](D:\Dropbox\2023-2\OOP\exercise\figures\run_with_parameters.png)

### 2.2 Kotlin 프로그램 사례

- 코드:
  
  ```kotlin
  fun main(args:Array<String>) {
      println("Hello")
      println(args[0])
      println("This is my First Kotlin Application")
  }
  ```

- 실행 방법
  
  - IntelliJ IDEA IDE 상단 아이콘 메뉴에서 **Run with Parameters**를 선택한 후, **Program arguments** 란에 인자를 입력한 후,  **[OK]** 를  눌러 실행한다.
    
      ![](D:\Dropbox\2023-2\OOP\exercise\figures\run_with_parameters.png)

## 3. 기존 예제 프로젝트를 여는 방법

1. 다음 사이트에 접속하여 **Code** 부분을 선택한 후,  zip 파일을 다운 로드 받고, 압축을 해제합니다.
   - https://github.com/kwanulee/KotlinJavaExamples.git
2. IntelliJ IDEA IDE의 **[File > Open]** 메뉴를 선택하고, 열고자 하는 예제 프로젝트 폴더를 선택한 후 **Open** 버튼을 클릭하면 선택된 예제 프로젝트가 빌드됩니다.

## 4. IntelliJ IDEA IDE의 유용한 기능

- main함수 시그니처 생성 기능
  
  - 에디터 창에서 다음 문자열을 입력한 후 엔터를 쳐보자
    - **psvm** 혹은 **main**
      - Kotlin 프로그램 작성시: **fun main()** 완성                
      - Java 프로그램 작성시: **public static void main(String[] args)** 완성  
    - **maina**
      - Kotlin 프로그램 작성시: **fun main(args: Array<String>)** 완성  

- java 프로그램 코드를 Kotlin 코드로 변환하기
  
  - Kotlin 파일 에디팅시에, Java 프로그램 코드를 복사하여 붙여넣으면, 자동으로 Kotlin 코드로 변환됨

- 코드 정리하기
  
  - 왼쪽 Project 창에서 소스 파일을 선택한후, 오른쪽 마우스를 클릭하여 **Reformat Code** 메뉴를 선택하면 선택된 소스 파일의 코드의 들여쓰기가 정리됨
