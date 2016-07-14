## 클래스와 구조체

*클래스<sup>Class</sup>*는 `class`로 정의하고, *구조체<sup>Structure</sup>*는 `struct`로 정의합니다.

```swift
class Dog {
    var name: String?
    var age: Int?

    func simpleDescription() -> String {
        return "🐶 \(self.name)"
    }
}

struct Coffee {
    var name: String?
    var size: String?

    func simpleDescription() -> String {
        return "☕️ \(self.name)"
    }
}

var myDog = Dog()
myDog.name = "찡코"
myDog.age = 3
print(myDog.simpleDescription()) // 🐶 찡코

var myCoffee = Coffee()
myCoffee.name = "아메리카노"
myCoffee.size = "Venti"
print(myCoffee.simpleDescription()) // ☕️ 아메리카노
```

클래스는 상속이 가능합니다. 구조체는 불가능합니다.

```swift
class Animal {
    let numberOfLegs = 4
}

class Dog: Animal {
    var name: String?
    var age: Int?
}

var myDog = Dog()
print(myDog.numberOfLegs) // Animal 클래스로부터 상속받은 값 (4)
```

클래스는 참조<sup>Reference</sup>하고, 구조체는 복사<sup>Copy</sup>합니다.

```swift
var dog1 = Dog()  // dog1은 새로 만들어진 Dog()를 참조합니다.
var dog2 = dog1   // dog2는 dog1이 참조하는 Dog()를 똑같이 참조합니다.
dog1.name = "찡코" // dog1의 이름을 바꾸면 Dog()의 이름이 바뀌기 때문에,
print(dog2.name)  // dog2의 이름을 가져와도 바뀐 이름("찡코")이 출력됩니다.

var coffee1 = Coffee()   // coffee1은 새로 만들어진 Coffee() 그 자체입니다.
var coffee2 = coffee1    // coffee2는 coffee1을 복사한 값 자체입니다.
coffee1.name = "아메리카노" // coffee1의 이름을 바꿔도
coffee2.name             // coffee2는 완전히 별개이기 때문에 이름이 바뀌지 않습니다. (nil)
```

### 생성자 (Initializer)

클래스와 구조체 모두 생성자를 가지고 있습니다. 생성자에서는 속성의 초깃값을 지정할 수 있습니다.

```swift
class Dog {
    var name: String?
    var age: Int?
    
    init() {
        self.age = 0
    }
}

class Coffee {
    var name: String?
    var size: String?
    
    init() {
        self.size = "Tall"
    }
}
```

만약 속성이 옵셔널이 아니라면 항상 초깃값을 가져야 합니다. 만약 옵셔널이 아닌 속성이 초깃값을 가지고 있지 않으면 컴파일 에러가 발생합니다.

```swift
class Dog {
    var name: String?
    var age: Int // 컴파일 에러!
}
```

> **stored property 'age' without initial value prevents synthesized initializers**

속성을 정의할 때 초깃값을 지정해 주는 방법과,

```swift
class Dog {
    var name: String?
    var age: Int = 0 // 속성을 정의할 때 초깃값 지정
}
```

생성자에서 초깃값을 지정해주는 방법이 있습니다.

```swift
class Dog {
    var name: String?
    var age: Int
    
    init() {
        self.age = 0 // 생성자에서 초깃값 지정
    }
}
```

생성자도 함수와 마찬가지로 파라미터를 받을 수 있습니다.

```swift
class Dog {
    var name: String?
    var age: Int
    
    init(name: String?, age: Int) {
        self.name = name
        self.age = age
    }
}

var myDog = Dog(name: "찡코", age: 3)
```

만약 상속받은 클래스라면 생성자에서 상위 클래스의 생성자를 호출해주어야 합니다. 만약 생성자의 파라미터가 상위 클래스의 파라미터와 같다면, `override` 키워드를 붙여주어야 합니다. `super.init()`은 클래스 속성들의 초깃값이 모두 설정 된 후에 해야 합니다. 그리고 나서부터 자기 자신에 대한 `self` 키워드를 사용할 수 있습니다.

