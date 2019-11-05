# Chapter 2. The TDD Cycle

1장에서 배웠듯이 TDD Cycle이 있다는 걸 배웠잖아
코드의 색상화가 되는 4가지 단계가 있음. 
1. Red: 앱 코드를 작성하기 전에 실패한 테스트 작성.
2. Green : 최소 코드를 작성하여 test pass
3. Refactor: 앱과 테스트 코드 정리
4. Repeat: 모든 기능이 구현될 때 까지 이 cycle을 다시 수행.
이것을 Red-Green-Refactor Cycle이라구 한다. 

다들 아시다시피, Xcode상에서 테스트에 실패하면 빨간색으로 x표시가 뜨고 성공하면 녹색으로 체크표시가 떠서 저렇게 Red-Green으로 말한거 ㅇㅇ

챕터 2에서는 간단한 cash register를 만듬.
> playground에서도…테스트 할 수 있구나..

그럼 일단 TDD Cycle체 맞게 실패하는 테스트를 작성해야함.

### Red: Write a failing test 

```swift
class CashRegisterTests: XCTestCase {
    
}
```
> 거의 대부분의 경우 XCTest 프레임워크의 일부인 XCTestCase의 하위 클래스로 테스트.

```swift
CashRegisterTests.defaultTestSuite.run()
```

이게  플레이그라운드에서 테스트 케이스들을 전부 실행시켜주는 커맨드인가봄

> 테스트 이름에 대한 규칙에 대해 설명
> XCTest: 모든 테스트 메소드들은 “test”로 시작해야함.
> test: 테스트 할 메소드 이름을 따른다. 
> 특별한 설정이 필요한 경우, 언더바 뒤에 온다. But 테스트는 이것을 포함하지 않음. 
> 마지막으로 예상 결과. 여기서는 createsCashRegister()를 의미. 

테스트 이름을 이런식으로 지정하면 문제를 신속하게 확인 가능.

지금은 테스트 실패인데, 

```swift
func testInit_createsCashRegister() {
      // 2
      XCTAssertNotNil(CashRegister()) // CashRegister가 아직 없음. 
    }
```
TDD에서 컴파일 실패는 테스트 실패를 의미.<p>
**그러므로 우리는 TDD Cycle중 Red단계를 완료한것!!!!!**

### Green: Make the test pass 
여기서는 위에서 말했듯이 테스트를 통과하기 위한 **최소한의** 코드만 작성해야함.<p>
최소한 보다 더 많은 코드를 작성하면 테스트코드가 앱 코드 뒷전이 되는거임 ㅇㅇ<p>
이 컴파일 에러를 해결하기 위해 작성 할 수 있는 최소한의 코드는 ?<p>
CashRegister를 정의하는 것 ㅇㅇ

CashRegister를 정의하고 플레이그라운드를 실행하면 테스트를 패스하게 된다. <p>
**즉 Green 단계 완료.**

### Refactor: Clean up your code 
이제 다음단계인 Refactor단계에 왔는데요. 여기서 뭐하랬ㅈㅣ?<p>
앱 코드와 테스트코드 모두 정리ㅇㅇ

여기서 리팩토링 할 수 있는 사항을 찾아보자.
- **중복되는 로직** : 중복을 제거하기 위해 프로퍼티, 메소드 또는 클래스를 가져올 수 있는가?
- **Comments** : 주석은 코드가 수행되는 방식이 아니라, 왜 수행되는지 이류를 설명해야함. 즉, 코드 작동 방식을 설명하려는 주석을 제거하자. 큰 메소드를 (이름을 잘 지어서) 여러 메소드로 나누고, 프로퍼티와 메소드의 이름을 보다 명확하게 하고..등등을 해야힘.
- **코드 냄새** : 때로는 특정 코드 블록이 단순히 잘못된 것처럼 보임. 즉 냄새가 난다는거 ㅇㅇ 우리의 직감을 믿고 이러한 코드 냄새를 없애야함. 예를들어 너무 많은 전제? 가정을 하고 있거나 하드코딩된 문자열, 또는 다른 문제가 있는 로직이 있을 수 있음. 이것도 위에서 한거랑 똑같이 적용가능. 프로퍼티와 클래스를 끌어내고, 이름을 바꾸고, 코드를 재구성하면 이러한 문제 해결 가능.

