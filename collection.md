# 컬렉션 확장 함수 (실습)

## 0. 시작하기 전에

이 Codelab에서는 컬렉션의 다양한 확장함수를 실습해봅니다.

### 실습 준비

- 최신 버전의 JDK와 IntelliJ IDEA IDE가 설치된 컴퓨터
- 컬렉션 주제의 온라인 강의영상 시청 완료

### 실습할 내용

- 컬렉션 요소의 순환 처리: **forEach**, **forEachIndexed**, **onEach**
-  컬렉션 요소의 개수 반환: **count**
-  컬렉션에서 최대값과 최솟값의 요소 반환: **max**, **min**, **maxBy**, **minBy**
-  각 요소에 정해진 식 적용하기: **fold**, **foldRight**, **reduce**, **reduceRight**
-  요소의 검사: **all**, **any**, **contains**, **containsAll**, **none**, **isEmpty**, **isNotEmpty**
-  요소의 필터와 추출: **filter**, **filterNot**, **filterNotNull**, **filterIndexed**, **filterIndexedTo**, **filterIsInstance**
-  특정범위를 잘라내거나 반환하기: **slice**, **take**, **takeLast**, **takeWhile**
-  특정 요소 제외하기: **drop**, **dropWhile**, **dropLastWhile**
-  각 요소의 반환: **componentN**
-  합집합과 교집합: **distinct**, **intersect**
-  요소의 매핑: **map**, **mapIndexed**, **mapNotNull**, **flatMap**, **groupBy**
-  요소의 처리와 검색: **elementAt**, **elementAtOrElse**, **elementAtOrNull**
-  순서와 정렬: **reversed**, **sorted**, **sortedBy**, **sortedDescending**

<a name="1"></a>
## 1. 컬렉션 요소의 순환 처리

- **forEach**, **forEachIndexed**: 각 요소에 대한 순환 처리를 위해 람다식(*action*)을 인자로 전달, 처리 후 컬렉션을 반환하지 않음

	
	```
	public inline fun <T> Iterable<T>.forEach(
	    action: (T) -> Unit
	): Unit
	```
	
	```
	public inline fun <T> Iterable<T>.forEachIndexed(
	    action: (Int, T) -> Unit
	):
	```

	- 실습 코드
		
		```
		val list = listOf(1, 2, 3, 4, 5, 6)
	
	
	    list.forEach { print("$it ") }
	    println()
	    list.forEachIndexed { index, value -> println("index[$index]: $value") }
		```
	
- **onEach**:각 요소를 람다식으로 처리하고 각 컬렉션을 반환

	```
	public inline fun <T, C : Iterable<T>> C.onEach(
	    action: (T) -> Unit
	): C
	```

	- 실습 코드
	
		```
		val list = listOf(1, 2, 3, 4, 5, 6)
		val map = mapOf(11 to "Java", 22 to "Kotlin", 33 to "C++")
		
		val returnedList = list.onEach { print(it) }
		println("returnedList = $returnedList")
		val returnedMap = map.onEach { println("key: ${it.key}, value: ${it.value}") }
		println("returnedMap = $returnedMap")
		```



## 2. 	요소의 개수 반환하기

- **count**: 주어진 predicate에 일치하는 요소의 개수를 반환

	```
	public inline fun <T> Iterable<T>.count(
	    predicate: (T) -> Boolean
	): Int
	```
	
	- 실습코드
	
		```
		val list = listOf(1, 2, 3, 4, 5, 6)
		println(list.count { it % 2 == 0 })
		```

## 3. 컬렉션에서 최대값과 최솟값의 요소 반환
- **max**

	```
	public fun <T : Comparable<T>> Iterable<T>.max(): T?
	  kotlin.collections
	```

- **min**

	``` 
	public fun <T : Comparable<T>> Iterable<T>.min(): T?
	  kotlin.collections
	```
- **maxBy**	
	
	```
	public inline fun <K, V, R : Comparable<R>> Map<out K, V>.maxBy(
	    selector: (Map.Entry<K, V>) -> R
	): Map.Entry<K, V>?
	```

