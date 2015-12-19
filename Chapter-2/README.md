# 2강 - Swift 둘러보기

이제 본격적으로 Swift에 대해서 알아봅시다. 지난번처럼 Playground를 새로 만들고, 하나씩 따라서 입력해보면 금방 익힐 수 있을 거예요.

## 변수와 상수

변수<sup>variable</sup>는 값을 수정할 수 있고, 상수<sup>constant</sup>는 그렇지 않습니다. Swift에서는 언제 어디서 값이 어떻게 바뀔지 모르는 변수보다는 상수를 사용하는 것을 권장하고 있습니다. 그래야 안전하거든요.

변수는 `var`로 선언하고, 상수는 `let`으로 선언합니다.

```swift
var name = "Suyeol Jeon"
let birthyear = 1995
```

나중에 제가 만약 이름을 바꾸고 싶다면 바꿀 수 있어요.

```swift
name = "전수열"
```

하지만, 아래와 같이 태어난 해를 바꾸려 한다면 컴파일 에러가 발생합니다.

```swift
birthyear = 2000
```

![cannot-assign-to-value-let](../images/Chapter-2/cannot-assign-to-value-let.png)

> Cannot assign to value: 'birthyear' is a 'let' constant

`let` 키워드로 선언된 상수의 값을 변경할 수 없다는 에러입니다. 이렇게, 바뀌면 안되는 값을 상수로 정의해두면 마음놓고 코딩할 수 있어요.

Swift는 정적 타이핑 언어입니다. 말이 어려운데요. 변수나 상수를 정의할 때 그 자료형(타입)이 어떤 것인지를 명시해주어야 하는 언어를 말해요. 예를 들면 이런 것이죠.

```swift
var name: String = "Suyeol Jeon"
let birthyear: Int = 1995
var height: Float = 180.1
```

`name`은 `String`이고, `birthyear`는 `Int`고, `height`은 `Float` 타입이네요. 이렇게 변수 또는 상수 이름 뒤에 콜론(`:`)을 붙이고 자료형을 써주면 된답니다. 이 때 사용하는 `: String`과 `: Int` 등을 가지고 타입 어노테이션<sup>Type Annotation</sup>이라고 합니다. 친구한테 가서 유식한 말 하나 배웠다고 자랑해도 돼요.

### 타입 추론 (Type Inference)

오잉? 또잉? 그런데 우리가 처음에 사용한 예제에서는 자료형을 명시하지 않았어요. 그런데도 우리는 `name`이 문자열이라는 것을 알았고, `birthyear`가 정수형이라는 것을 알았어요.

Swift 컴파일러도 마찬가지로, 큰 따옴표(`"`)로 감싸진 텍스트는 `String` 타입인 것을 알고, 숫자는 `Int` 타입인 것을 인식할 수 있답니다. 꽤 똑똑하죠. 이렇게 타입을 직접 명시하지 않고도 값을 가지고 정적 타이핑을 할 수 있게 해주는 것을 *타입 추론<sup>Type Inference</sup>*이라고 합니다.

이것도 말이 좀 어렵죠. 그래도 알아두면 나중에 친구들 앞에서 "야, 자바는 타입 추론 되냐?" 하고 시비를 걸 수도 있으니 꼭 알아두시길 바랍니다.

### 타입 캐스팅 (Type Casting)

타입 캐스팅은 특정한 타입으로 선언된 변수 혹은 상수의 값을 다른 타입으로 변환하는 것을 말합니다. 예컨대, 위에서 선언한 `name`과 `birthyear`를 가지고 "1995년에 태어난 전수열아 안녕!" 이라는 문자열을 만들고 싶으면 아래와 같이 할 수 있습니다.

```swift
String(birthyear) + "년에 태어난 " + name + "아 안녕!" // 1995년에 태어난 전수열아 안녕!
```

이렇게 쓰면 읽기가 어렵죠? Swift에서는 더 간단하게 작성할 수도 있습니다.

```swift
"\(birthyear)년에 태어난 \(name)아 안녕!" // 1995년에 태어난 전수열아 안녕!
```

Swift에서는 타입을 굉장히 엄격하게 다루기 때문에, 다른 자료형끼리는 기본적인 연산조차 되지 않습니다. 아래와 같이 `Int` 타입인 `birthyear`와 `Float` 타입인 `height`을 더하려고 하면 컴파일 에러가 발생합니다.