우리는 리팩터 단계를 마쳤고 다음 단게 ㄱㄱ

### Repeat: Do it again 

사실상 3단계니까?<p>
우리는 지금 첫번째 Cycle을 완료한 거~~<p>
이제 할일들을 추가하면서 계속 이 사이클을 돌면됨.<p>
지금 우리가 할 수 있는건<p>
- 이니셜라이저 작성.
- addItem같ㅇ은 메소드 작성.
- acceptPayment 메소드 작성.

### TDDing init(availableFunds:) 
자 다시 TDD Cycle을 돌려봅시다.<p>
먼저 Red! 실패하는 테스트를 작성해보자.

```swift
func testInitAvailableFunds_setsAvailableFunds() {
        // given
        let availableFunds = Decimal(100)
        // when
        let sut = CashRegister(availableFunds: availableFunds)
        // then
        XCTAssertEqual(sut.availableFunds, availableFunds)
    }
```

위 코드에서 눈여겨 볼 것은 <p>
**Given, when, then이라는 주석이 들어갔다는 점.**<p>
    
이 테스트는 아까의 테스트보다는 복잡하므로 이렇게 세부분으로 나눠서 생각하면 좋음.

- Given은 특정 조건이 주어지면.
- When은 어떤 행동이 일어날 때
- Then은 예상 결과가 발생. 

*sut*은 테스트 중인 시스템을 나타냄. TDD에서 사용되는 매우 일반적인 이름이라고 해요?<p>
지금은 CashRegister(availableFunds:) 이니셜라이저가 없으니까 당연히 컴파일 에러가 날거고 이걸 고쳐봅시더<p>

아까 정의”만” 해놓은 CashRegister를
```swift
class CashRegister {
    
    var availableFunds: Decimal
    init(availableFunds: Decimal = 0) {
      self.availableFunds = availableFunds
    }
}

```
로 고치자!<p>
그럼 이제 컴파일 에러는 사라지고 런 해보면 테스트 패스함.<p>
Green단계 완료!<p>

다음 단계는 앱코드와 테스트코드를 정리하는 단계.<p>
아까 처음으로 테스트 추가한거 보면<p>
    
```swift
func testInit_createsCashRegister() {
        // 2
        XCTAssertNotNil(CashRegister())
    }
```
이걸 추가했었는데, 우리는 init()메소드가 따로 없고,  init(availableFunds: )가 있음 <p>
그니까 삭제.<p>

그럼 이제 테스트 코드를 정리했고..앱코드 정리를 해보자.
```swift
class CashRegister {
    
    var availableFunds: Decimal
    init(availableFunds: Decimal = 0) {
      self.availableFunds = availableFunds
    }
}

```
보면 이니셜라이저가 availableFunds에 기본값을 0으로 주고 있음. 그래서 아까 
```swift
func testInit_createsCashRegister() {
        // 2
        XCTAssertNotNil(CashRegister())
    }
```
이것도 에러가 안났던것.

근데 지금 availableFunds에 기본값으로 0을 주는게 합리적인가? 말이 되는가?를 생각해봐야함. 
- 만약 기본 값을 유지한다면, availableFunds가 예상 기본값으로 설정되어있는지 확인하는 테스트를 추가할 수 있음.
- 기본값을 유지하지 않는다면? 제거해야지;
우리는 지금 기본값을 갖는게 의미가 없다고 가정해보자.<p>
그럼 뭐랬지? 삭제.

```swift
class CashRegister {
    
    var availableFunds: Decimal
    init(availableFunds: Decimal) {
      self.availableFunds = availableFunds
    }
}
```
삭제하자.<p>