- **minBy**

	```
	public inline fun <K, V, R : Comparable<R>> Map<out K, V>.minBy(
	    selector: (Map.Entry<K, V>) -> R
	): Map.Entry<K, V>? 
	```
- maxBy와 minBy는 람다식에 의해 컬렉션 요소를 처리
- 실습코드

	```
	val list = listOf(1, 2, 3, 4, 5, 6)
	
	// max: 가장 높은/낮은 요소의 반환
	println(list.max()) // 6
	println(list.min()) // 1
	
	// maxBy/minBy: 최대/최솟값으로 나온 요소 it에 대한 식의 결과
	println("maxBy: " + map.maxBy { it.key }) // 키를 기준으로 최댓값
	println("minBy: " + map.minBy { it.key }) // 키를 기준으로 최솟값
	```
	
## 4. 각 요소에 정해진 식 적용하기

- **fold**: 초기값 (*initial*)에서 부터 정해진 식(*operation*)을 처음 요소부터 끝 요소까지 적용하여 계산한 값을 반환
	
	```
	public inline fun <T, R> Iterable<T>.fold(
	    initial: R,
	    operation: (R, T) -> R
	): R
	```
- **foldRight**: **fold**와 같고, 마지막 요소에서 처음 요소순으로 적용
- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)

    // fold: 초기값과 정해진 식에 따라 처음요소부터 끝 요소에 적용하며 값을 생성
    println(list.fold(4) { total, next -> total + next }) // 4+ 1 + ... 6 = 25
    println(list.fold(1) { total, next -> total * next }) // 1 * 1 * 2 *... 6 = 720
    
    // foldRight: fold와 같고 마지막 요소에서 처음요소로 반대로 적용
    println(list.foldRight(4) { total, next -> total + next })
    println(list.foldRight(1) { total, next -> total * next })
    ```
- **reduce**: 정해진 식(*operation*)을 처음 요소부터 끝 요소까지 적용하여 계산한 값을 반환

	```
	public inline fun <S, T : S> Iterable<T>.reduce(
	    operation: (S, T) -> S
	): S
	```
- **reduceRight**: **reduce**와 같고, 마지막 요소에서 처음 요소순으로 적용
- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)

    // reduce: fold와 동일하지만 초기값을 사용하지 않음
    println(list.reduce { total, next -> total + next })
    println(list.reduceRight { total, next -> total + next })
    ```

## 5. 요소의 검사

- **all**: 모든 요소가 주어진 *predicate*과 일치할 때, true를 반환

	```
	public inline fun <T> Iterable<T>.all(
	    predicate: (T) -> Boolean
	): Boolean
	```

- **any**: 최소한 하나 혹은 그 이상의 요소가 주어진 *predicate*과 일치할 때, true를 반환

	```
	public inline fun <T> Iterable<T>.any(
	    predicate: (T) -> Boolean
	): Boolean
	```

- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)
    val listPair = listOf(Pair("A", 300), Pair("B", 200), Pair("C", 100))
    val map = mapOf(11 to "Java", 22 to "Kotlin", 33 to "C++")

    // all: 모든 요소가 매치 되어야 true를 반환
    println(list.all { it < 10 })  // true
    println(list.all { it % 2 == 0 }) // false

    // any: 최소한 하나 혹은 그 이상의 특정 요소가 매치되면 true를 반환
    println(list.any { it % 2 == 0 }) // true
    println(list.any { it > 10 }) // false
    ```
    
- **contains** : 요소가 포함되어 있는지를 검사 

	```
	public abstract fun contains(
	    element: E
	): Boolean
	```

- **containsAll** : 모든 요소가 포함되어 있는지를 검사 

	```
	public abstract fun containsAll(
	    elements: Collection<E>
	): Boolean
	```

- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)

    // contains: 요소가 포함되어 있으면 true
    println("contains: " + list.contains(2))  // true
    println(2 in list)  // true
    
    // containsAll: 모든 요소가 포함되어 있으면 true
    println("containsAll: " + list.containsAll(listOf(1, 2, 3)))
    ```
    
