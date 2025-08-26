# 제네릭과 배열 (실습)

## 0. 시작하기 전에

이 Codelab에서는 제네릭과 배열을 이용한 객체지향 프로그래밍을 실습해봅니다.

### 실습 준비

- 최신 버전의 JDK와 IntelliJ IDEA IDE가 설치된 컴퓨터
- 제네릭과 배열 주제의 온라인 강의영상 시청 완료

### 실습할 내용

- Kotlin에서 배열을 생성하고 배열에 객체를 저장 방법을 실습해봅니다.
- Kotlin에서 검색 조건에 따라 배열을 탐색하여 검색 조건과 일치하는 배열 항목을 반환하는 코드를 작성해 본다. 

<a name="1"></a>
### 1. 배열 생성 및 객체 저장 (실습)

1. 이름과 전화번호에 해당되는 name과 tel 프로퍼티를 가진 **Phone** 클래스를 정의하시오. 
	- **Phone** 객체간의 동일성 판단을 위해서 **Any** 클래스의 **fun equals(other: Any?):Boolean**를 재정의하시오
	
2. **Phone**객체를 내부에서 배열로 저장하는 **PhoneManager** 클래스를 정의하시오. **PhoneManager** 클래스의 내부 멤버는 다음과 같다. 
	- **phoneArray**: **Phone** 객체 배열 변수 (private 접근지정자)
	- **count** : **phoneArray** 배열에 저장된 **Phone** 객체의 수를 저장하는 Int형 변수 (private 접근지정자)
	- 생성자: **phoneArray**와  **count** 초기화
	- **fun add(phone:Phone): Unit** : 파라미터로 주어진 phone 객체를 **phoneArray** 배열에 저장
		- 단, 동일한  **Phone** 객체가 이미 배열에 저장되어 있으면 저장하지 않아야 한다.
	- **fun display(): Unit** : **phoneArray** 배열에 저장된 **Phone**객체의 내용을 이름을 기준으로 1차 정렬하고 전화번호를 기준으로 2차 정렬하여 출력한다.

- 이상을 테스트 하기 위한 코드는 다음과 같다.

	
	```kotlin
	fun main() {
	    val manager = PhoneManager()
	    print("인원수>>")
	    val count = readln().toInt()
	    for (i in 1..count) {
	        print("이름 >>")
	        val name = readln()
	        print("전화번호 >>")
	        val tel = readln()
	        manager.add(Phone(name, tel))
	    }
	    println("저장되었습니다.")
	    manager.display()
	}
	```


- 실행결과

	```
	인원수>>5
	이름 >>lee
	전화번호 >>123
	이름 >>kim
	전화번호 >>234
	이름 >>lee
	전화번호 >>111
	이름 >>kim
	전화번호 >>234
	이름 >>kang
	전화번호 >>231
	저장되었습니다.
	name:=kang, tel:=231
	name:=kim, tel:=234
	name:=lee, tel:=111
	name:=lee, tel:=123
	```

---
<a name="2"></a>
### 2. 배열 탐색 (실습)
- **PhoneManager** 클래스에 다음 메소드를 추가하시오
	- **fun find(name:String):Array\<Phone\>**: 인자로 주어진 name과 일치하는 모든 **Phone**객체를 포함한 Array<Phone> 배열을 반환한다. 

- 이상을 테스트 하기 위한 코드는 다음과 같다.

	```kotlin
	fun main() {
	    val manager = PhoneManager()
	    print("인원수>>")
	    val count = readln().toInt()
	    for (i in 1..count) {
	        print("이름 >>")
	        val name = readln()
	        print("전화번호 >>")
	        val tel = readln()
	        manager.add(Phone(name,tel))
	    }
	    println("저장되었습니다.")
	    manager.display()
	    println()
	    do {
	        print("검색할 이름>>")
	        val sName = readln()
	        if (sName.equals("exit"))
	            break;
	        val result: Array<Phone?> = manager.find(sName)
	        if (result != null) {
	            result.forEach {
	                println("${sName}의 번호는 ${it?.tel} 입니다.")
	            }
	        } else
	            println("${sName}는 등록되지 않았습니다.")
	    } while(true)
	}
	```

- 실행결과

	```
	인원수>>5
	이름 >>lee
	전화번호 >>123
	이름 >>kim
	전화번호 >>234
	이름 >>lee
	전화번호 >>111
	이름 >>kim
	전화번호 >>234
	이름 >>kang
	전화번호 >>231
	저장되었습니다.
	name:=kang, tel:=231
	name:=kim, tel:=234
	name:=lee, tel:=111
	name:=lee, tel:=123
	
	검색할 이름>>kim
	kim의 번호는 234 입니다.
	검색할 이름>>lee
	lee의 번호는 123 입니다.
	lee의 번호는 111 입니다.
	검색할 이름>>exit
	```

