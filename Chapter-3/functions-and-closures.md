## 함수와 클로저

함수는 `func` 키워드를 사용해서 정의합니다. `->` 를 사용해서 함수의 반환 타입을 지정합니다.

```swift
func hello(name: String, time: Int) -> String {
    var string = ""
    for _ in 0..<time {
        string += "\(name)님 안녕하세요!\n"
    }
    return string
}
```

Swift에서는 독특하게 함수를 호출할 때 파라미터 이름을 함께 써주어야 합니다. 첫 번째 파라미터는 예외적으로 파라미터 이름을 생략합니다.

```swift
hello("전수열", time: 3)
```

만약, 함수를 호출할 때 사용하는 파라미터 이름과 함수 내에서 사용하는 파라미터 이름을 다르게 사용하고 싶으면, 이렇게 할 수 있습니다.

```swift
func hello(name: String, numberOfTimes time: Int) {
    // 이곳에서는 `time`을 사용합니다.
}

hello("전수열", numberOfTimes: 3) // 이곳에서는 `numberOfTimes`를 사용합니다.
```

이 방법을 사용하면 첫 번째 파라미터에도 이름을 붙일 수 있습니다.

```swift
func hello(withName name: String, numberOfTimes time: Int) {
    // ...
}

hello(withName: "전수열", numberOfTimes: 3)
```

파라미터 이름을 `_`로 정의하면 함수를 호출할 때 파라미터 이름을 생략할 수 있게 됩니다.

```swift
func hello(name: String, _ time: Int) {
    // ...
}

hello("전수열", 3)
```

파라미터에 기본 값을 지정할 수도 있습니다. 기본 값이 지정된 파라미터는 함수 호출시 생략할 수 있습니다.

```swift
func hello(name: String, time: Int = 1) {
    // ...
}

hello("전수열")
```

`...`을 사용하면 개수가 정해지지 않은 파라미터를 받을 수 있습니다.

```swift
func sum(numbers: Int...) -> Int {
    var sum = 0
    for number in numbers {
        sum += number
    }
    return sum
}

sum(1, 2)
sum(3, 4, 5)
```

함수 안에 함수를 또 작성할 수도 있습니다.

```swift
func hello(name: String, time: Int) {
    func message(name: String) {
        return "\(name)님 안녕하세요!"
    }

    for _ in 0..<time {
        print message(name)
    }
}
```

심지어 함수 안에 정의한 함수를 반환할 수도 있습니다.

```swift
func helloGenerator(message: String) -> String -> String {
    func hello(name: String) -> String {
        return name + message
    }
    return hello
}

let hello = helloGenerator("님 안녕하세요!")
hello("전수열")
```

여기서 핵심은, `helloGenerator()` 함수의 반환 타입이 `String -> String`라는 것입니다. 즉, `helloGenerator()`는 '문자열을 받아서 문자열을 반환하는 함수'를 반환하는 함수인 것이죠.

만약 `helloGenerator()` 안에 정의한 `hello()` 함수가 여러개의 파라미터를 받는다면 이렇게 써야 합니다.

```swift
func helloGenerator(message: String) -> (String, String) -> String {
    func hello(firstName: String, lastName: String) -> String {
        return lastName + firstName + message
    }
    return hello
}

let hello = helloGenerator("님 안녕하세요!")
hello("수열", "전")
```

`String -> String`이 `(String, String) -> String`으로 바뀌었죠. 문자열 두 개를 받아서 문자열을 반환하는 의미입니다.

### 클로저 (Closure)

*클로저<sup>Closure</sup>*를 사용하면 바로 위에 작성한 코드를 조금 더 간결하게 만들 수 있습니다. 클로저는 중괄호(`{}`)로 감싸진 '실행 가능한 코드 블럭'입니다.

```swift
func helloGenerator(message: String) -> (String, String) -> String {
    return { (firstName: String, lastName: String) -> String in
        return lastName + firstName + message
    }
}
```

함수와는 다르게 함수 이름 정의가 따로 존재하지 않습니다. 하지만 파라미터를 받을 수 있고, 반환 값이 존재할 수 있다는 점에서 함수와 동일합니다. 혹시 눈치채셨나요? 함수는 이름이 있는 클로저입니다.

위 함수에서 클로저를 반환하는 코드를 조금 더 자세히 살펴볼까요? 클로저는 중괄호(`{}`)로 감싸져있습니다. 그리고 파라미터를 괄호로 감싸서 정의하고요. 함수와 마찬가지로 `->`를 사용해서 반환 타입을 명시합니다. 조금 다른 점은 `in` 키워드를 사용해서 파라미터, 반환 타입 영역과 실제 클로저의 코드를 분리하고 있습니다.

```swift
{ (firstName: String, lastName: String) -> String in
    return lastName + firstName + message
}
```

얼핏 봐서는 별로 간결하다는 느낌을 못받았죠? 클로저의 장점은 사실 간결함와 유연함에 있습니다. 바로 위에서 작성한 코드는 이해를 돕기 위해 생략가능한 것들을 하나도 생략하지 않고 모두 적었기 때문에 조금 복잡해보일 수 있습니다. 이제 하나씩 생략해볼까요?

Swift 컴파일러의 타입 추론 덕분에, `helloGenerator()` 함수에서 반환하는 타입을 가지고 클로저에서 어떤 파라미터를 받고 어떤 타입을 반환하는지를 알 수 있습니다. 과감하게 생략해버리죠.