- **none()**, **isEmpty()**, **isNotEmpty()**: 요소가 없는지, 비어 있는지 검사
- **none**:  주어진 *predicate*과 일치하는 요소가 하나도 없으면 true 반환

	```
	public inline fun <T> Iterable<T>.none(
	    predicate: (T) -> Boolean
	): Boolean
	```
	
- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)

    // none: 요소가 없으면 true, 있으면 false
    println("none: " + list.none()) // false
    println("none: " + list.none { it > 6}) // true - 6 이상은 없으므로

    // isEmpty/isNotEmpty: 컬렉션이 비어있는지 검사
    println(list.isEmpty()) // false
    println(list.isNotEmpty()) // true
    ```
    
## 6.  요소의 필터와 추출
### 특정 요소를 골라내기
- **filter**: 주어진 *prediate*과 일치하는 요소들만 포함한 리스트 반환
	
	```
	public inline fun <T> Iterable<T>.filter(
	    predicate: (T) -> Boolean
	): List<T>
	```

- **filterNot**: 주어진 *predicate*과 일치하지 않는 요소들만 포함한 리스트 반환

	```
	public inline fun <T> Iterable<T>.filterNot(
	    predicate: (T) -> Boolean
	): List<T>
	```

- **filterNotNull**: null을 제외한 요소들만 포함한 리스트 반환

	```
	public fun <T : Any> Iterable<T?>.filterNotNull(): List<T>
	```
	
- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)
    val listWithNull = listOf(1, null, 3, null, 5, 6)
    
    // filter: 식에 따라 요소를 골라내기
    println(list.filter { it % 2 == 0 }) // [2, 4, 6] - 짝수만 골라내기
    println(list.filterNot { it % 2 == 0 }) // [1, 3, 5] - 식 이외에 요소
    println(listWithNull.filterNotNull()) // [1, 3, 5, 6] - null을 제외
    ```	
    
- **filterIndexed**: 인덱스와 함께 주어진 *prediate*과 일치하는 요소들만 포함한 리스트 반환

	```
	public inline fun <T> Iterable<T>.filterIndexed(
	    predicate: (Int, T) -> Boolean
	): List<T>
	```    
	
- **filterIndexedTo**: 주어진 *predicate*과 일치하는 모든 요소를 포함한 컬렉션을 반환

	```
	public inline fun <T, C : MutableCollection<in T>> Iterable<T>.filterIndexedTo(
	    destination: C,
	    predicate: (Int, T) -> Boolean
	): C
	```
	
- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)
    
    // filterIndexed: 인덱스와 함께 추출
    println("filterIndexed: " + list.filterIndexed { idx, value -> idx != 1 && value % 2 == 0 })

    // filterIndexedTo: 추출 후 mutable 컬렉션으로 변환
    val mutList =
            list.filterIndexedTo(mutableListOf()) { idx, value -> idx != 1 && value % 2 == 0 }
    println("filterIndexedTo: $mutList")
    ```
    
- **filterKeys**: 주어진 *predicate*과 일치하는 키를 가진 모든 (키, 값)의 쌍을  포함한 Map을 반환

	```
	public inline fun <K, V> Map<out K, V>.filterKeys(
	    predicate: (K) -> Boolean
	): Map<K, V>
	```
	
- **filterValues**: 주어진 *predicate*과 일치하는 값을 가진 모든 (키, 값)의 쌍을  포함한 Map을 반환

	```
	public inline fun <K, V> Map<out K, V>.filterValues(
	    predicate: (V) -> Boolean
	): Map<K, V>
	```
	
- 실습코드

    ```
    val map = mapOf(11 to "Java", 22 to "Kotlin", 33 to "C++")
    
    // filterKeys/filterValues: Map의 키/값에 따른 필터
    println("filterKeys: " + map.filterKeys { it != 11 }) // {22=Kotlin, 33=C++}
    println("filterValues: " + map.filterValues { it == "Java" }) // {11=Java}
    ```	
    
- **filterIsInstance**: 명시된 R 타입의 모든 인스턴스를 포함한 리스트를 반환

	```
	public inline fun <reified R> Iterable<*>.filterIsInstance(): List<@NoInfer R>
	```

- 실습코드

    ```
    val listMixed = listOf(1, "Hello", 3, "World", 5, 'A')
    
    // filterIsInstance: 여러 타입의 요소중 원하는 타입을 골라냄
    println("filterIsInstance: " + listMixed.filterIsInstance<String>())	// [Hello, World]
    ```

### 특정 범위를 잘라내거나 반환하기
- **slice**: 특정 범위의 인덱스를 가진 List를 인자로 사용해 기존 List에서 요소들을 잘라내어 반환

	```
	public fun <T> List<T>.slice(
	    indices: Iterable<Int>
	): List<T>
	```
	
- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)
    
    // slice: 특정 인덱스의 요소들을 잘라서 반환하기
    println("slice: " + list.slice(listOf(0, 1, 2))) // [1, 2, 3]
    ```
    
