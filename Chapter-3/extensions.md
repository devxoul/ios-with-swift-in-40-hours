## 익스텐션 (Extension)

Swift에서는 이미 정의된 타입에 새로운 속성이나 메서드를 추가할 수 있습니다. *익스텐션<sup>Extension</sup>*이라는 기능인데요. `extension` 키워드를 사용해서 정의할 수 있습니다.

```swift
extension String {
  var length: Int {
    return self.characters.count
  }

  func reverse() -> String {
    return self.characters.reverse().map { String($0) }.joinWithSeparator("")
  }
}

let str = "안녕하세요"
str.length // 5
str.reverse() // 요세하녕안
```

> **응용하기**: 거꾸로 된 문자열을 반환하는 대신에, 자기 자신을 거꾸로 바꿔버리는 `reverseInPlace()` 메서드를 만들어보세요. 힌트: `mutating` 키워드와 `self`