```swift
birthyear + height
```

![int-plus-float-error.png](../images/Chapter-2/int-plus-float-error.png)

> Binary operator '+' cannot be applied to operands of type 'Int' and 'Float'

이건 좀 충격적이죠? 일반적인 다른 프로그래밍 언어라면 상상하기 어려운데요. 이럴 때에는 명확하게 다음과 같이 사용해야 합니다.

```swift
Float(birthyear) + height // 2175.1
```

저도 귀찮았는데, 조금만 참고 견디면 금방 익숙해질 거예요.

### 배열(Array)과 딕셔너리(Dictionary)

배열과 딕셔너리는 모두 대괄호(`[]`)를 이용해서 정의할 수 있습니다. 이렇게요.

```swift
var languages = ["Swift", "Objective-C", "Python"]
var capitals = [
    "한국": "서울",
    "일본": "도쿄",
    "중국": "베이징",
]
```

배열과 딕셔너리에 접근하거나 값을 변경할 때에도 대괄호를 사용합니다. 쉽죠?

```swift
languages[0] // Swift
languages[1] = "Ruby"

capitals["한국"] // 서울
capitals["프랑스"] = "파리"
```

참고로, 다른 상수와 마찬가지로 배열과 딕셔너리를 `let`으로 정의하면 값을 수정할 수 없습니다. 물론 값을 추가하거나 빼는 것도 불가능합니다.

위에서 정의해본 `languages`와 `capitals`의 타입은 어떻게 쓸 수 있을까요? 이번에도 대괄호를 써요. 대신, 대괄호 안에 어떤 타입을 받을 것인지를 명시합니다.

```swift
var languages: [String] = ["Swift", "Objective-C", "Python"]
var capitals: [String: String] = [
    "한국": "서울",
    "일본": "도쿄",
    "중국": "베이징",
]
```

만약 빈 배열이나 빈 딕셔너리를 정의하고 싶다면? 이번에도 또 대괄호를 씁니다. 배열과 딕셔너리는 대괄호로 시작해서 대괄호로 끝나는 친구들이에요. (진짜 대괄호로 시작해서 대괄호로 끝나거든요.)

```swift
var languages: [String] = []
var capitals: [String: String] = [:]
```

빈 배열로 선언하는 것을 조금 더 간결하게 하고싶다면, 이렇게 할 수 있어요.

```swift
var languages = [String]()
var capitals = [String: String]()
```

