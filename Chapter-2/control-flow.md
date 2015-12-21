## 조건문과 반복문

조건을 검사할 때에는 `if`, `switch`를 씁니다. 아래 코드는 `if`를 사용한 예시입니다.

```swift
var age = 19
var student = ""

if age >= 8 && age < 14 {
    student = "초등학생"
} else if age < 17 {
    student = "중학생"
} else if age < 20 {
    student = "고등학생"
} else {
    student = "기타"
}

student // 고등학생
```

`if`문의 조건절에는 값이 정확하게 참 혹은 거짓으로 나오는 `Bool` 타입을 사용해야 합니다. 위에서 언급한 것과 같이 Swift에서는 타입 검사를 굉장히 엄격하게 하기 때문에, 다른 언어에서 사용 가능한 아래와 같은 코드를 사용하지 못합니다.

```swift
var number = 0
if !number { // 컴파일 에러!
    // ...
}
```

![if-test-int](../images/Chapter-2/if-test-int.png)

> Unary operator '!' cannot be applied to an operand of type 'Int'

대신, 이렇게 써야해요.

```swift
if number == 0 {
    // ...
}
```

빈 문자열이나 배열 등을 검사할 때에도 명확하게 길이가 0인지를 검사해야 합니다.

```swift
if name.isEmpty { ... }
if languages.isEmpty { ... }
```

만약 C나 Java와 같은 프로그래밍 언어를 사용해봤다면 `switch`는 단순히 값이 '같은지'만을 검사하는 것으로 알고 있을텐데요. Swift의 `switch` 구문은 조금 특별합니다. 패턴 매칭이 가능하기 때문입니다. 아래 코드는 위에서 작성한 `if`문을 `switch`문으로 옮겨본 것입니다.

```swift
switch age {
case 8..<14:
    student = "초등학생"
case 14..<17:
    student = "중학생"
case 17..<20:
    student = "고등학생"
default:
    student = "기타"
}
```

`8..<14`와 같이 범위<sup>Range</sup> 안에 `age`가 포함되었는지 여부를 검사할 수 있습니다.

반복되는 연산을 할 때에는 `for`, `while`을 씁니다. `for` 구문을 사용해서 배열과 딕셔너리를 차례로 순환할 때에는 아래와 같이 씁니다.

```swift
for language in languages {
    print("저는 \(language) 언어를 다룰 수 있습니다.")
}

for (country, capital) in capitals {
    print("\(country)의 수도는 \(capital)입니다.")
}
```

쉽죠? 단순한 반복문을 만들고 싶다면 범위를 만들어서 반복시킬 수도 있어요. 아래 예시는 1강에서 Playground를 만들고 가장 먼저 입력했던 코드입니다.

```swift
for i in 0..<100 {
    i
}
```

만약 `i`를 사용하지 않는데 단순한 반복을 하고 싶다면, `i` 대신 `_`를 사용해서 무시할 수도 있어요.

```swift
for _ in 0..<10 {
    print("Hello!")
}
```

`-` 키워드는 어디서나 변수 이름 대신에 사용할 수 있는데요. 알아두면 유용하게 사용할 수 있답니다.

`while`은 조건문의 값이 `true`일 때 계속 반복됩니다.

```swift
var i = 0
while i < 100 {
    i += 1
}
```
