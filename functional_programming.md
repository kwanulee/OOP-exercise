# 함수형 프로그래밍 실습

## 0. 시작하기 전에

이 Codelab에서는 함수형 프로그래밍의 기본 개념을 이해하고, 고차함수, 람다식을 이용한 프로그래밍을 실습해봅니다.

### 실습 준비

- 최신 버전의 JDK와 IntelliJ IDEA IDE가 설치된 컴퓨터
- 함수와 함수형 프로그래밍 주제의 온라인 강의영상 시청 완료

### 실습할 내용

- Kotlin에서 함수를 선언하고 호출하는 방법을 실습해봅니다.
- Kotlin에서 Lambda식으로 함수를 정의하는 방법을 실습해봅니다.
- Kotlin에서 다른 함수를 매개변수로 받아들이는 고차함수를 정의하고, 다양한 형태(call by name, call by reference, call by lambda)의 인자로 호출되는 고차함수를 실습해봅니다.
- 키보드로부터 두 정수와 연산자를 입력 받고 이를 바탕으로 사칙연산을 수행하는 코드 작성해봅니다. 

## 1. 함수 선언 및 호출

1. 다음과 같은 함수를 정의하고 이를 호출하는 Kotlin 코드로 작성하시오.
	- 함수 정의
		- 이름: *printStudentInfo*
		- 매개변수
			- nameOfCollege (String 형) - 단과대학 이름
			- nameOfMajor (String 형) - 전공이름 (트랙 및 학과) 
			- id (String 형) - 학생 아이디
			- name (String형) - 학생 이름
		- 반환값: 없음
		- 함수코드: 매개변수의 값을 화면에 출력하는 코드
	- 함수 호출
		- *printStudentInfo* 함수에 적절한 인자를 전달하여 호출
		
			```
			fun main() { 
				printStudentInfo("창의융합대학", "AI응용", "001", "이관우")
			}
			```
		
		- 출력 결과
		
			```
			단과대학 : 창의융합대학
			전공 : AI응용
			아이디 : 001
			이름 : 이관우
			```
2. 1번에서 정의한 함수에서 nameOfCollege와 nameOfMajor의 매개변수에 대해서만 다음과 같은 기본값을 설정한 후에, 매개변수 이름과 함께 함수를 호출해 봅니다. 	
	- 매개변수 기본값 설정
		- nameOfCollege 기본값: 창의융합대학
		- nameOfMajor 기본값: AI응용
	-  함수 호출
		- 함수 호출시, 매개변수 이름과 함께 다양한 방식 함수를 호출해 보고 올바른 결과가 출력되는 지  검토해 보세요
		- 함수 호출 예시
		
			```
			printStudentInfo(id = "001", name="이관우")
			printStudentInfo("IT공과대학","사물인터넷","002","홍사물")
			printStudentInfo("IT공과대학",id="003",nameOfMajor="지능시스템",name="김지능")
			printStudentInfo("IT공과대학","사이버보안",name="박보안",id="004")  
			```

## 2. 함수와 람다식
1.  다음은 하나의 정수형 매개변수를 받아 제곱을 한 값을 반환하는 square 함수를 정의하고 호출하는 코드이다.

	```
	fun square(a:Int):Int {
		return a*a
	}
	
	fun main() {
		println(square(3))
	}
	```
	- 이 squre 함수를 간략하게 표현해 보세요
	- 이 squre 함수를 주석처리한 후에 이를 람다식으로 변환하고 동일한 이름인 sqaure 변수에 할당해보세요. 동일한 수행결과가 나오나요?
2. 다음은 두개의 정수형 매개변수를 받아 두 값의 합을 반환하는 sum 함수를 함수를 정의하고 호출하는 코드이다.

	```
	fun sum(a:Int, b:Int):Int {
		return a+b
	}
	```
	- 이 sum 함수를 간략하게 표현해 보세요
	- 이 sum 함수를 주석처리한 후에 이를 람다식으로 변환하고 동일한 이름인 sum 변수에 할당해보세요. 동일한 수행결과가 나오나요?
3. 지금까지 수행한 실습코드에 다음 연산을 람다식으로 정의한 변수를 추가하고, 이를 람다식 함수로 호출하는 코드를 작성하시오. 
	- negative: 하나의 입력 매개변수 값의 부호를 바꾸는 연산
	- sub: 두개의 입력 매개변수에 대해서 첫번째 변수에서 두번째 변수의 값을 빼는 연산
	- mul: 두개의 입력 매개변수의 값을 곱하는 연산
	- div: 두개의 입력 매개변수에 대해서 첫번째 변수에서 두번째 변수의 값을 나누는 연산
	
