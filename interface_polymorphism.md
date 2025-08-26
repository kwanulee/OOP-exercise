# 인터페이스와 다형성 (실습)

지난주 실습과제 클래스 상속에서 정의한 Shape, Rectangle, Circle 클래스를 바탕으로 다음의 내용을 구현해 보자.

<a name="1"></a>
### 1. 메소드 오버라이딩 (실습)

1. **Shape** 클래스의 아래와 같이 수정하시오.
	- **Any** 클래스의 **fun equals(other: Any?):Boolean** 메소드를 재정의 한다.
		- 파라미터로 입력된 Any 객체 other이 Shape 타입의 객체인지 판별 (is 연산자 이용)
		- Any 객체 other이 Shape 타입의 객체인 경우, 객체변수 other로 참조될 수 있는 Shape 타입의 프로퍼티 x, y의 값과 현재 Shape 객체의 프러퍼티 수 x, y의 값을 각각 비교하여 모두 참이면 true를 반환, 그렇지 않으면 false를 반환

2. **Rectangle** 클래스와 **Circle** 클래스에서 **Shape** 클래스에서 재정의된 **fun equals(other: Any?):Boolean**를 확장하여 재정의한다.
	- **Rectangle** 클래스의 **fun equals(other: Any?):Boolean**:
		- 파라미터로 입력된 Any 객체 other이 Rectangle 타입의 객체인지 판별 (is 연산자 이용)
		- Any 객체 other이 Rectangle 타입의 객체인 경우, super.equals(other) 의 결과와 함께, 객체변수 other로 참조될 수 있는 Rectangle 타입의 프로퍼티 width, height의 값과 현재 Rectangle 객체의 프로퍼티 width, height의 값을 각각 비교하여 모두 참이면 true를 반환, 그렇지 않으면 false를 반환
	- **Circle** 클래스의 **fun equals(other: Any?):Boolean**:
		- 앞의 **Rectangle** 클래스의 **equals()** 메소드 구현과 같은 방식

- 이상을 테스트 하기 위한 코드는 다음과 같다.


	```kotlin
	fun main() {
	    val r1 = Rectangle(1, 2, 3, 4)
	    val r2 = Rectangle(2, 3, 4, 5)
	    val r3 = Rectangle(1, 2, 3, 4)
	
	    r1.displayRectangle()
	    r2.displayRectangle()
	    println("두 Rectangle 객체는 동일한가? " + r1.equals(r2))
	    println()
	    r1.displayRectangle()
	    r3.displayRectangle()
	    println("두 Rectangle 객체는 동일한가? " + r1.equals(r3))
	    println()
	
	    val c1 = Circle(3, 4, 5)
	    val c2 = Circle(4, 5, 6)
	    val c3 = Circle(4, 5, 6)
	
	    c1.displayCircle()
	    c2.displayCircle()
	    println("두 Cirlce 객체는 동일한가? " + c1.equals(c2))
	    println()
	
	    c2.displayCircle()
	    c3.displayCircle()
	    println("두 Cirlce 객체는 동일한가? " + c2.equals(c3))
	    println()
	}
	```


- 실행결과

	```
	[Rectangle] x=1, y=2, width=3, height=4 
	[Rectangle] x=2, y=3, width=4, height=5 
	두 Rectangle 객체는 동일한가? false
	
	[Rectangle] x=1, y=2, width=3, height=4 
	[Rectangle] x=1, y=2, width=3, height=4 
	두 Rectangle 객체는 동일한가? true
	
	[Circle] x=3, y=4,radius=5
	[Circle] x=4, y=5,radius=6
	두 Cirlce 객체는 동일한가? false
	
	[Circle] x=4, y=5,radius=6
	[Circle] x=4, y=5,radius=6
	두 Cirlce 객체는 동일한가? true
	
	```

---
<a name="2"></a>
### 2. 메소드 오버라이딩 (실습)

1. **Shape** 클래스의 아래와 같이 수정하시오.
	- **Any** 클래스의 **fun toString():String** 메소드를 재정의 한다.
		- 프로퍼티 x, y의 값을 문자열로 반환 (문자열 형식은 자유롭게 정의 가능) 

