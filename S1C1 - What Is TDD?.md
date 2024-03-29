# What Is TDD?


TDD는 다들 아시다시피 Test-driven development의 약자. <p>
TDD는 Test를 통해 많고 작은 변경을 반복적으로 수행하여 소프트웨어를 개발하는 반복적인 방법(iterative way)입니다.

4가지 스텝이 있는데,
1. 먼저 실패하는 테스트를 작성
2. 테스트를 pass하도록 만듬
3. 리팩토링
4. 반복.

이것이 TDD Cycle인데, 보시다시피 “실패하는” 테스트를 먼저 작성하고 그에 따라 개발이 이루어지기 때문에 **개발이 테스트에 의해 주도된다**고 할 수 있음.<p>
개발이 테스트에 의해 주도되기 때문에 코드를 철저하고 정확하게 테스트 가능. 

테스트를 먼저 작성하고, 프로덕션 코드를 작성하여 pass시키면 
- 프로덕션 코드가 테스트가능하고(testable)
- 개발 중 모든 요구사항을 충족하는지 확인이 가능.
또한 테스트는 프로덕션 코드의 도큐먼트 역할을 하며 작동방식을 설명할 수 있음.

### Why should you use TDD? 

그럼 왜 TDD를 사용해야하는지 의문이 드는데,<p>
**TDD는 소프트웨어가 미래에도 계속 잘 작동할 수 있는 가장 좋은 방법.** 임

근데 꼭 TDD가 아니어도 되잖아? 예를들어 
- 모든 프로덕션 코드를 작성한 다음 그에대한 테스트코드를 작성 할 수 있음.
- 테스트작성을 건너뛰고 수동으로(manually) 코드를 테스트 할 수도 있음.

이런것보다 TDD가 좋은 이유는??<p>
- 좋은 테스트는 앱이 예상대로 작동하는지 확인하는 테스트.
- 하지만 테스트를 위해 테스트를 작성하는것은 가치가 없음.

TDD는 다음과 같은 테스트 방법을 제공해서 좋다는데 함 보자

1. 첫번째 단계는 아까 봤듯이, “실패하는 테스트”를 작성하는 것. 실패할 수 없는 테스트는 그다지 유용하지 않으므로 “실패하는 테스트”는 꽤나 유용하게 사용될 수 있음(도큐먼트로서의 역할이라거나?)
2. 새 테스트를 작성하기 전에, 이전에 작성했던 다른 모든 테스트를 통과해야함. 이렇게 하면 계속 테스트를 반복할 수 있음. 작업중인 단일 테스트만 실행할게 아니라 지속적으로 모든 테스트를 실행할 것.
3. 모든 테스트를 자주 실행하면 테스트를 빠르게 실행할 수 있도록 해야함. 모든 테스트를 실행하는데는 몇”초”단위로 걸리며, 바람직한 숫자는 1초. 테스트를 돌리는데 너무 오래걸리면 사람들은 테스트를 실행하지 않을 것.
4. 리팩토링을 하면 프로덕션 코드와 테스트코드 모두 업데이트 됨. 이를 통해 테스트가 유지되며 지속적으로 최신 상태를 유지할 수 있음.
5. 프로덕션 코드와 테스트를 병렬로 반복하여 작성하면 코드를 테스트 할 수 있음. 코드를 완성한 후 테스트를 작성하면 프로덕션코드는 완전한 유닛테스트를 위해 약간의 리팩토링이 필요할 것.


아마 이까지 읽고도 TDD를 굳~이 따르지 않고 좋은 테스트를 작성 할 수 있다고 할 수 있음.
단기적으로는 아마 할 수 있을것이지만 장기적으로는 어렵다.<p> 
좋은 테스트를 작성하는것에 대해 **훈련**을 받아야함. 그것을 도와줄 수 있는게 TDD임. 


### 그럼 TDD를 한다고 했을때 무엇을 테스트 해야하는것이냐?

테스트 커버리지가 좋다고 해서 앱이 더 나은 테스트를 받고있다는것은 아님. 
테스트 해야할 것과 하지 말아야 할 것 이 있음.

### do’s and don’ts:
- 자동화된 방식으로 포착 할 수 없는 코드에 대한 테스트를 작성할 것. 여기에는 내가 작성하는 대부분의 코드가 포함됨.
-  생성된 코드에 대한 테스트를 작성하지 말 것. 
- 컴파일러가 포착할 수 있는 문제에 대해 테스트를 작성하지 말 것.
- 앱에서 사용하는 라이브러리, 프레임워크와 같은 종속성 코드에 대한 테스트를 작성하지 말것.(UIKit에 대한 테스트를 작성 하지 않듯이?) 하지만 프레임워크 작동 방식(어떤걸 말하는지 모르겠음)을 결정하기 위해 테스트를 작성하는 것은 유용 할 수 있음. 하지만 장기간 유지하면 x 
- 또다른 예외는 타사 코드가 예상대로 작동한다는 것을 증명하려는 “위생성(sanity) 테스트”. 이러한 종류의 테스트는 라이브러리가 완전히 안정적이지 않거나 신뢰할 수 없는 경우에 유용.

### 하지만.. TDD 너무 오래걸려!!
TDD의 가장 일반적인 불만은 **시간이 너무 오래걸린다**는 것임.
하지만 TDD도 익숙해지면 더 빨라질 것. <p>
사실 테스트를 전혀 하고 있지 않다고 해도, 궁극적으로 우리는 “더 많은” 코드를 작성하고 있음.<p>
TDD는 그냥 처음에 시간이 좀 걸릴뿐임.<p>
장기적으로 TDD를 추적하면 버그가 적은 유지관리 가능한 코드가 생성되기 떄문에 TDD를 따르지 않는 것보다 훨씬 적은 시간이 소요됨.

또한 버그가 프로덕션에 미치는 영향을 생각해볼 수 있는데, 문제가 발견되지 않는 기간이 길수록 부정적인 평가, 신뢰 또는 수익상실 등 비용이 비례해서 커짐. <p>
TDD를 수행하면 궁극적으로 앱을 버그로부터 보호하는데 도움이 됨. 

### 언제 TDD를 사용해야 하는거지?
TDD는 언제든지 사용할 수 있음! 그러나 TDD를 시작하는 방법과 장소는 프로젝트 상태에 따라 다름.<p>
예를들어 해커톤앱, 테스트 프로젝트 또는 임시로 앱을 만든다면 TDD가 말이 되는지 먼저 생각해야함.<p>
앱 버전이 한개뿐인 경우에는 TDD를 따르지 않거나, 중요하거나 어려운 부분에 대해서만 TDD를 수행 할 수 있음. 


