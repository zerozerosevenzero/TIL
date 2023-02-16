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

