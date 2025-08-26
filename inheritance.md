# 클래스 상속 실습

## 0. 시작하기 전에

이 Codelab에서는 클래스 상속의 기본 개념을 이해하고, Kotlin에서의 클래스 상속을 정의하고, 상속관계에 있는 클래스에서 생성자를 정의하는 방법을 실습해 봅니다. 또한 업캐스팅과 다운캐스팅의 개념을 이해하고 실습해봅니다.

### 실습 준비

- 최신 버전의 JDK와 IntelliJ IDEA IDE가 설치된 컴퓨터
- 클래스 상속 주제의 온라인 강의영상 시청 완료

### 실습할 내용
- Kotlin에서 클래스 상속을 정의하는 다양한 방법을 실습해봅니다.
- 업캐스팅과 다운캐스팅의 개념을 실습해봅니다.

## 1. 다양한 도형 클래스 정의
1. 다음과 같은 멤버를 가지는 직사각형을 표현하는 **Rectangle** 클래스를 정의하시오.
	- **private** 가시성을 가지는 int 타입의 x, y, width, height 프로퍼티: 사각형의 기준점(x,y)과 너비(width)와 높이(height)를 나타냄
	-  **displayRectangle()** 메소드: 프로퍼티의 값을 다음과 같은 형식으로 화면에 출력
		
		```
		[Rectangle] x=1, y=2, width=3, height=4 
		```
2. 다음과 같은 멤버를 가지는 원을 표현하는 **Circle** 클래스를 정의하시오.
	- **private** 가시성을 가지는 int 타입의 x, y, radius 프로퍼티: 원의 중심점과 반지름을 나타냄 
	- **displayCircle()** 메소드: 프로퍼티의 값을 다음과 같은 형식으로 화면에 출력
		
		```
		[Circle] x=1, y=2, radius=3
		```

3. 다음과 같은 main 함수를 통해서 앞서 정의한 두 클래스를 테스트 해 봅니다.

	```
	fun main() {
	    val r1 = Rectangle(1,2,3,4);
	    val r2 = Rectangle(2,3,4,5)
	    val r3 = Rectangle(3,4,5,6)
	    val c1 = Circle(3,4,5)
	    val c2 = Circle(4,5,6)
	    val c3 = Circle(5,6,7)
	    
	    r1.displayRectangle()
	    r2.displayRectangle()
	    r3.displayRectangle()
	    c1.displayCircle()
	    c2.displayCircle()
	    c3.displayCircle()
	}
	```
	- 실행결과

	```
	[Rectangle] x=1, y=2, width=3, height=4
	[Rectangle] x=2, y=3, width=4, height=5
	[Rectangle] x=3, y=4, width=5, height=6
	[Circle] x=3, y=4, radius=5
	[Circle] x=4, y=5, radius=6
	[Circle] x=5, y=6, radius=7
	```

## 2. Shape 클래스  정의

1. 앞의 문제 코드를 클래스 상속을 통해 재구조화한다.
	- **Shape** 클래스는 전체 도형의 슈퍼클래스이고, 다음의 멤버를 가진다.
		- **protected** 가시성을 가진 int 타입의 x, y 프로퍼티: Shape의 기준점을 나타냄

2. 문제1에서 정의한 **Rectangle**과 **Circle** 클래스를 앞서 정의한 **Shape** 클래스의 서브클래스로 수정하시오. 이때 다음 두 가지 방식으로 **Rectangle**과 **Circle** 클래스를 구현하시오
	1. 방식1: 주생성자를 가진 **Rectangle**와 **Circle** 클래스
	2. 방식1: 부생성자만을 가진 **Rectangle**와 **Circle** 클래스
				
3. 문제1에서 사용한 main함수를 통해서 동일과 결과가 나오는지를 확인해보세요

## 3. 업캐스팅과 다운캐스팅 이해
1.  문제2에서 정의한 **Shape**, **Rectangle**, **Circle**  클래스를 그대로 이용하고, 다음과 같이 main함수를 수정하시오.

	```
	fun main() {
	    val r1 = Rectangle(1,2,3,4);
	    val r2 = Rectangle(2,3,4,5)
	    val r3 = Rectangle(3,4,5,6)
	    val c1 = Circle(3,4,5)
	    val c2 = Circle(4,5,6)
	    val c3 = Circle(5,6,7)
	
	    val shapes:Array<Shape> = arrayOf(r1,r2,r3,c1,c2,c3)
	    for (s in shapes) {
	        if (s is Rectangle)
	            s.displayRectangle()
	        else if (s is Circle)
	            s.displayCircle()
	    }
	
	}
	```
2. 위 코드에서 업캐스팅과 다운캐스팅이 일어난 곳은 어느부분이고, 이를 통해 얻게된 이점이 무엇인지 이해해 봅니다.
