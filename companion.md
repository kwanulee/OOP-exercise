# 정적 멤버와 Companion Object (실습)

## 0. 시작하기 전에

이 Codelab에서는 companion object와 싱글턴 패턴을 실습해봅니다.

### 실습 준비

- 최신 버전의 JDK와 IntelliJ IDEA IDE가 설치된 컴퓨터
- 정적 멤버와 Companion Object 주제의 온라인 강의영상 시청 완료


<a name="1"></a>
## 1. Companion Object 실습 
- 학생을 나타내는 **Student** 클래스는 다음과 같은 프로퍼티를 가지고 있다고 가정한다.
	- 학생의 이름을 나타내는 **name**을 프로퍼티로 가진다.
	- 학번을 나타내는 **id**는 학생마다 고유한 값을 가진 프로퍼티이다.
-  **Student** 클래스를 구현할 때, 이름을 생성자 파라미터로 받아 들이고, 학번은 고유한 값을 가질 수 있도록 구현하시오.
	- [**힌트**] **companion object**의 멤버로 **count** 변수를 선언하고, **Student** 객체 인스턴스가 생성될 때마다 값을 증가시키고, 이를 **id**의 값으로 초기화한다.  

<!-- 정답
	```kotlin
	class Student(val name:String) {
	    val id:String = "${count++}"
	
	    companion object {
	        var count: Int = 0
	    }
	}
	```
-->
- 다음 코드를 실행하여 **Student** 객체 인스턴스가 고유한 id 값을 가지는 지를 확인해본다.

	```kotlin
	fun main() {
	    val s1 = Student("Lee")
	    val s2 = Student("Kim")
	    val s3 = Student("Park")
	
	    println("name = ${s1.name}, id = ${s1.id}")
	    println("name = ${s2.name}, id = ${s2.id}")
	    println("name = ${s3.name}, id = ${s3.id}")
	}
	```
	
	- 실행결과

		```
		name = Lee, id = 0
		name = Kim, id = 1
		name = Park, id = 2
		```


## 2. 싱글턴 실습
- **Stduent** 객체를 관리하는 **StudentManager**는 다음과 같은 메소드를 가지고 있다. 
	- **fun add(student:Student):Unit** : 파라미터로 입력된 **student** 객체를 내부 컬렉션에 등록
	- **fun display():Unit**: 내부 컬렉션에 등록된 모든 **Student** 객체 정보를 출력
- **StudentManager** 객체 인스턴스가 **싱글턴 조건** (프로그램 실행 중에 단 하나의 인스턴스으로만 존재)을 만족시키도록 다음 두 가지 방식으로 구현해 보시오.
	1. **companion object**를 이용하는 방식 
	2. **object** 키워드를 이용하는 방식
		
- 다음 코드를 실행하여 **Student** 객체 인스턴스가 고유한 id 값을 가지는 지를 확인해본다.

	```
	fun main() {
	    StudentManager.add(Student("Lee"))
	    StudentManager.add(Student("Kim"))
	    StudentManager.add(Student("Park"))
	
	    StudentManager.display()
	}
	```

	- 실행결과

		```
		name = Lee, id = 0
		name = Kim, id = 1
		name = Park, id = 2
		```
