# 입출력 스트림과 파일 (실습)

## 0. 시작하기 전에

이 Codelab에서는 객체를 파일에 저장하는 방법을 실습해봅니다.

### 실습 준비

- 최신 버전의 JDK와 IntelliJ IDEA IDE가 설치된 컴퓨터
- 파일과 입출력 스트림 주제의 온라인 강의영상 시청 완료


<a name="1"></a>
## 1. 객체를 파일에 저장하고 읽기

- 다음의 정보를 프로퍼티로 가지는 Student 클래스를 data 클래스 정의하시오
	- 학번(String), 이름(String), 학과/트랙(String), 나이(int)
	- 데이터 클래스는 toString(), hashCode(), equals(), copy()메소드를 자동으로 만들어주는 클래스입니다.

	``` 	
	data class Student (
	     val id: String,
	     val name: String,
	     val dept: String,
	     val age: Int
	)
	```
	
- 객체를 파일에 저장하고 읽는 방법 두 가지를 살펴본다.
	1. **ObjectOutputStream**과 **ObjectInputStream**을 사용
	2. **구글의 Gson 라이브러리** 사용

### 1. **ObjectOutputStream**과 **ObjectInputStream**을 사용
1. 저장하려는 객체의 클래스 정의에서 java.io.Serializable 인터페이스 구현
2. 객체를 저장하기 위해서, **ObjectOutputStream**의 **writeObject()** 메소드 사용
3. 객체를 읽기 위해서, **ObjectInputStream**의 **readObject()** 메소드 사용

- 전체코드

	```
	import java.io.File
	import java.io.ObjectInputStream
	import java.io.ObjectOutputStream
	import java.io.Serializable
	
	data class Student (
	    val id: String,
	    val name: String,
	    val dept: String,
	    val age: Int
	) : Serializable    // 직렬화가능 선언
	
	fun main() {
	    val student = Student("100", "Lee", "사물인터넷", 21)
	
	    //직렬화
	    ObjectOutputStream(File("Output.txt").outputStream())
	                    .use { it.writeObject(student)}
	
	    //역직렬화
	    val result = ObjectInputStream(File("Output.txt").inputStream())
	                    .use { it.readObject()}
	
	    println(result)
	}
	```


### 2. **구글의 Gson 라이브러리** 사용
0. **프로젝트 설정**
	1. **IntelliJ IDEA IDE**의 **File - Project Structure** 메뉴 선택
	2. **Proejct Settings**의 **Libraries** 선택
	3. **+** (New Project Library) 클릭후, **From MAVEN...* 선택
	4. 검색창에 *gson* 입력후 검색 버튼 클릭
	5. 검색 결과 중에 *com.google.code.gson:gson:2.10.1* 선택
	6. **OK** 클릭
- 객체를 Json 문자열로 변환하기 위해서, **Gson**의 **toJson()** 사용
- Json 문자열을 텍스트 파일에 저장하기 위해서 **File**의 **writeText()** 사용
-  텍스트 파일에서 저장된 Json 문자열을 읽기 위해서 **File**의 **readText()** 사용
- Json 문자열로부터 객체를 얻기 위해서. **Gson**의 **fromJson()** 사용

- 전체코드

	```
	package problem2
	
	import com.google.gson.Gson
	import java.io.File
	import java.io.ObjectInputStream
	import java.io.ObjectOutputStream
	import java.io.Serializable
	
	data class Student (
	    val id: String,
	    val name: String,
	    val dept: String,
	    val age: Int
	)
	
	fun main() {
	    val student = Student("100", "Lee", "사물인터넷", 21)
	
	    // 2. 객체를 Json 문자열로 변환
	    val jsonString = Gson().toJson(student)
	
	    // 3. Json 문자열을 텍스트 파일에 저장
	    File("output.txt").writeText(jsonString)
	
	    // 4. 텍스트 파일에서 저장된 Json 문자열을 읽기
	    val resultStr = File("output.txt").readText()
	
	    // 5. Json 문자열로부터 객체를 얻기
	    println(Gson().fromJson(resultStr, Student::class.java))
	}
	```

## 2. 실습문제	
- Student 배열 객체인 students가 아래와 같이 초기화 되어 있을 경우에, 이를 파일에 저장하는 함수와 파일로부터 저장된 정보를 읽어와 Student 배열 객체를 재구성하여 반환하는 함수를 각각 구현하시오.
	- Student 클래스는 문제1의 정의를 따른다. 

	```
	fun main() {
	    var students = arrayOf(
	        Student("100", "Lee", "사물인터넷", 21),
	        Student("101", "Kim", "지능시스템", 21),
	        Student("102", "Park", "사이버보안", 24),
	        Student("111", "Kwon", "AI응용", 21),
	    )
	
	    saveDataToFile(students, "output.txt")
	    students = loadDataFromFile("output.txt")
	    students.forEach { println("$it") }
	
	    saveObjectToFile(students, "output.dat")
	    students = loadObjectFromFile("output.dat")
	    students.forEach { println("$it") }
	}
	```

- fun loadDataFromFile(path: String): Array\<Student> {...}

- fun saveDataToFile(students: Array\<Student>, path: String) {...}

- fun saveObjectToFile(students: Array\<Student>, path: String) {...}

- fun loadObjectFromFile(path: String):Array\<Student> {...}
 