2. **Rectangle** 클래스와 **Circle** 클래스에서 **Shape** 클래스에서 재정의된 **fun toString():String**를 확장하여 재정의한다.
	- **Rectangle** 클래스의 **fun toString():String**:
		- super.toString() 반환값과 프로퍼티 width, height의 값을 문자열로 결합하여 반환
	- **Circle** 클래스의 **fun toString():String**:
		- 이전 **Rectangle** 클래스의 **toString()** 메소드 구현과 같은 방식
3. **Rectangle** 클래스와 **Circle** 클래스의 **displayRectangle()**, **displayCircle()** 구현 변경
	-  **toString()** 메소드 활용

- 이상을 테스트 하기 위한 코드는 다음과 같다.


	```kotlin
	fun main() {
	    val r1 = Rectangle(1, 2, 3, 4)
	    val r2 = Rectangle(2, 3, 4, 5)
	    val r3 = Rectangle(1, 2, 3, 4)
	
	    r1.displayRectangle()
	    r2.displayRectangle()
	    println("두 Rectangle 객체는 동일한가? " + r1.equals(r2))
	    println()
	    r1.displayRectangle()
	    r3.displayRectangle()
	    println("두 Rectangle 객체는 동일한가? " + r1.equals(r3))
	    println()
	
	    val c1 = Circle(3, 4, 5)
	    val c2 = Circle(4, 5, 6)
	    val c3 = Circle(4, 5, 6)
	
	    c1.displayCircle()
	    c2.displayCircle()
	    println("두 Cirlce 객체는 동일한가? " + c1.equals(c2))
	    println()
	
	    c2.displayCircle()
	    c3.displayCircle()
	    println("두 Cirlce 객체는 동일한가? " + c2.equals(c3))
	    println()
	}
	```


- 실행결과

	```
	[Rectangle] x=1, y=2, width=3, height=4 
	[Rectangle] x=2, y=3, width=4, height=5 
	두 Rectangle 객체는 동일한가? false
	
	[Rectangle] x=1, y=2, width=3, height=4 
	[Rectangle] x=1, y=2, width=3, height=4 
	두 Rectangle 객체는 동일한가? true
	
	[Circle] x=3, y=4,radius=5
	[Circle] x=4, y=5,radius=6
	두 Cirlce 객체는 동일한가? false
	
	[Circle] x=4, y=5,radius=6
	[Circle] x=4, y=5,radius=6
	두 Cirlce 객체는 동일한가? true
	
	```
	
---
<a name="3"></a>
### 3. 추상클래스 (실습)

- **Shape** 클래스를 추상클래스로 변경하시오.
	- 추상메소드  **abstract fun display()** 추가

- **Rectanlge** 클래스
	- 추상메소드 **abstract fun display()**를 재정의
- **Circle** 클래스
	- 추상메소드 **abstract fun display()**를 재정의
			
- display() 메소드 구현
	- **public void display()**
		- Shape 배열에서 저장된 모든 도형 객체를 화면에 출력
			- 각 도형이 가지고 있는 정보를 출력

- 이상을 테스트 하기 위한 코드는 다음과 같다.

	```kotlin
	fun main() {
	    val r1 = Rectangle(1, 2, 3, 4)
	    val r2 = Rectangle(2, 3, 4, 5)
	    val r3 = Rectangle(1, 2, 3, 4)
	
	    val c1 = Circle(3, 4, 5)
	    val c2 = Circle(4, 5, 6)
	    val c3 = Circle(4, 5, 6)
	
	    val shapes: Array<Shape> = arrayOf(r1, r2, r3, c1, c2, c3)
	    for (s in shapes) {
	        s.display()
	    }
	}
	```

- 실행결과

	```
	[Rectangle] x=1, y=2, width=3, height=4
	[Rectangle] x=2, y=3, width=4, height=5
	[Rectangle] x=1, y=2, width=3, height=4
	[Circle] x=3, y=4, radius=5
	[Circle] x=4, y=5, radius=6
	[Circle] x=4, y=5, radius=6
	```

<a name="4"></a>
### 4. 인터페이스 (실습과제)
- 추상클래스로 정의된 3번 문제의 결과를 인터페이스 방식으로 변경해서 동일한 출력결과가 나오도록 변경해 보세요
- 실습 결과를 바탕으로 추상클래스와 인터페이스의 차이점을 설명해 보세요