이제 리팩터 단계는 끝났고, 다음 TDD Cycle로 넘어가보자.

### TDDing addItem 
항상 그렇듯이 먼저 실패한 테스트를 작성해야겠찌???

```swift
func testAddItem_oneItem_addsCostToTransactionTotal() {
  // given
  let availableFunds = Decimal(100)
  let sut = CashRegister(availableFunds: availableFunds)
  let itemCost = Decimal(42)
  // when 
  sut.addItem(itemCost) // error
// then 
  XCTAssertEqual(sut.transactionTotal, itemCost) // error
}

```
지금 컴파일 에러가 나는데, ㅇㅣ유는 addItem메소드와 transactionTotal프로퍼티가 앖기때문.<p>

암튼 실패하는 테스트를 작성했고, 다음 Green단계로 넘어가보자<p>

테스트를 패스하도록 만들기 위해 최소한의 코드를 작성해보자.

```swift
class CashRegister {
    
    var availableFunds: Decimal
    var transactionTotal: Decimal = 0
    init(availableFunds: Decimal) {
      self.availableFunds = availableFunds
    }
     func addItem(_ cost: Decimal) {
      transactionTotal = cost
    }
}
```
다음 단계인 리팩터로 가보자.

```swift
func testAddItem_oneItem_addsCostToTransactionTotal() {
      // given
      let availableFunds = Decimal(100)
      let sut = CashRegister(availableFunds: availableFunds)
      let itemCost = Decimal(42)
      // when
      sut.addItem(itemCost)
    // then
      XCTAssertEqual(sut.transactionTotal, itemCost)
    }
    
    func testInitAvailableFunds_setsAvailableFunds() {
        // given
        let availableFunds = Decimal(100)
        // when
        let sut = CashRegister(availableFunds: availableFunds)
        // then
        XCTAssertEqual(sut.availableFunds, availableFunds)
    }
```
아까 리팩터 단계에서 중복된 로직 이런걸 제거할 수 있다고 말했는데, 지금 위 두 테스트를 보면 중복된 로직이 있는 것을 볼 수 있음.

바로

```swift
      let availableFunds = Decimal(100)
      let sut = CashRegister(availableFunds: availableFunds)

```
이부분의 중복을 제거하기 위해<p>
CashRegisterTests내에 변수를 정의한다. 
    
```swift
class CashRegisterTests: XCTestCase {
    
   var availableFunds: Decimal!
    var sut: CashRegister!
```

여기서 알고가야 할 사실!
setup()과 tearDown메소드가 있는데, setup은 각 테스트 메소드가 실행되기 직전에 호출되며 tearDown은 각 테스트 메소드가 완료된 직후에 호출된다. 이러한 메소드들은 중복된 로직을 위치하기에 완벽한 장소 ㅇㅇ

```swift
// 1
    override func setUp() {
        super.setUp()
        self.availableFunds = 100
        self.sut = CashRegister(availableFunds: availableFunds)
    }
    // 2
    override func tearDown() {
        self.availableFunds = nil
        self.sut = nil
        super.tearDown()
    }
```

1. setup()내에서 super.setup()을 호출하여 슈퍼클래스에세 설정을 수행하도록 함. 그다음에 할 작업 하기
2. tearDown에서 반대의 작업을 수행한다. 먼저 변수들의 메모리에서 해제시켜주고 마지막에 super.tearDown()을 호출해준다. setup()에서 설정한 모든 프로퍼티가 해제되어야함. 이는 XCTest프레임워크의 작동방식 때문. 테스트 target내에서 각 XCTestCase서브클래스를 인스턴스화하고 모든 테스트 케이스가 실행될때까지 릴리즈 하지 않음. 따라서 많은 테스트 케이스가 있고 tearDown내에서 프로퍼티를 nil로 설정하지 않으면 프로퍼티의 메모리가 필요 이상으로 길게 유지될 수 있음. 또한 테스트 케이스가 충분히 많으면 테스트를 실행 할 때 메모리 및 성능 문제가 발생 할 수 있음