```swift
class Dog: Animal {
    var name: String?
    var age: Int
    
    override init() {
        self.age = 0 // 초깃값 설정
        super.init() // 상위 클래스 생성자 호출
        print(self.simpleDescription()) // 여기서부터 `self` 접근 가능
    }
    
    func simpleDescription() -> String {
        return "🐶 \(self.name)"
    }
}
```

만약, 위 예시 코드를 아래처럼 바꿔서 `super.init()`을 하기 전에 `self`에 접근한다면 컴파일 에러가 발생합니다.

```swift
override init() {
    self.age = 0
    print(self.simpleDescription()) // 컴파일 에러!
    super.init()
}
```

> **error: use of 'self' in method call 'simpleDescription' before super.init initializes self**

`deinit`은 메모리에서 해제된 직후에 호출됩니다.

```swift
class Dog {
    // ...
    
    deinit {
        print("메모리에서 해제됨")
    }
}
```

### 속성 (Properties)

속성은 크게 두 가지로 나뉩니다. *값을 가지는 속성<sup>Stored Property</sup>*과 *계산되는 속성<sup>Computed Property</sup>*인데요. 한글말로 쓰니까 굉장히 어색하네요. 쉽게 말하면 속성이 값 자체를 가지고 있는지, 혹은 어떠한 연산을 수행한 뒤 그 결과를 반환하는지의 차이입니다.

우리가 지금까지 정의하고 사용한 `name`, `age`와 같은 속성들은 모두 Stored Property입니다. Computed Property는 `get`, `set`을 사용해서 정의할 수 있습니다. `set`에서는 새로 설정될 값을 `newValue`라는 예약어를 통해 접근할 수 있습니다.

```swift
struct Hex {
    var decimal: Int?
    var hexString: String? {
        get {
            if let decimal = self.decimal {
                return String(decimal, radix: 16)
            } else {
                return nil
            }
        }
        set {
            if let newValue = newValue {
                self.decimal = Int(newValue, radix: 16)
            } else {
                self.decimal = nil
            }
        }
    }
}

var hex = Hex()
hex.decimal = 10
hex.hexString // "a"

hex.hexString = "b"
hex.decimal // 11
```

위 코드에서 `hexString`은 실제 값을 가지고 있지는 않지만, `decimal`로부터 값을 받아와 16진수 문자열로 만들어서 반환합니다. `decimal`은 Stored Property, `hexString`은 Computed Property입니다.

참고로, `get`만 정의할 경우에는 `get` 키워드를 생략할 수 있습니다. 이런 속성을 *읽기 전용<sup>Read Only</sup>*이라고 합니다.

```swift
class Hex {
    // ...

    var hexCode: String? {
        if let hex = self.hexString {
            return "0x" + hex
        }
        return nil
    }
}
```

`get`, `set`과 비슷한 `willSet`, `didSet`을 이용하면 속성에 값이 지정되기 직전과 직후에 원하는 코드를 실행할 수 있습니다.

```swift
struct Hex {
    var decimal: Int? {
        willSet {
            print("\(self.decimal)에서 \(newValue)로 값이 바뀔 예정입니다.")
        }
        didSet {
            print("\(oldValue)에서 \(self.decimal)로 값이 바뀌었습니다.")
        }
    }
}
```

마찬가지로, `willSet`에서는 새로운 값을 `newValue`로 얻어올 수 있고, `didSet`에서는 예전 값을 `oldValue`라는 예약어를 통해 얻어올 수 있습니다.

`willSet`과 `didSet`은 일반적으로 어떤 속성의 값이 바뀌었을 때 UI를 업데이트하거나 특정 메서드를 호출하는 등의 역할을 할 때에 사용됩니다.