- **take**: 처음 n개의 요소를 포함한 리스트를 반환

	```
	public fun <T> Iterable<T>.take(
	    n: Int
	): List<T>
	```    
-  **takeLast**: 마지막 n개의 요소를 포함한 리스트를 반환

	```
	public fun <T> List<T>.takeLast(
	    n: Int
	): List<T>
	```
	
- **takeWhile**: 주어진 *predicate*과 일치하는 요소를 포함한 리스트를 반환

	```
	public inline fun <T> Iterable<T>.takeWhile(
	    predicate: (T) -> Boolean
	): List<T>
	```

- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)

    // take: n개의 요소를 반환
    println("take: " + list.take(2)) // [1, 2]
    println("takeLast: " + list.takeLast(2)) // [5, 6] - 마지막 요소부터
    println("takeWhile: " + list.takeWhile { it < 3 }) // [1, 2] - 조건식에 따른 반환
    ```
    
### 특정 요소 제외하기
- **drop**: **take**과 정반대

- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)

    // drop: 처음부터 n개의 요소를 제외한 목록 List 반환
    println("drop: " + list.drop(3)) // [4, 5, 6]
    println("dropWhile: " + list.dropWhile { it < 3 }) // [3, 4, 5, 6]
    println("dropLastWhile: " + list.dropLastWhile { it > 3 }) // [1, 2, 3]
    ```
 
### 각 요소의 반환   
- **componentN**: 1부터 시작하는 N번째 요소를 반환

- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)

    println("component1(): " + list.component1()) // 1
    ```
    
### 합집합과 교집합
- **distinct()** : 여러 중복 요소가 있는 경우 1개로 취급해 다시 컬렉션 List로 반환
- **intersect()**: 파라미터 *other* 컬렉션과 겹치는 요소만 골라내 Set으로 반환
	
	```
	public infix fun <T> Iterable<T>.intersect(
	    other: Iterable<T>
	): Set<T>
	```
	
- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)
    val listRepeated = listOf(2, 2, 3, 4, 5, 5, 6)
    
     // distinct: 중복 요소는 하나로 취급해 목록 반환
    println("distinct: " + listRepeated.distinct()) // [2, 3, 4, 5, 6]

    // intersect: 교집합 요소만 골라낸다
    println("intersect: " + list.intersect(listOf(5, 6, 7, 8)))
    ```
    
## 7. 요소의 매핑
- **map**: 주어진 식 *transform**을 이용해 새로운 List를 반환

	```
	public inline fun <T, R> Iterable<T>.map(
	    transform: (T) -> R
	): List<R>
	```

- **mapIndexed**: 인덱스를 포함한 주어진 식을 이용해 새로운 List를 반환

	```
	public inline fun <T, R> Iterable<T>.mapIndexed(
	    transform: (Int, T) -> R
	): List<R>
	```