타입 뒤에 괄호(`()`)를 쓰는 것은 *생성자<sup>Initializer</sup>*를 호출하는 것인데요. 아래에서 조금 더 자세하게 다룰 예정입니다.

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
if !number {
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

## 옵셔널 (Optional)

Swift가 가지고 있는 가장 큰 특징 중 하나가 바로 옵셔널<sup>Optional</sup>입니다. 직역하면 '선택적인' 이라는 뜻이 되는데요. 값이 있을 수도 있고 없을 수도 있는 것을 나타냅니다.

예를 들어볼까요? 문자열의 값이 있으면 `"가나다"`가 될 것입니다. 그럼, 값이 없다면 `""`일까요? 땡. `""`도 엄연히 값이 있는 문자열입니다. 정확히는 '값이 없다'가 아니고 '빈 값'이죠. 값이 없는 문자열은 바로 `nil`입니다.

또 다른 예를 들어볼게요. 정수형의 값이 있으면 `123`과 같은 값이 있을 것입니다. 값이 없다면 `0`일까요? 마찬가지로 `0`은 `0`이라는 숫자 '값'입니다. 이 경우에도 값이 없는 정수는 `nil`입니다.

마찬가지로, 빈 배열이나 빈 딕셔너리라고 해서 '값이 없는'것이 아닙니다. 다만 '비어 있을' 뿐이죠. 배열과 딕셔너리의 경우에도 '없는 값'은 `nil`입니다.

이렇게, 값이 없는 경우를 나타낼 때에는 `nil`을 사용합니다. 그렇다고 해서 모든 변수에 `nil`을 넣을 수 있는 것은 아닙니다. 예로, 우리가 위에서 정의한 `name`이라는 변수에 `nil`을 넣으려 하면 에러가 발생합니다.

```swift
var name: String = "전수열"
name = nil
```

![nil-cannot-be-assigned](../images/Chapter-2/nil-cannot-be-assigned.png)

> Nil cannot be assigned to type 'String'

값이 있을 수도 있고 없을 수도 있는 변수를 정의할 때에는 타입 어노테이션에 `?`를 붙여야 합니다. 이렇게 정의한 변수를 바로 *옵셔널<sup>Optional</sup>*이라고 하고요. 옵셔널에 초깃값을 지정하지 않으면 기본값은 `nil`입니다.

```swift
var email: String?
print(email) // nil

email = "devxoul@gmail.com"
print(email) // Optional("devxoul@gmail.com")
```

옵셔널로 정의한 변수는 옵셔널이 아닌 변수와는 다릅니다. 예를 들어, 아래와 같은 코드는 사용할 수 없습니다.

```swift
let optionalEmail: String? = "devxoul@gmail.com"
let requiredEmail: String = optionalEmail
```

![optional-unwrapped](../images/Chapter-2/optional-unwrapped.png)

> Value of optional type 'String?' not unwrapped; did you mean to use '!' or '?'?

`requiredEmail` 변수는  옵셔널이 아닌 `String`이기 때문에 항상 값을 가지고 있어야 합니다. 반면에, `optionalEmail`은 옵셔널로 선언된 변수이기 때문에 실제 코드가 실행되기 전까지는 값이 있는지 없는지 알 수 없습니다. 따라서 Swift 컴파일러는 안전을 위해 `requiredEmail`에는 옵셔널로 선언된 변수를 대입할 수 없게 만들었습니다.

옵셔널은 개념적으로 이렇게 표현할 수 있습니다. 어떤 값 또는 `nil`을 가지고 있는 녀석이죠.

```
        ,-- 어떤 값 (String, Int, ...)
Optional
        `-- nil
```

### 옵셔널 바인딩 (Optional Binding)

그럼 옵셔널의 값을 가져오고 싶은 경우에는 어떻게 하면 될까요? 이 때 사용하는 것이 바로 *옵셔널 바인딩<sup>Optional Binding</sup>*입니다.

옵셔널 바인딩은 옵셔널의 값이 존재하는지를 검사한 뒤, 존재한다면 그 값을 다른 변수에 대입시켜줍니다. `if let` 또는 `if var`를 사용하는데요. 옵셔널의 값을 벗겨서 값이 있다면 `if`문 안으로 들어가고, 값이 `nil`이라면 그냥 통과하게 됩니다.

예를 들어, 아래의 코드에서 `optionalEmail`에 값이 존재한다면 `email`이라는 변수 안에 실제 값이 저장되고, `if`문 내에서 그 값을 사용할 수 있습니다. 만약 `optionalEmail`이 `nil`이라면 `if`문이 실행되지 않고 넘어갑니다.

```swift
if let email = optionalEmail {
    print(email) // optionalEmail의 값이 존재한다면 해당 값이 출력됩니다.
}
// optionalEmail의 값이 존재하지 않는다면 if문을 그냥 지나칩니다.
```

하나의 `if`문에서 콤마(`,`)로 구분하여 여러 옵셔널을 바인딩할 수 있습니다. 이곳에 사용된 모든 옵셔널의 값이 존재해야 `if`문 안으로 진입합니다.

```swift
var optionalName: String? = "전수열"
var optionalEmail: String? = "devxoul@gmail.com"

if let name = optionalName, email = optionalEmail {
    // name과 email 값이 존재
}
```

> **Tip**: 코드가 너무 길 경우에는, 이렇게 여러 줄에 걸쳐서 사용하는 것이 바람직합니다.
>
> ```swift
> if let name = optionalName,
>    let email = optionalEmail {
>     // name과 email 값이 존재
> }
> ```
> 
> 참고로, 두 번째 `let` 부터는 생략이 가능합니다.

위 코드는 아래 코드와 동일합니다.

```swift
if let name = optionalName {
    if let email = optionalEmail {
        // name과 email 값이 존재
    }
}
```

> **Tip**: 한 번의 `if`문에서 여러 옵셔널을 바인딩할 수 있게 된 것은 Swift 1.2 버전부터입니다. 이전 버전까지는 바로 위와 같이 여러 번으로 감싸진 옵셔널 바인딩을 사용했습니다.

옵셔널을 바인딩할 때 `where` 키워드를 통해 조건도 함께 지정할 수 있습니다. `where` 절은 옵셔널 바인딩이 일어난 후에 실행됩니다. 즉, 옵셔널이 벗겨진 값을 가지고 조건을 검사하게 됩니다.

```swift
var optionalAge: Int? = 22

if let age = optionalAge where age >= 20 {
    // age의 값이 존재하고, 20 이상입니다.
}
```

위 코드는 아래 코드와 동일합니다.

```swift
if let age = optionalAge {
    if age >= 20 {
        // age의 값이 존재하고, 20 이상입니다.
    }
}
```

## 옵셔널 체이닝 (Optional Chaining)

Swift 코드를 간결하게 만들어주는 많은 요소들이 있는데, *옵셔널 체이닝<sup>Optional Chaining</sup>*을 알게되면 다른 프로그래밍 언어가 조금 불편하게 느껴지는 경우가 생깁니다.

옵셔널 체이닝을 이해하는 데에는 설명보다 코드를 보는 편이 훨씬 좋습니다. 예컨대, 옵셔널로 선언된 어떤 배열을 떠올려봅시다. 이 배열이 '빈 배열'인지를 검사하려면 어떻게 해야 할까요? `nil`이 아니면서 빈 배열인지를 확인해보면 될 것입니다. 이렇게요.

```swift
let array: [String]? = []
var isEmptyArray = false

if let array = array where array.isEmpty {
    isEmptyArray = true
} else {
    isEmptyArray = false
}

isEmptyArray
```

옵셔널 체이닝을 사용하면 이 코드를 더 간결하게 쓸 수 있습니다.

```swift
let isEmptyArray = array?.isEmpty == true
```

혹시 감이 오시나요? 옵셔널 체이닝은 옵셔널의 속성에 접근할 때, 옵셔널 바인딩 과정을 `?` 키워드로 줄여주는 역할을 합니다. 다음과 같이 3가지 경우의 수를 생각해봅시다.

- `array`가 `nil`인 경우

    ```
    array?.isEmpty
    ~~~~~~
    여기까지 실행되고 `nil`을 반환합니다.
    ```

- `array`가 빈 배열인 경우

    ```
    array?.isEmpty
    ~~~~~~~~~~~~~~
    여기까지 실행되고 `true`를 반환합니다.
    ```

- `array`에 요소가 있는 경우

    ```
    array?.isEmpty
    ~~~~~~~~~~~~~~
    여기까지 실행되고 `false`를 반환합니다.
    ```

`array?.isEmpty`의 결과로 나올 수 있는 값은 `nil`, `true`, `false`가 됩니다. `isEmpty`의 반환값은 `Bool`인데, 옵셔널 체이닝으로 인해 `Bool?`을 반환하도록 바뀐 것이죠. 따라서 값이 실제로 `true`인지를 확인하려면, `== true`를 해주어야 합니다.

## 옵셔널 벗기기

옵셔널을 사용할 때마다 옵셔널 바인딩을 하는 것이 가장 바람직합니다. 하지만, 개발을 하다보면 분명히 값이 존재할 것임에도 불구하고 옵셔널로 사용해야 하는 경우가 종종 있는데요. 이럴 때에는 옵셔널에 값이 있다고 가정하고 값에 바로 접근할 수 있도록 도와주는 키워드인 `!`를 붙여서 사용하면 됩니다.

```swift
print(optionalEmail) // Optional("devxoul@gmail.com")
print(optionalEmail!) // devxoul@gmail.com
```

`!`를 사용할 때에는 주의할 점이 있는데, 옵셔널의 값이 `nil`인 경우에는 런타임 에러가 발생한다는 것입니다. Java의 NullPointerException과 비슷하다고 생각하시면 될 듯 합니다.

```swift
var optionalEmail: String?
print(optionalEmail!) // 런타임 에러!
```

> **fatal error: unexpectedly found nil while unwrapping an Optional value**

런타임 에러가 발생하면 iOS 앱은 강제로 종료(크래시)됩니다. 그러니 굉~~장히 조심해서 사용해야 해요.

## 암묵적으로 벗겨진 옵셔널 (Implicitly Unwrapped Optional)

만약, 옵셔널을 정의할 때 `?` 대신 `!`를 붙이면 `ImplicitlyUnwrappedOptional`이라는 옵셔널로 정의됩니다. 이름이 굉장히 길죠. 직역하면 '암묵적으로 벗겨진 옵셔널'입니다.

```swift
var email: String! = "devxoul@gmail.com"
print(email) // devxoul@gmail.com
```

이렇게 정의된 옵셔널은 `nil`을 포함할 수 있는 옵셔널이긴 한데, 접근할 때 옵셔널 바인딩이나 옵셔널을 벗기는 과정을 거치지 않고도 바로 값에 접근할 수 있다는 점에서 일반적인 옵셔널과 조금 다릅니다.

옵셔널 벗기기와 마찬가지로, 값이 없는데 접근을 시도하면 런타임 에러가 발생합니다.

```swift
var email: String!
print(email) // 런타임 에러!
```

> **fatal error: unexpectedly found nil while unwrapping an Optional value**

가급적이면 일반적인 옵셔널을 사용해서 정의하고, 옵셔널 바인딩 또는 옵셔널 체이닝을 통해 값에 접근하는 것이 더 바람직합니다.

## 함수와 클로저

- 스코프
- `defer` `guard`

## 클래스와 구조체

### 튜플 (Tuple)

튜플<sup>Tuple</sup>은 어떠한 값들의 묶음입니다. 배열과 비슷하다고 볼 수 있는데요. 배열과는 다르게 길이가 고정되어있답니다. 값에 접근할 때에도 `[]` 대신 `.`을 사용해요.

```swift
var coffeeInfo = ("아메리카노", 5100)
coffeeInfo.0 // 아메리카노
coffeeInfo.1 // 5100
coffeeInfo.1 = 5100
```

이 튜플의 파라미터에 이름을 붙일 수도 있어요.

```swift
var namedCoffeeInfo = (coffee: "아메리카노", price: 5100)
namedCoffeeInfo.coffee // 아메리카노
namedCoffeeInfo.price // 5100
namedCoffeeInfo.price = 5100
```

이렇게 보면, 앞서 살펴본 구조체와 비슷하죠? 실제로도 간단한 자료형을 만들 때에는 구조체 대신 튜플을 사용해서 만들기도 한답니다.

튜플의 타입 어노테이션은 이렇게 생겼어요.

```swift
var coffeeInfo: (String, Int)
var namedCoffeeInfo: (coffee: String, price: Int)
```

튜플을 조금 응용하면, 아래와 같이 여러 변수에 값을 지정할 수도 있습니다.

```swift
let (coffee, price) = ("아메리카노", 5100)
coffee // 아메리카노
price // 5100
```

튜플이 가진 값을 가지고 변수에 값을 지정할 때, 무시하고 싶은 값이 있다면 `_` 키워드를 사용해서 할 수 있습니다. 아래 코드에서는 `"라떼"`라는 첫 번째 값을 무시합니다.

```swift
let (_, latteSize, lattePrice) = ("라떼", "Venti", 5600)
latteSize // Venti
lattePrice // 5600
```

물론, 튜플을 반환하는 함수도 만들 수 있습니다.

```swift
/// 커피 이름에 맞는 커피 가격 정보를 반환합니다.
///
/// - Parameters:
///     - name: 커피 이름
///
/// - Returns: 커피 이름과 가격 정보로 구성된 튜플을 반환합니다.
func coffeeInfoForName(name: String) -> (name: String, price: Int)? {
    let coffeeInfoList: [(name: String, price: Int)] = [
        ("아메리카노", 5100),
        ("라떼", 5600),
    ]
    for coffeeInfo in coffeeInfoList {
        if coffeeInfo.name == name {
            return coffeeInfo
        }
    }
    return nil
}

coffeeInfoForName("아메리카노")?.price // 5100
coffeeInfoForName("에스프레소")?.price // nil

let (_, lattePrice) = coffeeInfoForName("라떼")!
lattePrice // 5600
```

## Enum

## 프로토콜

## 익스텐션 (Extension)