암튼 지금 중복된 로직을 setup으로 옮겼기 때문에

```swift
func testAddItem_oneItem_addsCostToTransactionTotal() {
        // given
        let itemCost = Decimal(42)
        // when
        sut.addItem(itemCost)
        // then
        XCTAssertEqual(sut.transactionTotal, itemCost)
    }
    
    func testInitAvailableFunds_setsAvailableFunds() {
    
        XCTAssertEqual(sut.availableFunds, availableFunds)
    }
```

이렇게 리팩터 단계가 끝나고 이제 다음 TDD Cycle로 가보자.

### Adding two items 

testAddItem_oneItem_addsCostToTransactionTotal는 하나의 item에 대해 addItem패스를 확인하지만 2개에대해서는 전달할수도 있고 안할수도..아직 모름
이것을 테스트 해보자.

```swift
func testAddItem_twoItems_addsCostsToTransactionTotal() {
  // given
  let itemCost = Decimal(42)
  let itemCost2 = Decimal(20)
  let expectedTotal = itemCost + itemCost2
// when 
  sut.addItem(itemCost)
  sut.addItem(itemCost2)
// then 
  XCTAssertEqual(sut.transactionTotal, expectedTotal)
}

```
먼저 실패하는 테스트 작성.<p>
위 테스트를 돌려보면 당연히 실패하는데, expectedTotal은 42 + 20인데, addItem을 2번하고 난 결과 transactionTotal는 20임 
왜냐면

```swift
class CashRegister {
    
    var transactionTotal: Decimal = 0

    func addItem(_ cost: Decimal) {
        transactionTotal = cost
    }
}
```
transactionTotal에 그냥 cost를 바로 대입하고 있기 때문에. 우리 테스트를 통과하려면
```swift
func addItem(_ cost: Decimal) {
        transactionTotal += cost
    }
```
이렇게 더해줘야함. 이렇게 최소한의 코드로 테스트틀 패스하게 했으니 Green 단계 완료.<p>
다음 리팩터 단계로 가자.

```swift
func testAddItem_twoItems_addsCostsToTransactionTotal() {
  // given
  let itemCost = Decimal(42)
  let itemCost2 = Decimal(20)
  let expectedTotal = itemCost + itemCost2
// when 
  sut.addItem(itemCost)
  sut.addItem(itemCost2)
// then 
  XCTAssertEqual(sut.transactionTotal, expectedTotal)
}

```
여기서 itemCost가 중복되고 있음. <p>

CashRegisterTests 안에
```swift
    var itemCost: Decimal!
```
프로퍼티 정의. Setup 및 tearDown에 잘 해주고
```swift
func testAddItem_twoItems_addsCostsToTransactionTotal() {
      // given
      let itemCost2 = Decimal(20)
      let expectedTotal = itemCost + itemCost2
       
    // when
      sut.addItem(itemCost)
      sut.addItem(itemCost2)
    // then
      XCTAssertEqual(sut.transactionTotal, expectedTotal)
    }
    
    func testAddItem_oneItem_addsCostToTransactionTotal() {

        // when
        sut.addItem(itemCost)
        // then
        XCTAssertEqual(sut.transactionTotal, itemCost)
    }
```
이렇게 itemCost를 정의하던 부분을 지울 수 있음. <p>
또 중복된 로직을 찾아보자면 
    
```swift
        sut.addItem(itemCost)
```

이 부분! 이 부분도 지금 중복인데 그럼 이부분도 setup으로 옮겨야 할까? <p>
안됨.
왜냐면 아까 말했듯이 setup은 각 테스트케이스가 시작하기 전에 호출되는데 addItem이 필요없는 다른 테스트를 작성할 수 있음. 따라서 얘를 setup으로 옮겨서는 안되고 그대로 둬야한다. 
