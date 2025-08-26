# Kotlin/Java 프로그래밍 기초 1 실습

## 0. 시작하기 전에

이 Codelab에서는 Kotlin 및 Java 프로젝트의 구조를 이해하고, 프로그램의 기본 개념인  변수, 자료형, 연산자를 활용하여 기초적인 프로그램을 실습해봅니다.

### 실습 준비

- 최신 버전의 JDK와 IntelliJ IDEA IDE가 설치된 컴퓨터
- 패키지, 변수와 자료형, 연산자 주제의 온라인 강의영상 시청 완료

### 실습할 내용

- IntelliJ IDEA IDE환경에서 Kotlin 및 Java 프로젝트를 생성하고, 패키지를 생성하여 파일 및 클래스를 구조화하는 방법을 실습해봅니다.
- Kotlin 과 Java 언어에서 다양한 자료형으로 변수를 선언하고 초기화하는 방법을 실습해봅니다.
- Kotlin 과 Java 언어에서 변수의 자료형을 검사하고 변환하는 방법을 실습해봅니다.
- Kotlin 과 Java 언어에서 다양한 연산자를 활용하여 프로그램의 결과를 예측해 봅시다. 

## 1. Java 및 Kotlin 패키지 생성하기

1. 다음과 같은 설정의 Kotlin 프로젝트, 패키지, Kotlin 파일을 생성하고, IntelliJ IDEA IDE의 *Project File* 뷰를 통해 디렉토리, 패키지, 파일의 구조를 확인해보세요. 
	- Kotlin 프로젝트  
		- 이름: PackageCreation
	- 패키지
		- 이름: com.practice.oop.data     
	- Kotlin 클래스/파일
		- 이름 : Student.kt
		- 코드 
			```kotlin
			package com.practice.oop.data
     
			class Student(val id: String, val name: String)
			```

2. 앞서 생성한 Kotlin 프로젝트에 다음과 같은 설정의 패키지와 Kotlin 파일을 생성하면, Student 부분에서 오류 메시지가 표시된다. 이를 해결하기 위해서 앞서 정의한 Student 클래스를 import한 후에, Kotlin 파일을 실행하여 아래와 같은 결과를 얻으시오.
 	- 패키지 
 		- 이름: com.practice.oop.view    
	- Kotlin 파일 
		- 이름: DisplayInformation.kt
		- 코드
		
			``` kotlin
			
			package com.practice.oop.view
			
			fun main() {
				val std1 = Student("AI001","Kildong")
       
			     println(std1.id)
			     println(std1.name)         
			}
			```
	- 실행결과:
		```
		AI001
		Kildong
		```

3. 1,2번에서 진행된 내용을 Java 프로젝트로 만들어서 진행해 보세요. 

## 2. 변수 선언과 초기화

1. 다음 Kotlin 코드에서 변수 선언 및 초기화에 대해서 잘못된 부분이나 사용이 적절하지 않는 부분을 지적하고 이를 적절히 수정하시오.
   
   ```kotlin
   fun main() { 
       val username = 123
       var secondNumber : int = 30
       username = "kwanwoo"
       val exp01 = 3.14
       var _011 = 4    
   }
   ```

2. 변수의 값이나 표현식을 문자열 안에 넣어 출력하려면 \$ 기호와 함께 변수나 표현식을 사용하면됩니다. 
   
   - 예제
     
     ```kotlin
     val a = 1
     val b = 3
     val s1 = "a is $a"        // $a는 a의 값을 문자열로 변환
     val s2 = "b is $b"        // $b는 b의 값을 문자열로 변환
     val s3 = "a+b is ${a+b}"  // ${a+b} 는 a+b의 수식 값을 문자열로 변환
     
     // \"는 큰따옴포(")을 문자열의 종료 문자로 인지하지 않게하여 문자열 안에 포함시킴
     println("s1 = \"$s1\", s2 = \"$s2\", s3 = \"$s3\"")  
     ```
   
   - 문제 : 다음과 같은 문자열이 출력되도록 코드를 작성하시오.
     
     ```
     "hello", I have $15.
     ```

## 3. 연습문제

1. 변수 input에는 임의의 4자리 정수가 할당된다고 가정한다. 이 변수의 4자리 정수 값을 예시된 형식으로 출력하는 Kotlin 코드를 작성하시오.
	- 코드
     
		```kotlin
		fun main() {
			val input = 4938
     
			// 이 부분에 코드를 완성 하시오
     
		}
		```
	- 출력결과
     
		```
		₩4,983
		```
	- 힌트
		- 자리수별로 값을 구하여 변수에 저장한 후에, 예시된 형식에 맞추어 변수의 값을 출력합니다.
		- 이때, ${변수}와 \(이스케이프 문자)를 활용합니다.

2. 1번 문제에 대한 Java 코드를 작성하시오.

3. 4개의 변수 g1, g2, g3, g4에 0~100 사이의 임의의 정수값이 지정된다고 가정한다. 각 변수의 값, 변수 값의 총합, 변수 값의 평균(실수 값으로 표현되어야 함)을 각각 다음 형식으로 출력하는 코드를 작성하시오.
   - 코드
     ```kotlin
     fun main() {
         val g1 = 78
         val g2 = 90
         val g3 = 84
         val g4 = 74
     
         // 이 부분에 코드를 완성 하시오
     
     }
     ```
   - 출력결과 (예시)
     
     ```
     g1 = 78
     g2 = 90
     g3 = 84
     g4 = 74
     
     총합 = 326
     평균 = 81.5
     ```
4. 3번 문제에 대한 Java 코드를 작성하시오
