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
## 코틀린에서 Type을 다루는 방법

