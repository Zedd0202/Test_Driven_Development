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
playground에서도…테스트 할 수 있구나..

그럼 일단 TDD Cycle체 맞게 실패하는 테스트를 작성해야함.

### 	Red: Write a failing test 

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
TDD에서 컴파일 실패는 테스트 실패를 의미. 그러므로 우리는 TDD Cycle중 Red단계를 완료한것!!!!!

### Green: Make the test pass 
여기서는 위에서 말했듯이 테스트를 통과하기 위한 “최소한의” 코드만 작성해야함.
최소한 보다 더 많은 코드를 작성하면 테스트코드가 앱 코드 뒷전이 되는거임 ㅇㅇ
이 컴파일 에러를 해결하기 위해 작성 할 수 있는 최소한의 코드는 ?
CashRegister를 정의하는 것 ㅇㅇ

CashRegister를 정의하고 플레이그라운드르 ㄹ실행하면 테스트를 패스하게 된다. 
즉 Green 단계 완료.

### Refactor: Clean up your code 
이제 다음단계인 Refactor단계에 왔는데요. 여기서 뭐하랬ㅈㅣ?
앱 코드와 테스트코드 모두 정리ㅇㅇ

여기서 리팩토링 할 수 있는 사항을 찾아보자.
- 중복되는 로직 : 중복을 제거하기 위해 프로퍼티, 메소드 또는 클래스를 가져올 수 있는가?
- Comments : 주석은 코드가 수행되는 방식이 아니라, 왜 수행되는지 이류를 설명해야함. 즉, 코드 작동 방식을 설명하려는 주석을 제거하자. 큰 메소드를 (이름을 잘 지어서) 여러 메소드로 나누고, 프로퍼티와 메소드의 이름을 보다 명확하게 하고..등등을 해야힘.
- 코드 냄새 : 때로는 특정 코드 블록이 단순히 잘못된 것처럼 보임. 즉 냄새가 난다는거 ㅇㅇ 우리의 직감을 믿고 이러한 코드 냄새를 없애야함. 예를들어 너무 많은 전제? 가정을 하고 있거나 하드코딩된 문자열, 또는 다른 문제가 있는 로직이 있을 수 있음. 이것도 위에서 한거랑 똑같이 적용가능. 프로퍼티와 클래스를 끌어내고, 이름을 바꾸고, 코드를 재구성하면 이러한 문제 해결 가능.

우리는 리팩터 단계를 마쳤고 다음 단게 ㄱㄱ

### Repeat: Do it again 
사실상 3단계니까?
우리는 지금 첫번째 Cycle을 완료한 거~~
이제 할일들을 추가하면서 계속 이 사이클을 돌면됨.
지금 우리가 할 수 있는건
- 이니셜라이저 작성.
- addItem같ㅇ은 메소드 작성.
- acceptPayment 메소드 작성.

### 	TDDing init(availableFunds:) 
자 다시 TDD Cycle을 돌려봅시다.
먼저 Red! 실패하는 테스트를 작성해보자.