- **mapNotNull**: null을 제외하고 주어진 식을 이용해 새로운 List를 반환

	```
	public inline fun <T, R : Any> Iterable<T>.mapNotNull(
	    transform: (T) -> R?
	): List<R>
	```
	
- 실습코드

    ```
    val list = listOf(1, 2, 3, 4, 5, 6)
    val listWithNull = listOf(1, null, 3, null, 5, 6)

    // map: 컬렉션에 주어진 식을 적용해 새로운 컬렉션을 반환
    println(list.map { it * 2 })

    // mapIndexed:  컬렉션에 인덱스를 포함해 주어진 식을 적용해 새로운 컬렉션 반환
    val mapIndexed = list.mapIndexed { index, it -> index * it }
    println(mapIndexed)

    // mapNotNull: null을 제외하고 식을 적용해 새로운 컬렉션 반환
    println(listWithNull.mapNotNull { it?.times(2) })
    ```
    
- **flatMap**: 컬렉션의 각 요소에 *transform*식을 적용한 후, 이것을 다시 하나로 합쳐 새로운 컬렉션을 반환

	```
	public inline fun <T, R> Iterable<T>.flatMap(
	    transform: (T) -> Iterable<R>
	): List<R>
	```
	
	- 실습코드
	
	    ```
	    val list = listOf(1, 2, 3, 4, 5, 6)
	    
	    // flatMap: 각요소에 식을 적용 후 다시 합쳐 새로운 컬렉션을 반환
	    println(list.flatMap { listOf(it, 'A') })
	    val result = listOf("abc", "12").flatMap { it.toList() }
	    println(result) // [a, b, c, 1, 2]
	    ```
	
- **groupBy**: 주어진 식 *keySelector*에 따라 요소를 그룹화하고 이것을 키로 사용하여 다시 Map으로 반환

	```
	public inline fun <T, K> Iterable<T>.groupBy(
	    keySelector: (T) -> K
	): Map<K, List<T>>
	```	
	
	- 실습코드
	
	    ```
	    val list = listOf(1, 2, 3, 4, 5, 6)
	    
	    // groupBy: 주어진 함수의 결과에 따라 그룹화 하여 map으로 반환
	    val grpMap = list.groupBy { if (it % 2 == 0) "even" else "odd" }
	    println(grpMap) // {odd=[1, 3, 5], even=[2, 4, 6]}
	    ```
    
## 8. 요소 처리와 검색

- **elementAt(index)**: index 위치의 요소를 반환; index가 범위를 벗어나면 예외 발생
- **elementAtOrNull(index)**: index 위치의 요소를 반환하거나 index가 범위를 벗어나는 경우 null을 반환
- **elementAtorElse**: index가 범위를 벗어나는 경우 defaultValue 식의 결과를 반환

	```
	public inline fun <T> List<T>.elementAtOrElse(
	    index: Int,
	    defaultValue: (Int) -> T
	): T
	```
	
	- 실습코드
	
	    ```
	    val list = listOf(1, 2, 3, 4, 5, 6)
	
	    // elementAt: 인덱스에 해당하는 요소 반환
	    // 범위를 벗어나는 경우 IndexOutOfBoundsException 가 발생
	    println("elementAt: " + list.elementAt(1))
	
	    // elementAtOrElse: 인덱스를 벗어나는 경우 식에 따라 결과 반환 아니면 요소 반환
	    println("elementAtOrElse: " + list.elementAtOrElse(10, { 2 * it }))
	    // elementAtOrElse(10) { 2 * it }) 표현식과 동일
	
	    // elementAtOrNull: 인덱스를 벗어나는 경우 null 반환
	    println("elementAtOrNull: " + list.elementAtOrNull(10))
	    ```