## 3. 고차함수

1. [**고차함수 정의와 고차함수 인자로 람다식의 이름 전달**] 이전 실습문제에서 정의한 람다식을 매개변수로 받아들이는 두개의 고차함수를 정의하고, 각각의 함수를 람다식 이름을 이용하여 호출 코드를 수행해보세요.
	- applyUnaryCalculation
		- 매개변수
			- a: Int 형 값
			- op: (Int) ->Int 형식의 람다식
		- 반환값 자료형: Int 형
		- 함수 코드: 첫번째 매개변수 a의 값을 두번째 매개변수 op 람다식의 인자로 사용하여 연산한 결과를 반환
	- 함수 호출
			
		```
		val square = ... // 하나의 입력 매개변수 값을 제곱한 값을 연산하는 람다식
		val negative = ... // 하나의 입력 매개변수 값의 부호를 바꾸는 연산을 수행하는 람다식
		
		fun main() {
		    println(applyUnaryCalculation(3,square))
		    println(applyUnaryCalculation(3,negative))
		
		}
		```	
	- applyBinCalculation
		- 매개변수
			- a: Int 형 값
			- b: Int 형 값
			- op: (Int,Int) ->Int 형식의 람다식
		- 반환값 자료형: Int 형
		- 함수 코드: 첫번째 두번째 매개변수 a,b의 값을 세번째 매개변수 op 람다식의 인자로 사용하여 연산한 결과를 반환
	- 함수 호출
			
		```
		val sum = ... // 두개의 입력 매개변수에 대해서 두 변수의  값을 더하는 연산을 수행하는 람다식
		val sub = ... // 두개의 입력 매개변수에 대해서 첫번째 변수에서 두번째 변수의 값을 빼는 연산을 수행하는 람다식
		
		fun main() {
		    println(applyBinCalculation(3,2,sum))
		    println(applyBinCalculation(3,2,sub))
		
		}
		```	
	

2. [**고차함수의 인자로 다른 함수 참조 전달**] 이전 문제에서는 두개의 고차함수의 마지막 인자로 람다식을 할당한 변수 (람다식의 이름)를 전달하였는데, 이를 함수 참조로 수정하시오. 즉 실습 2.1, 2.2, 2.3에서 정의한 함수의 참조를 고차함수의 마지막 인자로 전달하도록 코드를 수정하시오.
3. [**고차함수의 인자로 람다식 자체 전달**] 이전 문제의 고차함수의 마지막 인자로 람다식 자체를 직접 전달하는 방식으로 코드를 수정하시오. 이때 아래와 같이 코드를 변형해 보세요
	- 마지막 람다식을 소괄호 밖으로 빼낼 수 있습니다. 
	- 람다식의 매개변수가 한개인 경우에는 매개변수를 생략하고 **it**으로 매개변수를 참조할 수 있습니다.

## 4. 사칙 연산 계산기
1. 키보드로부터 두 정수와 연산자를 입력 받고 이를 바탕으로 사칙연산을 수행하는 코드를 수행해 보고 이해해봅니다.

```
package prob6.domain

val sum = {a:Int, b:Int -> a+b}
val sub = {a:Int, b:Int -> a-b}
val mul = {a:Int, b:Int -> a*b}
val div = {a:Int, b:Int -> a/b}
val noop = {a:Int, b:Int -> 0}

fun applyBinOperation(a:Int, b:Int, op:(Int, Int)->Int ) : Int = op(a,b)
```

```
package prob6.ui

import prob6.domain.*

fun main() {
    print("첫 번째 정수를 입력하세요: ")
    val num1 = readLine()?.toIntOrNull()

    print("두 번째 정수를 입력하세요: ")
    val num2 = readLine()?.toIntOrNull()

    if (num1 == null || num2 == null) {
        println("올바른 정수를 입력하세요.")
        return
    }
    print("사용할 연산자를 입력하세요 (+, -, *, /): ")
    val operatorStr = readLine()
    val operator = getOperator(operatorStr)
    println(applyBinOperation(num1,num2,operator))

}

fun getOperator(str: String?) : (Int, Int)->Int {
    return when (str) {
        "+" -> sum
        "-" -> sub
        "*" -> mul
        "/" -> div
        else -> {
            println("유효하지 않은 연산자입니다.")
            noop
        }
    }
}
```
