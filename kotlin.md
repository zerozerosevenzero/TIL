## kotlin

## 코틀린에서 변수를 다루는법
- var : 변경 가능하다
- val : 변경 불가능하다 (raed-only)
- 타입을 명시적으로 작성하지 않아도 타입이 추론된다.
--- 
## 코틀린에서 null을 다루는 방법
- null이 아닌 경우에만 호출되는 Safe Call(?.) 이 있다
- null인 경우에만 호출되는 Elvis 연산자 (?:) 가 있다
1. null일 경우 Exception을 발생한다.
```
fun startsWithA1(str: String?): Boolean {
    return str?.startsWith("A")?: throw IllegalArgumentException("null이 들어왔습니다.")
}
```
2. null일 경우 null을 리턴
```
fun startsWithA2(str: String?): Boolean? {
    return str?.startsWith("A")
}
```

3. null일 경우 false를 리턴
```
fun startsWithA3(str: String?): Boolean {
    return str?.startsWith("A") ?: false
}
```

4. null불가 타입 !!
```
fun startsWithA4(str: String?): Boolean {
    return str!!.startsWith("A")
}
```
--- 
## 코틀린에서 연산자를 다루는 방법
- Java에서는 동일성에 ==를 사용, 동등성에 equals를 직접 호출
- Kotlin에서는 동일성에 ===를 사용, 동등성에 == 를 호출, ==을 사용하면 간접적으로 equals를 호출해준다.
- in / !in -> 컬렉션이나 범위에 포함되어 있다, 포함되어 있지 않다.
- a..b -> a부터 b까재 범위 객체를 생성한다.

## 코틀린 반복문을 다루는 방법
1. for each 문
 ```
 val nums = listOf(1L, 2L, 3L)
 for (num in nums) {
    println(num)
 }
 ```
 
 
 ```
 for (i in 1..3) {
    ...
 }
 ```
 
 내려가는 경우
 ```
 for (i in 3 downTo 1) {
    ...
 }
 ```
 
 2칸씩 올라가는 경우
```
 for (i in 1..5 step 2) {
    ...
 }
 ```
 
 ---
 
 # 코틀린에서 상속을 다루는 방법
 ```
 class Cat(
	species: String
) : Animal(species, 4) {
	override fun move() {
    	println("고양이가 사뿐 사뿐 걸어가~")
    }
}
 ```
 위 코드는 고양이가 animal이라는 부모 클래스를 상속 받고 있는 모습입니다.

상속 받을 시 주의사항
- 앞에 무조건 공백을 넣고 부모 클래스를 상속 받아야 됩니다.
- 상속 받음을 나타냄과 동시에 생성자를 호출해야 한다.
- 메소드가 존재하면 override를 필수적으로 붙여주어야 한다. override에는 어노테이션이 없는 지시어이다.

```
abstract class Animal(
	protected val species: String,
    protected open val legCount: Int
) {
	abstract fun move()
}
```

- 추상 프로퍼티가 아니라면, 상속받을 때 open을 붙여야 한다.
- final: override를 할 수 없게 한다. default로 보이지 않게 존재한다. 디폴트로 final이 붙어있다.
- open: override를 열어 준다.
- abstract: 반드시 override 해야 한다.
- override: 상위 타입을 오버라이드 하고 있다.
- 상속 또는 구현을 할 때에 : 을 사용해야 한다.
- 상위 클래스 상속을 구현할 때 생성자를 반드시 호출해야 한다.
- override를 필수로 붙여야 한다.
- 추상 멤버가 아니면 기본적으로 오버라이드가 불가능하다.
- open을 사용해주어야 한다.
- 상위 클래스의 생성자 또는 초기화 블록에서 open 프로퍼티를 사용하면 얘기치 못한 버그가 생길 수 있다.
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 

