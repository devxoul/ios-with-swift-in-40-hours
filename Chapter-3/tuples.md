## 튜플 (Tuple)

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
/// 커피 이름에 맞는 커피 가격 정보를 반환합니다. 일치하는 커피 이름이 없다면 `nil`을 반환합니다.
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