```swift
func helloGenerator(message: String) -> (String, String) -> String {
    return { firstName, lastName in
        return lastName + firstName + message
    }
}
```

훨씬 깔끔해졌죠? 놀라운 사실은 여기서 생략할 수 있는게 더 있다는 사실입니다. 마찬가지로 타입 추론 덕분에 첫 번째 파라미터가 문자열이고, 두 번째 파라미터도 문자열이라는 것을 알 수 있습니다. 첫 번째 파라미터는 `$0`, 두 번째 파라미터는 `$1`로 바꿔서 쓸 수 있습니다.

```swift
func helloGenerator(message: String) -> (String, String) -> String {
    return {
        return $1 + $0 + message
    }
}
```

클로저 내부의 코드가 한 줄이라면, `return`까지도 생략해버릴 수 있답니다!

```swift
func helloGenerator(message: String) -> (String, String) -> String {
    return { $1 + $0 + message }
}
```

이제 진짜로 간결해졌죠? 처음에 작성했던 `helloGenerator()` 함수의 코드가 4줄이었는데 클로저를 사용하면서 3줄로 줄어들었고, 클로저에서 불필요한 부분을 생략하면서 달랑 1줄로 줄어들었습니다.

클로저는 변수처럼 정의할 수 있습니다.

```swift
let hello: (String, String) -> String = { $1 + $0 + "님 안녕하세요!" }
hello("수열", "전")
```

물론 옵셔널로도 정의할 수 있습니다. 옵셔널 체이닝도 가능하고요.

```swift
let hello: ((String, String) -> String)?
hello?("수열", "전")
```

클로저를 변수로 정의하고 함수에서 반환할 수도 있는 것처럼, 파라미터로도 받을 수 있습니다.

```swift
func manipulateNumber(number: Int, usingBlock block: Int -> Int) -> Int {
    return block(number)
}

manipulateNumber(10, usingBlock: { (number: Int) -> Int in
    return number * 2
})
```

아까 했던 것처럼, 생략할 수도 있습니다.

```swift
manipulateNumber(10, usingBlock: {
    $0 * 2
})
```

만약 함수의 마지막 파라미터가 클로저라면, 괄호와 파라미터 이름마저 생략해버릴 수 있습니다.

```swift
manipulateNumber(10) {
    $0 * 2
}
```

이런 구조로 만들어진 예시가 바로 `sort()`와 `filter()`입니다. 함수가 클로저 하나만을 파라미터로 받는다면, 괄호를 아예 쓰지 않아도 됩니다.

```swift
let numbers = [1, 3, 2, 6, 7, 5, 8, 4]

let sortedNumbers = numbers.sort { $0 < $1 }
print(sortedNumbers) // [1, 2, 3, 4, 5, 6, 7, 8]

let evens = numbers.filter { $0 % 2 == 0 }
print(evens) // [2, 6, 8, 4]
```

### 클로저 활용하기

클로저는 Swift의 굉장히 많은 곳에서 사용됩니다. 바로 위에서 예시를 든 것처럼 `sort()`나 `filter()`와 같은 배열에 많이 쓰입니다. 대표적인 메서드로는 `sort()`, `filter()`, `map()`, `reduce()`가 있습니다. `sort()`와 `filter()`는 바로 위에서 써봤으니 `map()`과 `reduce()`에 대해서 살펴볼까요?

`map()`은 파라미터로 받은 클로저를 모든 요소에 실행하고, 그 결과를 반환합니다. 예를 들어, 정수 배열의 모든 요소들에 2를 더한 값으로 이루어진 배열을 만들고 싶다면, 이렇게 작성할 수 있습니다.

```swift
let arr1 = [1, 3, 6, 2, 7, 9]
let arr2 = arr1.map { $0 * 2 } // [2, 6, 12, 4, 14, 18]
```

`reduce()`는 초깃값이 주어지고, 초깃값과 첫 번째 요소의 클로저 실행 결과, 그리고 그 결과와 두 번째 요소의 클로저 실행 결과, 그리고 그 결과와 세 번째 요소의 클로저 실행 결과, ... 끝까지 실행한 후의 값을 반환합니다. 바로 위에서 정의한 `arr1`의 모든 요소의 합을 구하고 싶다면, 아래와 같이 작성할 수 있습니다.

```swift
arr1.reduce(0, combine: { $0 + $1 }) // 28
```

첫 번째 인자로 주어진 0부터 시작해서, 각 요소들과의 주어진 클로저에 대한 실행 결과를 바로 다음 요소와 실행합니다. 처음에는 0과 1을 더해서 1, 그 결과인 1과 3을 더해서 4, 그리고 4와 6을 더해서 10, 10과 2를 더해서 12, 12와 7을 더해서 19, 그리고 19와 9를 더해서 28이 반환됩니다.

> **Tip**: Swift에서는 연산자도 함수입니다. 함수는 곧 클로저이기 때문에 연산자는 클로저입니다. 1 + 2를 실행하면, `+`라는 이름을 가진 연산자 함수가 실행됩니다. 파라미터로는 1과 2가 넘겨지게 됩니다. 즉, `+` 함수는 파라미터 두 개를 받아서 합을 반환하는 클로저입니다. `{ $0 + $1 }` 인거죠. 그렇기 때문에, 이런 문법도 가능해집니다. `+`라는 연산자를 클로저로 넘겨버리는 거죠.
> 
> ```swift
> arr1.reduce(0, combine: +) // 28
> ```