- **first**, **last**, **firstOrNull**, **lastOrNull**: 식과 일치하는 첫번째나 마지막 요소 값을 반환

	```
	public inline fun <T> Iterable<T>.first(
	    predicate: (T) -> Boolean
	): T
	```
	```
	public inline fun <T> Iterable<T>.last(
	    predicate: (T) -> Boolean
	): T
	```
	```
	public inline fun <T> Iterable<T>.firstOrNull(
	    predicate: (T) -> Boolean
	): T?
	```
	```
	public inline fun <T> Iterable<T>.lastOrNull(
	    predicate: (T) -> Boolean
	): T?
	```
	- 실습코드
	
	    ```
	    val listPair = listOf(Pair("A", 300), Pair("B", 200), Pair("C", 100), Pair("D", 200))
	    
	    // first: 식에 일치하는 첫 요소 반환
	    println("first: " + listPair.first { it.second == 200 })
	
	    // last: 식에 일치하는 마지막 요소 반환
	    println("last: " + listPair.last { it.second == 200 })
	
	    // firstOrNull: 식에 일치하지 않은 경우 null 반환
	    println("firstOrNull: " + listPair.firstOrNull { it.first == "E" })
	
	    // lastOrNull: 식에 일치하지 않은 경우 null 반환
	    println("lastOrNull: " + listPair.lastOrNull { it.first == "E" })
	    ```
    
- **indexOf(element)**: 주어진 요소 element에 일치하는 첫 인덱스 반환
- **indexOfFirst**: 람다식에 일치하는 첫 요소의 인덱스 반환 없으면 -1
	
	```
	public inline fun <T> List<T>.indexOfFirst(
	    predicate: (T) -> Boolean
	): Int
	```
- **lastIndexOf(element)**: 주어진 요소에 일치하는 가장 마지막 인덱스 반환
- **indexOfLast**: 람다식에 일치하는 마지막 요소의 인덱스 반환 없으면 -1

	```
	public inline fun <T> List<T>.indexOfLast(
	    predicate: (T) -> Boolean
	): Int
	```

	- 실습코드
	
	    ```
	    val list = listOf(1, 2, 3, 4, 5, 6)
		
	    // indexOf: 주어진 요소의 일치하는 첫 인덱스 반환
	    println("indexOf:" + list.indexOf(4)) // 3
	
	    // indexOfFirst: 람다식에 일치하는 첫 요소의 인덱스 반환, 없으면 -1
	    println("indexOfFirst:" + list.indexOfFirst { it % 2 == 0 }) // 1
	
	    // lastIndexOf: 주어진 요소 일치하는 가장 마지막 인덱스 반환
	    println("lastIndexOf:" + listRepeated.lastIndexOf(5)) // 5
	
	    // indexOfLast: 람다식에 일치하는 마지막 요소의 인덱스 반환, 없으면 -1
	    println("indexOfLast:" + list.indexOfLast { it % 2 == 0 }) // 5
	    ```	
	
- **single**, **singleOrNull**: 해당 조건식에 일치하는 요소 하나를 반환

	```
	public inline fun <T> Iterable<T>.single(
	    predicate: (T) -> Boolean
	): T
	
	public inline fun <T> Iterable<T>.singleOrNull(
	    predicate: (T) -> Boolean
	): T?
	```
	
	- 실습코드
	
	    ```
	    val listPair = listOf(Pair("A", 300), Pair("B", 200), Pair("C", 100), Pair("D", 200))
	    	
	    // single: 람다식에 일치하는 요소 하나 반환
	    println("single: " + listPair.single { it.second == 100 })
	    println("singleOrNull: " + listPair.singleOrNull { it.second == 500 })
	    ```
    
- **binarySearch** 
	- 인자로 주어진 요소 element에 대해 이진 탐색 후 요소의 인덱스를 반환   
	- 중복된 요소가 있는 경우에 해당 요소가 원하는 순서에 있는 요소인지를 보장하지 않음	

	```
	public fun <T : Comparable<T>> List<T?>.binarySearch(
	    element: T?,
	    fromIndex: Int = ...,
	    toIndex: Int = ...
	): Int
	```
	
	- 실습코드
	
		```
		val list = listOf(1, 2, 3, 4, 5, 6)
		    	    
		// binarySearch: 요소에 대해 이진 검색후 인덱스 반환
		println("binarySearch: " + list.binarySearch(3))
		```

- **find**: 조건식을 만족하는 첫번째 검색된 요소를 반환, 없으면 null 반환

	```
	public inline fun <T> Iterable<T>.find(
	    predicate: (T) -> Boolean
	): T?
	```	
	
	- 실습코드

		```
		val list = listOf(1, 2, 3, 4, 5, 6)
		
		// find: 조건식을 만족하는 첫번째 검색된 요소 반환, 없으면 null
		println("find: " + list.find { it > 3 })
		```
		
## 9. 컬렉션의 분리와 병합
- **union**: 두 컬렉션의 중복된 요소를 하나만 포함하는 Set을 반환 

	```
	public infix fun <T> Iterable<T>.union(
	    other: Iterable<T>
	): Set<T>
	```

- **plus**: 기존 컬렉션 다음에 elements 컬렉션을 합하여 List로 반환

	```
	public operator fun <T> Collection<T>.plus(
	    elements: Iterable<T>
	): List<T>
	```

- **partition**: 주어진 predicate을 기준으로 컬렉션을 두개의 컬렉션을 분리해 Pair로 반환

	```
	public inline fun <T> Iterable<T>.partition(
	    predicate: (T) -> Boolean
	): Pair<List<T>, List<T>>
	```

- **zip**:  2개의 컬렉션을 동일한 인덱스끼리 Pair를 만들어 반환

	```
	public infix fun <T, R> Iterable<T>.zip(
	    other: Iterable<R>
	): List<Pair<T, R>>
	```
- 실습코드

    ```
    val list1 = listOf(1, 2, 3, 4, 5, 6)
    val list2 = listOf(2, 2, 3, 4, 5, 5, 6, 7)

    // union: 두 List를 합친다 (중복요소는 하나만)
    println(list1.union(list2))

    // union: 두 List를 합친다 (중복요소 포함), + 연산자와 같음
    println(list1.plus(list2))

    // partition: 주어진 식에 따라 두개의 컬렉션으로 분리해 Pair로 반환
    // 첫번째 컬렉션은 true, 두번째 컬렉션은 식이 false일 때
    val part =  list1.partition { it % 2 == 0 }
    println(part)

    // zip: 동일 인덱스끼리 Pair를 만들어 반환
    // (반환 시 가장 작은 요소를 가진 컬렉션의 갯수 만큼만 반환)
    val zip = list1.zip(listOf(7, 8))
    println(zip)
    ```
    
## 10. 순서와 정렬
- **reversed()**: 뒤집힌 순서로 컬렉션 반환 
- **sorted()**: 정렬된 컬렉션 반환
- **sortedDescending()**: 내림차 순으로 정렬된 컬렉션 반환
- **sortedBy**: *selector*에 의해서 반환된 값을 기준으로 정렬된 컬렉션 반환
	
	```
	public inline fun <T, R : Comparable<R>> Iterable<T>.sortedBy(
	    crossinline selector: (T) -> R?
	): List<T>
	```
- **sortedByDescending**: *selector*에 의해서 반환된 값을 기준으로 큰수에서 작은수로 정렬된 컬렉션 반환

	```
	public inline fun <T, R : Comparable<R>> Iterable<T>. sortedByDescending(
	    crossinline selector: (T) -> R?
	): List<T>
	```

- 실습코드

    ```
    // resersed: 뒤집힌 순서의 컬렉션 반환
    val unsortedList = listOf(3, 2, 7, 5)
    println(unsortedList.reversed()) // [5, 7, 2, 3]

    // sort: 요소를 정렬 후 정렬된 컬렉션 반환
    println(unsortedList.sorted()) // [2, 3, 5, 7]
    // 내림차순 정렬
    println(unsortedList.sortedDescending()) // [7, 5, 3, 2]

    // sortBy: 특정 비교식에 의해 정렬된 컬렉션 반환
    println(unsortedList.sortedBy { it % 3 }) // [3, 7, 2, 5]
    println(unsortedList.sortedByDescending { it % 3 }) // [2, 5, 7, 3]
    ```