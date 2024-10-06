# 레벨 1
- ## 1. Swift에서 옵셔널이란 무엇이며, 언제 사용해야 하나요?
  - 값이 있을수도 있고 없을 수도 있는 상황을 안전하게 다룰수 있게 해주는 개념
  - ### 옵셔널 바인딩과 강제 언래핑의 차이점은 무엇인가요?
    - 옵셔널 바인딩이란 옵서녈 포장지를 벗겨 값을 추출하는 과정이다. 옵셔널의 값이 존재하는지를 검사한 뒤, 존재한다면 그 값을 다른 변수에 대입시켜줍니다.
    ```swift
    if let email = optionalEmail {
      print(email) // optionalEmail의 값이 존재한다면 해당 값이 출력됩니다.
    } // optionalEmail의 값이 존재하지 않는다면 if문을 그냥 지나칩니다.
    ```
    - 강제 언래핑은 옵셔널 값을 강제로 추출하는 방법으로 반드시 옵셔널 값이 있을 때에만 사용해야 한다.
    - 즉, nil 값을 처리할 때 옵셔널 바인딩은 값을 안전하게 처리할 수 있는 반면 강제 언래핑은 nil값일 경우 런타임 오류로 이어질 수 있어 안정성 측면에서 위험하다.
  - ### 옵셔널 체이닝의 동작 원리를 설정해주세요.
    - 옵셔널 체이닝이란 옵셔널을 연쇄적으로 사용하는 것이면, dot(.)을 통해 프로퍼티나 메서드에 옵셔널이 하나라도 붙어있으면 옵셔널 체이닝이라고 한다.
  - ### 암시적 언래핑 옵셔널을 사용하는 경우는 언제인가요?
    - 값이 항상 있다고 판단될 때 사용한다.
  - ### nil 병합 연산자(??)의 사용 예시를 들어주세요.
    ```swift
    let presentOrDefault = gitf ?? "기본 선물"
    ```
- ## 2. iOS 앱의 생명주기(App Life Cycle)에 대해 설명해주세요.
  - 앱 생명주기란 앱의 최초 실행 부터 앱이 완전히 종료 되기까지 앱이 가지는 상태와 그 상태들 사이의 전이를 뜻합니다.
  - ### 앱의 각 상태(Not Running, Inactive, Active, Background, Suspended)에서 할 수 있는 작업은 무엇인가요?
    - Not Running: 앱이 아예 실행되지 않았거나 시스템에 의해 종료되었을 때의 상태
    - Foreground: 앱이 실행되어 클라이언트에게 보여지고 있는 상태
    - Inactive: 앱이 실행되면서 Foreground에 진입하지만, 어떠한 이벤트도 받지 않는 상태. 앱의 상태 전환 과정에서 잠깐 머무는 단계(ex.배터리 부족 알림)
    - Active: 앱이 실제 실행중이고 사용자 이벤트를 받아서 상호작용 할 수 있는 상태. 바로 Active상태는 될 수 없으며 Inactive 상태를 거쳐서 Active 상태가 됩니다.
    - Background: 앱 실행 중 홈 화면으로 나가거나 다른 앱으로 전환되어 현재 앱이 클라이언트에게 보여지지 않는 상태
    - Running: 앱 실행 중 화면을 나가거나 다른 앱으로 전환이 되었지만 실질적으로는 앱이 실행중인 상태(ex.음악 앱을 키고 화면을 닫아도 음악이 나올 때)
    - Suspended: Background - Running 상태에서 특별한 작업이 없을 경우 Suspended 상태가 됩니다. Background상태에 있지만 아무 코드도 실행하지 않으며, 메모리상으로 올라가 있지만 배터리를 사용하지 않습니다. OS에 의해 메모리 부족현상이 발생하면 앱이 메모리에서 해제될 수 있다.
  - ### 앱 상태 변화에 따라 호출되는 AppDelegate 메서드들을 나열해주세요.
    - Not Running
      - application(_:willFinishLaunchingWithOptions:) 앱이 최초 실행될 때 호출되는 메서드
      - application(_:didFinishLaunchingWithOptions:) 앱이 실행된 직후 사용자의 화면에 보여지기 직전에 호출되는 메서드
      - applicationWillTerminate(_:) 앱이 종료되기 직전에 호출. 사용자 데이터등을 종료 전에 한번 더 저장해두는 것이 좋습니다.
    - Inactive
      - applicationWillEnterForeground(_:) 앱이 Active 상태가 되기 직전, 화면에 보여지기 직전에 호출되는 메서드
    - Active
      - applicationDidBecomeActive(:) -> sceneDidBecomeActive(:) 앱이 Active 상태로 전환된 직후 호출되는 메서드
      - applicationWillResignActive(:) -> sceneWillResignActive(:) 앱이 InActive 상태로 전환되기 직전에 호출되는 메서드
    - Background
      - applicationDidEnterBackground(:) -> sceneDidEnterBackground(:) 앱이 Background 상태로 전환된 직후 호출되는 메서드
      - applicationWillEnterForeground(:) -> sceneWillEnterForeground(:) 앱이 Active 상태가 되기 직전, 화면에 보여지기 직전에 호출되는 메서드
    - Suspended
      - Suspended 상태는 AppDelegate에서 직접 처리되지 않고, 앱이 Background 상태로 전환된 후 일정 시간이 지나면 시스템이 앱을 Suspended 상태로 전환합니다.
  - ### 백그라운드에서 작업을 완료하기 위한 방법들은 무엇이 있나요?
    - iOS 앱은 기본적으로 Foreground, 즉 사용자가 앱을 열어 활성화한 경우에만 작동합니다. 하지만 사용자가 홈으로 나가거나 앱을 전환하면 앱은 Background 상태로 실행 됩니다. iOS는 퍼포먼스 이유로 Background 실행시간을 제한 합니다. 이 제한된 시간안에 작업을 수행하려면 BackgroundTask를 사용하여 시간 제한을 늘릴 수 있습니다.
- ## 3. Storyboard와 XIB의 차이점은 무엇인가요?
  - XIB 파일은 개별적인 UI 컴포넌트를 설계하는데 사용됩니다. 하나의 XIB 파일에는 보통 하나의 View나 View Controller의 레이아웃이 들어갑니다. 즉, XIB 파일은 독립적인 UI 요소를 설계하는 데 적합합니다.
  - Storyboard는 여러 View Controller와 그 사이의 관계를 한 곳에서 시각적으로 설계할 수 있게 해줍니다. 하나의 Storyboard에서 앱의 전체적인 흐름을 정의할 수 있으며, 화면 간 전환 및 데이터 전달 등을 설정할 수 있습니다.
  - XIB는 화면 간 전환에 대한 개념이 없습니다. 화면 간의 전환을 직접 코드로 작성해야 합니다.
  - Storyboard는 화면 간의 전환(세그, Segue)을 시각적으로 설정할 수 있습니다. 이는 코드 작성 없이도 화면 전환과 데이터 전달이 가능하게 합니다.
  - ### Storyboard에서 세그를 사용하는 이유는 무엇인가요?
    - Segue는 Storyboard에서 화면 전환을 설정할 때 사용되는 객체입니다.
    - 화면 간 전환의 시각적 구성
    - 자동 데이터 전달
    - 코드 작성 최소화
  - ### Storyboard에서 참조(Storyboard Reference)의 장점
    - Storyboard Reference는 Storyboard를 모듈화하는 방법으로, 하나의 Storyboard를 여러 작은 Storyboard로 나누어 참조할 수 있게 해줍니다.
    - 모듈화된 UI 관리
    - 협업의 용이성
    - 재사용성
    - 성능 향상
  - ## 4. 뷰를 구현할 때 Storyboard와 Code로 구현되는 각각의 장단점은 무엇인가요?
    - Storyboard의 장점: UI 구성을 한눈에 확인할 수 있다. View에 어떤 속성과 값을 설정했는지 확인하기 쉽다.
    - Storyboard의 단점: Xcode메모리가 올라간다. 협업시 충돌 이슈 발생할 수 있다. 인터페이스빌드와 Storyboard간 연결을 추적하기 어려울 수 있다.
    - 코드 기반 UI의 장점: 스토리보드와 비교했을 때 가볍다. 협업시 충돌 위험도가 낮아진다. 스토리보드에 비해 View의 재사용성이 좋다.
    - 코드 기반 UI의 단점: View가 어떤 모습을 갖고 있을지 한눈에 파악하기 어렵다. View의 속성 및 기능을 숙지하고 있어야한다.
  - ## 5. Auto Layout을 사용하는 이유와 장점은 무엇인가요?
    - AutoLayout은 iOS 및 macOS 애플리케이션에서 다양한 화면 크기와 방향에 따라 사용자 인터페이스가 적절하게 배치되도록 하는 레이아웃 시스템입니다.
    - 다양한 화면 크기와 장치지원
    - 동적 컨텐츠 지원
    - 코드와 UI의 분리
    - 화면 회전에 대한 대응
    - 유지보수 및 확장성
    - ### 제약 조건의 우선순위는 어떤 역할을 하나요?
      - AutoLayout에서 제약 조건의 우선순위는 충돌 가능성을 해결하거나 특정 제약 조건이 다른 제약 조건보다 우선시되는 경우를 정의하는 데 사용됩니다.
      - 제약 조건 충돌 해결: 여러 제약 조건이 충돌하는 상황에서, 각 제약 조건의 우선순위를 설정해 시스템이 어떤 제약 조건을 더 우선적으로 적용할 지 결정하게 됩니다. 우선순위는 1에서 1000까지의 값으로 설정할 수 있으며, 기본값은 1000입니다.
      - 선택적 제약 조건: 특정 상황에서만 적용되길 원하는 제약 조건에는 낮은 우선순위를 설정할 수 있습니다. 예를 들어, 화면이 특정 크기 이상이 될 때만 제약 조건을 적용하고 싶다면 우선순위를 낮게 설정해 다른 제약 조건이 우선되도록 할 수 있습니다.
      - 제약 조건의 유연성 제공: 필수적이지 않은 제약 조건은 우선순위를 낮게 설정하여 레이아웃이 유연하게 변화할 수 있도록 합니다. 이는 특히 가변적인 콘텐츠나 여러 해상도 및 화면 비율을 지원할 때 유용합니다.
    - ### 스택뷰의 속성들을 설명해주세요.
      - Axis: 스택 뷰가 자식 뷰들을 배치하는 방향을 정의합니다. Horizontal은 수평으로, Vertical은 수직으로 뷰를 배치합니다.
      - Distribution: 스택 뷰 내의 자식 뷰들이 어떻게 분배될지를 설정합니다.
      - Alignment: 스택 뷰 내의 자식 뷰들이 어떻게 정렬될지를 설정합니다.
      - Spacing: 스택 뷰 내 자식 뷰들 간의 간격을 설정합니다. 고정된 값을 지정할 수 있으며, 이 값을 통해 뷰들 간의 거리를 조정할 수 있습니다.
      - LayoutMarings: 스택 뷰의 내부 여백을 설정하여 자식 뷰들이 스택 뷰의 경계로부터 일정한 거리를 유지하게 합니다.
    - ### 인터페이스 빌더에서 제약 조건 충돌을 해결하는 방법은 무엇인가요?
      - 충돌 원인 파악
      - 제약 조건 수정
      - 우선순위 조정
      - 내장된 자동 수정 기능 사용
      - 명시적인 크기와 위치 설정
  - ## 6. Swift에서 클로저란 무엇이며, 어떻게 사용하나요?
    - 클로저는 코드에서 일급 객체로 취급되는 함수의 일종입니다. 함수와 유사하게 코드 블록을 캡처하고 전달할 수 있지만, 이름이 없고 주변의 변수와 상수를 캡처할 수 있다는 점에서 함수와 구분됩니다. 클로저는 보통 함수나 메서드의 인수로 전달되어, 나중에 실행될 코드 블록을 정의하는 데 사용됩니다.
    - ### 클로저의 캡처 리스트는 어떤 역할을 하나요?
      - 클로저는 주위의 변수들을 캡처할 수 있습니다. 클로저는 그 클로저를 만든 순간에 존재하던 변수들을 기억하고 있다. 하지만, 이런 캡처된 변수들이 메모리에 계속 남아있게 만들 수도 있다. 그래서 필요하지 않은 변수가 메모리에 남아있지 않도록 관리한는 방법이 바로 캡처 리스트이다.
      - 캡처리스트는 클로저가 주변 환경에서 변수나 상수를 캡처할 때 그 변수나 상수가 어떻게 관리될지를 명시하는 데 사용됩니다. 클로저는 캡처한 변수나 상수를 strong참조로 캡처하는데, 이로 인해 메모리 누수가 발생할 수 있다. 이러한 문제를 해결하기 위해서 캡처 리스트를 사용하여 캡처할 변수의 참조 타입을 weak 또는 unowned로 지정할 수 있습니다.
      ```swift
      class MyClass {
        var value = 10
        func doSomething() {
          let closure = { [weak self] in // 캡처리스트로 캡처
            guard let strongSelf = self else { return }
            print(strongSelf.value)
          }
          Closure()
        }
      }
      ```
    - ### @escaping 클로저와 non-escaping 클로저의 차이점은 무엇인가요?
      - 클로저는 기본적으로 non-escaping입니다. 이는 클로저가 함수의 실행이 종료되기 전에 호출된다는 것을 의미합니다. 클로저가 함수의 범위를 벗어나서 실행될 필요가 없는 경우 non-escaping으로 동작합니다. @escaping 클로저는 함수의 실행이 종료된 후에도 호출될 수 있는 클로저입니다. 클로저가 비동기 작업과 같이 함수가 반환된 이후에 호출될 경우 @escaping으로 선언해야 합니다.
      ```swift
      func performAsyncTask(completion: @escaping () -> Void) {
          DispatchQueue.global().async {
              completion() // 함수가 반환된 후 클로저 호출
          }
      }
      ```
    - ### 트레일링 클로저(Trailing Clousre)문법은 언제 사용하면 좋나요?
      - 트레일링 클로저 문법은 함수 호출 시 클로저가 마지막 인수로 전달될 때 사용합니다.
      ```swift
      func performTask(completion: () -> Void) {
          completion()
      }

      performTask(completion: {
          print("Task Completed")
      })

      performTask {
          print("Task Completed")
      }
      ```
  - ## 7. iOS에서 델리게이트 패턴은 어떤 목적으로 사용되나요?
    - 델리게이트 패턴은 어떤 객체의 행동을 다른 객체에 위임하기 위해 사용되는 패턴입니다. iOS에서 자주 사용되며, 특정 객체가 해야 할 일을 다른 객체가 대신 처리하도록 할 수 있습니다. 이를 통해 코드의 재사용성을 높이고, 객체 간의 결합도를 낮출 수 있습니다.
    ```swift
    protocol CarDelegate {
        func engineDidStart()
    }

    class Car {
        var delegate: CarDelegate?
        func startEngine() {
            print("엔진이 켜놨습니다.")
            delegate?.engineDidStart()
        }
    }

    class Driver: CarDelegate {
        func engineDidStart() {
            print("운전자가 알림을 받았습니다. 자동차 엔진이 켜졌습니다.")
        }
    }
    let myCar = Car()
    let driver = Driver()

    myCar.delegate = driver
    myCar.startEngine()
    ```
    - ### 델리게이트 패턴과 콜백 함수의 차이점은 무엇인가요?
      - 콜백 함수와 델리게이트 패턴은 둘 다 비슷한 역할을 하지만 콜백 함수는 특정 작업이 끝났을 때 함수 자체가 호출되는 방식이다. 간단하고, 작은 작업을 처리할 때 유용하다.
      - 델리게이트 패턴은 객체 전체가 특정 작업을 대신 처리할 수 있게 해주는 패턴이다. 더 복잡한 작업이나 여러 종류의 작업을 할 때 유용하다.
    - ### 델리게이트 패턴과 옵저버 패턴의 차이점은 무엇이고 각각 어떨때 사용하면 좋나요?
      - 델리게이트 패턴은 한 객체가 다른 객체에게 특정 작업을 위임하는 경우에 사용한다. 델리게이트는 하나의 객체와 하나의 델리게이트가 존재한다.
      - 옵저버 패턴은 여러 객체가 특정 이벤트에 대해 관찰하고 있다가, 그 이벤트가 발생하면 모두에게 알리는 방식이다. 여러 객체가 동시에 변화나 상태를 관찰할 때 유용하다.
      - 델리게이트 패턴을 사용하면, 온도 업데이트를 처리하는 하나의 특정 객체만 존재.
      ```swift
      protocol TemperatureDelegate {
          func didUpdateTemperature(_ temperature: Int)
      }

      class WeatherStation {
          var delegate: TemperatureDelegate?
          func updateTemperature() {
              let newTemperature = 30
              delegate?.didUpdateTemperature(newTemperature)
          }
      }

      class Display: TemperatureDelegate {
          func didUpdateTemperature(_ temperature: Int) {
              print("현재 온도는 \(temperature) 입니다.")
          }
      }
      let station = WeatherStation()
      let display = Display()

      station.delegate = display
      station.updateTemperature()
      ```
      - 옵저버 패턴을 사용하면, 여러 객체가 온도 변화를 관찰하고, 업데이트 시 동시에 알림을 받을 수 있다.
      ```swift
      class WeatherStation {
          var observers = [Observer]()

          func addObserver(_ observer: Observer) {
              observers.append(observer)
          }
          func updateTemperature() {
              let newTemperature = 30
              for observer in observers {
                  observer.didUpdateTemperature(newTemperature)
              }
          }
      }
      protocol Observer {
          func didUpdateTemperature(_ temperature: Int)
      }

      class Display: Observer {
          func didUpdateTemperature(_ temperature: Int) {
              print("Display: 현재 온도는 \(temperature) 입니다.")
          }
      }

      class Logger: Observer {
          func didUpdateTemperature(_ temperature: Int) {
              print("Logger: 온도를 \(temperature)로 기록했습니다.")
          }
      }

      let station = WeatherStation()
      let display = Display()
      let logger = Logger()

      station.addObserver(display)
      station.addObserver(logger)
      station.updateTemperature()
      ```
    - ### 델리게이트 메서드에서 반환값을 사용하는 경우는 언제인가요?
      - 델리게이트는 단순히 알리는 역할뿐 아니라, 호출자에게 결과나 데이터를 돌려줄 수 있다.
      ```swift
      protocol RestaurantDelegate {
          func orderFood() -> String
      }

      class Restaurant {
          var delegate: RestaurantDelegate?
          func takeOrder() {
              if let order = delegate?.orderFood() {
                  print("주문이 접수되었습니다: \(order)")
              } else {
                  print("주문이 접수되지 않았습니다.")
              }
          }
      }

      class Customer: RestaurantDelegate {
          func orderFood() -> String {
              return "파스타"
          }
      }

      let restaurant = Restaurant()
      let customer = Customer()

      restaurant.delegate = customer
      restaurant.takeOrder()
      ```
  - ## 8. Swift의 기본 데이터 타입에는 어떤 것들이 있나요?
    - Int & UInt
      - Int와 UInt는 정수를 나타내는 가장 기본적인 Number 타입입니다.
      - Int는 +/- 부호를 포함한 정수를 의미하며 UInt는 양의 정수만을 포함한 정수를 나타냅니다.
    - Bool
      - 불리언은 참/거짓의 두가지중 하나만 값으로 가집니다.
    - Float와 Double
      - Float와 Double은 부동소수점을 사용하는 실수이며, 부동소수 타입이라고 합니다. 부동소수 타입은 정수 타입보다 훨씬 넓은 범위의 수를 표현할 수 있습니다. 스위프트에는 64비트 부동소수 표현을 하는 Double과 32비트 부동소수 표현을 하는 Float이 있습니다.
    - Character
      - Character는 말 그대로 문자를 의미합니다. 단 하나의 문자를 의미합니다.
    - String
      - String은 문자열의 나열, 즉 문자열입니다.
    - Any, AnyObject와 nil
      - Any는 스위프트이 모든 데이터 타입을 사용할 수 있다는 뜻입니다.
      - AnyObject는 모든 클래스 타입을 지칭하는 프로토콜입니다.
      - AnyObject는 클래스의 인스턴스만 수용 가능하기 때문에 클래스의 인스턴스가 아니면 할당할 수 없습니다.
      - nil은 값이 없음을 의미하는 키워드입니다.
    - ### 값 타입(Value Type)과 참조 타입(Reference Type)의 차이점을 설명해주세요.
      - 값 타입은 구조체, 열거형, 튜플등이 있습니다.
      - 값 타입은 stack영역에 실제 데이터가 저장됩니다. 때문에, 값을 전달 시 실제 데이터가 복사됩니다.
      - 참조 타입은 클래스, 클로저등이 있습니다.
      - 참조 타입은 heap영역에 실제 데이터가 저장되고, stack영역에는 heap영역 메모리 주소가 저장됩니다. 값의 전달은 인스턴스가 위치한 실제 주소(=heap 영역의 주소)의 복사입니다.
    - ### 구조체(Struct)와 클래스(Class)는 어떤 차이가 있나요?
      - 구조체는 값 타입이고, 구조체 변수를 새로운 변수에 할당할 때마다 새로운 구조체가 할당됩니다.
      - 즉 같은 구조체를 여러 개의 변수에 할당한 뒤 값을 변경시키더라도 다른 변수에 영향을 주지 않습니다.(값 자체를 복사)
      - 클래스는 참조 타입이고, ARC로 메모리를 관리합니다. 같은 클래스 인스턴스를 여러 개의 변수에 할당한 뒤 값을 변경시키면 할당한 모든 변수에 영향을 줍니다.(메모리만 복사)
      - 클래스는 상속이 가능하고, deinit을 사용하여 클래스 인스턴스의 메모리 할당을 해제할 수 있습니다.
    - ### 열거형(Enum)의 원시값(Raw Value)과 연관값(Associated Value)은 무엇인가요?
      - 열거형은 관련된 값의 그룹을 위한 타입을 정의하고, 코드에서 type-safe 방법으로 값을 동작하게 한다. type-safe란 값에 대해 타입을 명확하도록 도와주고, 잘못된 타입의 값이 전달되는 것을 막아주는 것을 말한다.
      - 열거형을 사용하면, 미리 정의해둔 타입의 케이스에서 벗어날 수 없으므로 코드의 가독성과 안정성이 높아진다.
      ```swift
      enum Planet{
        case mercury, venus, earth, mars, jupiter, seturn, uranus, neptune
      }
      ```
      - 원시값은 열거형을 처음 정의할 때 미리 설정하는 값이다. 열거형의 케이스에 기본값을 제공하지 않아도 되지만, 필요하다면 열거형 케잇느느 모두 동일한 타입의 원시값으로 미리 채워질 수 있다. 원시값이 각 열거형 케이스로 제공된다면 그 값은 문자열, 문자 또는 정수 또는 부동 소수 타입일 수 있다. 각 원시값은 열거형 선언부 내에서 유일한 값이어야 한다.
      ```swift
      enum HTTPCode: Int {
        case OK = 200
        case SEE_OTHER = 303
        case NOT_FOUND = 404
        case SERVER_ERROR = 500

        func showStatus() -> String {
          switch self {
            case .OK: return "OK"
            case .SEE_OTHER: return "요구한 데이터를 변경하지 않음"
            case .NOT_FOUND: return "페이지를 찾을 수 없음"
            case .SERVER_ERROR: return "서버 긴급점검"
            }
        }
      ```
      - 원시값을 String으로 했을 때, 케이스에 원시값을 별도로 정해주지 않으면, 케이스와 문자열이 매칭된다.
      ```swift
      enum Gender: String {
        case man = "남성"
        case woman // "woman" 
        case nothing // "nothing"
      ```
      - 원시값을 Int로 설정, 각 케이스의 원시값을 별도로 정해주지 않으면, 기본적으로 0부터 증가하며 매칭. 위 케이스에 설정된 값이 있다면 그 값부터 차례대로 증가하며 매칭된다.
      ```swift
      enum HTTPCode: Int {
        case OK // 0
        case NO_PAGE // 1
        case NOT_FOUND = 404
        case SERVER_ERROR // 405
      ```
      - 연관값이란, 각 케이스와 함께 보다 구체적인 정보를 저장해서 사용하는 것이 유용할 때 사용한다. 이 추가적인 정보를 연관값이라 한다. 연관된 정보를 케이스에 추가적으로 저장하는 개념으로, 타입에 제한없이 자유롭게 정의 가능하다.
      ```swift
      enum Computer {
        case cpu(core: Int, ghz: Double)
        case ram(Int, String)
        case hardDisk(gb: Int)
      }

      var cpu1 = Computer.cpu(core: 6, ghz: 1.4)
      var cpu2 = Computer.cpu(core: 8, ghz: 2.4)
      var ram1 = Computer.ram(16, "DDR4")
      var ram2 = Computer.ram(8, "DDR3")
      ```
      - 하나의 열거형에서 원시값과 연관값을 동시에 사용하는 것은 불가능하다.
  - ## 9. Xcode에서 디버깅 시 자주 사용하는 기능들은 무엇이 있나요?
    - BreakPoint: 원하는 라인에서 실행중인 앱을 일시정지 하는 포인트
    - ### 중단점의 종류와 사용 방법을 설명해주세요.
      - 중단점에 작동 조건을 설정할 수 있다.(-> 특정 횟수 이상 반복한 후에 중단점이 작동하도록 설정가능)
      - 소스코드 이외의 부분에 브레이크 포인트 설정할 수 있다.(-> 오토레이아웃과 같은 소스코드 이외의 부분에도 브레이크 포인트를 설정할 수 있다.)
      - 예외(exception) 상황에 중단점 설정할 수 있다.
      - 런타임 이슈에 중단점 설정할 수 있다.
      - 중단점에 액션을 추가할 수 있다.
    - ### LLDB 콘솔에서 자주 사용하는 명령어는 무엇인가요?
      - Help: 커맨드 명령어에 대한 나열 및 설명
      - Apropos: 검색 기능과 같이 관련 키워드를 검색하여 원하는 명령어를 찾는 명령어
      - Breakpoint: 문제 발생되는 지점을 탐색해 멈춘 후 조건변경을 하며 테스트를 하기 위한 명령어
      - command: 브레이크 시 --command(-C) 옵션을 통해 원하는 커맨드 실행 가능
      - AutoContinue: -G1 옵션을 통해 커맨드 실행 후 브레이크 탈출해서 프로그램 자동 진행하게 해줌
      - List: 현재 브레이크포인트 잡힌 리스트를 보여줌
      - Delete: breakpoint delete 번호로 브레이크포인트 삭제
      - Enable/Disable: breakpoint disable / enable 번호로 브레이크포인트 활성/비활성화
    - ### 조건부 중단점은 어떤 경우에 사용하면 좋나요?
      - 루프를 일정 횟수 반복한 후에 결과를 검토하려는 경우.
  - ## 10. iOS 앱에서 데이터를 저장하는 방법에는 어떤 것들이 있나요?
    - UserDefaults: 간단한 설정 값 저장에 최적화
    - Keychain: iOS에서 제공하는 보안 저장소로, 사용자의 비밀번호나 인증 토큰 같은 중요한 정보를 안전하게 저장할 수 있습니다. Keychain에 저장된 데이터는 암호화되어 있으며, 앱을 삭제해도 데이터는 유지됩니다.
    - CoreData: iOS에서 제공하는 객체 그래프 관리 및 영구 저장소입니다. 복잡한 데이터 구조나 대량의 데이터를 관리할 때 사용됩니다. 데이터 모델을 시각적으로 설계할 수 있고, 관계 및 제약조건을 쉽게 설정할 수 있습니다.
    - ### UserDefaults의 사용 예시와 주의 사항을 설명해주세요.
      - 사용자가 설정에서 토글을 통해 어떤 설정을 바꾸는데 -> 화면을 나가도 이 설정이 계속 유지되어야 하는경우
      - UserDefaults를 사용하면 앱의 어느 곳에서나 데이터를 쉽게 읽고 저장할 수 있다.
      - 반면, 암호화되지 않아 보안이 필요한 데이터에는 부적합하다.
    - ### Keychain은 어떤 데이터를 저장하는 데 적합한가요?
      - Keychain은 보안이 필요한 데이터를 암호화하여 안전하게 저장해주는 데이터 베이스이다.
      - Keychain Services api를 사용하여 보안이 필요한 데이터를 암호화하고, 이 정보를 사용할 때 복호화하여 재사용하는 방식이다.
      - Keychain에서는 데이터가 암호화되어 저장되기 때문에 보안이 필요한 데이터에 적합하며 비밀번호나 OAuth 토큰 등 UserDefaults에 정보를 저장하려 할 때 보안 문제가 발생할 것 같은 정보들을 Keychain을 사용하여 저장하는데 유용하다.
      - 사용자가 정보를 삭제하지 않는 한 정보가 계속 남아있다.
    - ### CoreData와 SQLite의 차이점은 무엇인가요?
      - CoreData는 CloudKit을 사용하여 디바이스에 데이터를 유지 또는 cache 할 수도 있고, 데이터를 여러장치에 동기화하는 애플 프레임워크이다.(데이터베이스가 아님)
      - 주로 데이터의 구조가 복잡하거나 관계가 중요한 애플리케이션에서 사용되어 데이터 관리를 보다 객체 지향적으로 할 수 있다.
      - SQLite는 직접적인 데이터 베이스 파일 시스템으로 SQL 쿼리를 사용하여 데이터를 관리한다. 관계형 데이터베이스라는 것이 특징이며 CoreData에 비해 저수준의 작업이 가능하며, 데이터 베이스 관리에 좀 더 세밀한 제어가 필요한 경우 사용된다.
  - ## 11. Swift에서 프로토콜(Protocol)이란 무엇이며, 어떻게 사용하나요?
    - 프로토콜은 특정 작업이나 기능에 적합한 메서드, 속성, 그 외 필수요소의 청사진을 정의한다.
    - 프로토콜은 일급객체이다.(변수에 할당가능, 함수의 파라미터로 전달 가능, 반환값으로 사용 가능)
    - 단순히 무엇을 해야하는지, 무엇을 정의해야하는지에 대한 요구사항만을 담고, 구현은 프로토콜을 채택한 클래스, 구조체, 열거형에서 한다.
    ```swift
    protocol Music {
        func playPiano(title: String, time: Int)
        func sint(title: String)

        var name: String { get }
    ```
    - 프로토콜은 초기화하지 않은 변수와 실행구문이 없는 함수를 선언하고, 상수 let을 사용하지 않는다.
    - 왜냐하면, 프로토콜은 메서드나 변수의 이름과 타입만 정하기 때문에, 프로토콜 내 변수는 Computed Property만 가능하며, Computed Property는 실행할 때 초기화하기 때문에, 값이 변경된다라는 의미로 해석되기 때문이다.
    - ### 프로토콜의 요구 사항에는 어떤 것들이 있나요?
      - 프로퍼티를 프로토콜에 정의하면 var 키워드를 통해 정의를 해줘야 하고 읽기 전용으로 할지 읽기 쓰기 전용으로 할지는 프로토콜이 정해야 합니다.
      - 인스턴스 메서드, 타입 메서드 둘 다 요구할 수 있습니다.
      - 값 타입의 인스턴스 메서드는 자기 자신의 인스턴스에 있는 내부의 값을 변경하려고 할 때 메서드의 func 키워드 앞에 mutating 키워드를 적어 내부의 값을 바꾼다고 알려준다.
    - ### 프로토콜 확장(Protocol Extension)을 사용하는 이유는 무엇인가요?
      - 프로토콜 역시 타입이기 때문에 extension을 활용하여 확장할 수 있다.
      - 문법적으로는 프로토콜의 구현을 추가하지만 실제로는 프로토콜을 채용한 타입의 구현이 추가된다고 보면 된다.
      ```swift
      protocol SayText {
          var text: String { get set }
          func say()
      }

      extension SayText {
          func say() {
              print(text)
          }
      }

      struct A: SayText {
          var text = "프로토콜 확장"
      }

      let a = A()
      a.say()
      ```
      - 구조체 A에서는 프로토콜에 정의된 say() 메소드를 구현하지 않았는데 에러가 없다. 확장을 통하여 say 메서드를 구현해줬기 때문에 프로토콜의 요구사항을 충족시키기 때문이다.
      ```swift
      protocol SayText {
          var text: String { get set }
          func say()
      }

      extension SayText {
          func say() {
              print(text)
          }
      }

      struct A: SayText {
          var text = "프로토콜 확장"
          func say() { // say 메서드 구현
              print("중복은 가볍게 무시")
          }
      }

      let a = A()
      a.say()
      ```
      - 메서드를 직접 구현해도 중복으로 인한 에러는 발생하지 않는다.
      - 타입에서 직접 구현한 멤버가 확장을 통해 구현한 멤버보다 높은 우선순위를 가지고 있기 때문이다.
    - ### 프로토콜 지향 프로그래밍(Protocol-Oriented Programming)의 장점은 무엇인가요?
      - 여러 프로토콜을 채택할 수 있어 다중 상속과 유사한 특성을 제공한다. 클래스뿐만 아니라 구조체와 열거형에도 적용 될 수 있다. 이는 값 타입을 강화하고 불변성을 유지할 수 있는데 도움이 된다.
      - 테스트, 기능확장, 유지보수, 재사용성을 높이는데 도움이 된다.
  - ## 12. Swift의 접근 제어자(Access Control)에 대해 설명해주세요.
    - open: 가장 높은 수준의 접근 제어자로, 다른 모듈에서도 해당 클래스나 메서드를 서브클래싱하거나 오버라이딩 할 수 있습니다. class에만 접근 제어 선언이 가능하다.
    - public: open과 접근 제어 정도가 같으나 다른 모듈에서 서브클래싱하거나 오버라이딩 할 수 없습니다.
    - internal: 같은 모듈 내에서는 어디서든지 해당 요소들을 사용할 수 있습니다. 모듈 외부에서는 사용할 수 없습니다.
    - fileprivate: 같은 파일 내에서만 해당 요소들을 사용할 수 있습니다.
    - private: 해당 요소가 선언된 블록 내에서만 사용할 수 있습니다.
    - ### open과 public의 차이점은 무엇인가요?
      - open은 public보다 더욱 개방적인 접근수준을 지정합니다.
      - open은 서브클래싱하거나 오버라이딩이 가능하나, public은 제한된다.
    - ### 접근 제어자를 사용하는 이유는 무엇인가요?
      - 클래스 내부에 선언된 데이터를 보호하기 위해서이다.
    - ### 상속과 관련된 접근 제어자는 무엇이 있나요?
      - open, internal
  - ## 13. iOS 앱에서 네트워크 통신을 하는 방법에는 어떤 것들이 있나요?
    - URL Session, Alamofire 등이 있다.
    - ### URLSession의 주요 구성 요소를 설명해주세요.
      - URLSessionConfiguration: URLSession을 생성하기 위해서 필요한 요소이며, Configuration을 생성할 때는 URLSession 정책에 따라서 default, ephemeral, background 세 가지 형태로 생성한다.
        - DefaultSession: 기본적인 Session으로 디스크 기반 캐싱을 지원합니다.
        - Ephemeral Session: 어떠한 데이터도 저장하지 않는 형태의 세션입니다. 쿠키나 캐시를 저장하지 않는 정책을 가져갈 때 사용합니다.
        - BackgroundSession: 앱이 종료된 이후에도 통신이 이뤄지는 것을 지원하는 세션입니다. 앱이 백그라운드에 있는 상황에서 컨텐츠 다운로드, 업로드를 할 때 사용합니다.
      - URLSessionTask: Task 객체는 일반적으로 Session 객체가 서버로 요청을 보낸 후, 응답을 받을 때 URL 기반의 내용들을 받는 역할을 합니다.
        - Data Task: HTTP의 각종 메서드를 이용해 서버로부터 응답 데이터를 받아서 Data 객체를 가져오는 작업을 수행(Response 데이터를 메모리 상에서 처리)
        - Download Task: 서버로부터 데이터를 다운로드 받아서 파일의 형태로 저장하는 작업을 수행. 백그라운드 다운로드 지원(서버에서 응답으로 준 데이터를 파일에 저장해주는 task)
        - Upload Task: 애플리케이션에서 웹 서버로 Data 객체 또는 파일 데이터를 업로드하는 작업을 수행(데이터를 request body에 넣어서 서버에 업로드하는 task)
    - ###  네트워크 요청 시 에러 처리는 어떻게 하나요?
      - 네트워크 통신시 반환되는 ResponseCode에 따라서 적절하게 처리한다.
    - ### Alamofire와 같은 서드파티 라이브러리를 사용하는 이유는 무엇인가요?
      - 코드의 간소화, 가독성 측면에서 도움을 주고, 여러 기능을 구축하지 않아도 쉽게 사용할 수 있다.
      - 요청을 생성할 때 메서드 파라미터의 URL과 파라미터를 넘겨주면 내부에서 자동으로 URL의 파라미터를 매핑시켜준다.
  - ## 14. Swift의 옵셔널과 관련된 함수에는 어떤 것들이 있나요?
    - map: 옵셔널 값이 있을 때 특정함수를 적용하고, 그 결과를 새로운 옵셔널로 반환한다. 옵셔널의 값이 nil인 경우, map은 클로저를 실행하지 않고 그냥 nil을 반환한다.
    ```swift
    let optionalValue: Int? = 5
    let transformedValue = optionalValue.map { $0 * 2 }
    print(transformedValue) // optional(10)
    ```
    - flatMap: 옵셔널 값을 변환한 결과가 또 다른 옵셔널일 때, 이중 옵셔널을 평탄화하여 단일 옵셔널로 반환하는 기능을 제공합니다. flatMap을 사용하면 옵셔널의 중첩을 제거할 수 있습니다.
    ```swift
    let optionalValue: Int? = 5
    let transformValue = optionalValue.flatMap { value in
        return value > 0 ? String(value) : nil
    }

    print(transformedValue) // Optional("5")
    ```
    - compactMap: 주어진 클로저의 결과가 nil이 아닌 요소들만 포함하는 새로운 배열을 생성합니다. 즉, nil 값을 자동으로 걸러내고, 비어있지 않은 값만 반환합니다.
    ```swift
    let numbers = ["1","2","three","4","five"]
    let validNumbers = numbers.compactMap { Int($0) }
    print(validNumbers) // [1,2,4]
    ```
    - ### map()과 flatMap()의 차이점을 설명해주세요.
      - map은 변환 결과는 동일한 타입의 옵셔널 또는 컬렉션으로 반환됩니다. 또한 결과는 중첩되지 않습니다
      - flatMap은 변환 결과가 옵셔널일 경우, 이중 옵셔널을 평탄화하여 단일 옵셔널로 반환합니다. 중첩된 옵셔널을 제거하는데 유용합니다.
    - ### compactMap()은 어떤 경우에 사용하나요?
      - 옵셔널 배열에서 nil 값을 제거할 때 유용합니다.
    - ### 옵셔널 체이닝을 사용할 때 주의할 점은 무엇인가요?
      - 옵셔널 체이닝을 사용하면 각 단계에서 값이 nil일 경우 다음 단계로 진행되지 않으며 결과도 nil이 됩니다.
      - 옵셔널 체이닝 후 강제 언래핑(!)을 사용하면 nil일 경우 런타임 오류가 발생합니다.
  - ## 15. Git에서 브랜치(Branch)를 사용하는 이유와 장점은 무엇인가요?
    - 동시작업: 여러 사람이 동시에 프로젝트를 작업할 수 있도록 한다. 각자가 자신의 브랜치(독립된 영역)에서 작업을 하고, 이후에 변경 사항을 병합하여 하나로 통합할 수 있다.
    - 버전 이력 관리: 각 브랜치는 프로젝트의 특정 시점을 나타내는 커밋들의 연속이므로, 작업 이력을 관리하고 이전 상태로 쉽게 돌아갈 수 있다.
    - 기능 분리: 새로운 기능을 개발할 때 기존 코드에 영향을 미치지 않도록 별도의 브랜치에서 작업할 수 있다.
    - 안정성 유지: 메인 브랜치에서는 안정된 코드를 유지하고, 개별 브랜치에서는 새로운 기능 개발이나 기존 코드 수정을 진행함으로써 프로그램 전체의 안정성을 유지할 수 있다.
    - 테스트 및 배포: 각 브랜치에서 작업이 완료되면, 테스트를 거친 후 메인 브랜치에 병합하여 배포할 수 있다. 이를 통해 안정성을 유지하면서 효율적인 개발 및 배포를 진행할 수 있다.
    - ### 브랜치를 병합(Merge)하는 방법에는 어떤 것들이 있나요?
      - 3-way Merge: 각 브랜치에 커밋이 있는 경우, git merge 명령어를 사용하면 두 브랜치의 코드를 합쳐서 새로운 커밋을 만들어주는 방식이 바로 3-Way Merge 방식입니다. 이 경우 같은 파일에 대해 다른 변경사항이 있을 경우 충돌이 발생하게 됩니다.
      - Fast-Forward Merge: 기준이 되는 브랜치에는 신규 커밋이 존재하지 않고 다른 브랜치에만 커밋이 존재할 때 브랜치 병합을 하는 경우, 자동으로 Fast-Forward Merge가 이루어집니다. 새로운 커밋이 생기지 않고 HEAD의 위치만 변하게 됩니다.
    - ### 브랜치 전략(Git-Flow, GitHub-Flow 등)에 대해 설명해주세요.
      - git flow 방식은 master, developo, feature, release, hotfix 브랜치 종류를 가진다.
      - 신규 기능 개발을 위해 개발자는 develop 브랜치를 기준으로 한 feature 브랜치를 따서 작업을 진행한다.
      - 작업이 완료된 feature 브랜치는 develop 브랜치로 병합된다.
      - 다음 출시 버전을 위해 개발중인 develop 브랜치에서 release 브랜치를 따서 배포를 위한 준비를 한다.
      - 충분한 테스트 후에, 일정한 주기로 master 브랜치로 merge 하여 제품을 출시한다.
      - 상용 배포 이후, release 브랜치에서 미처 발견되지 못한 새로운 버그들은 hotfix 브랜치에 바로 반영합니다.
      - github flow는 쉽게 요약하면, 브랜치를 하나의 base브랜치 + base브랜치에 기능을 추가하기 위한 브랜치 두개만으로 운영하여 훨씬 간단하지만 빠르게 수정 배포할 수 있는 전략입니다.
  - ## 16. iOS 앱에서 코어데이터를 사용하는 이유는 무엇인가요?
    - 코어데이터는 객체 그래프 관리 프레임워크이다.(데이터 베이스가 아님)
    - 복잡한 SQL 문을 작성하지 않고도 데이터베이스와 상호작용 할 수 있도록 직관적이고 사용하기 쉬운 인터페이스를 제공한다.
    - ### 코어 데이터의 주요 구성 요소(Entity, Attribute, Relationship 등)를 설명해주세요.
      - Entity: 코어 데이터에 의해 관리되는 객체의 단위입니다. 클래스에 해당하며 데이터베이스의 schema와 유사합니다. 객체가 가지는 attribute들과, 다른 entity와의 관계(Relationship)들로 이루어 집니다.
      - Attribute: 객체가 가지는 데이터의 타입과 제약조건을 나타냅니다. entity가 클래스라면, attribute는 프로퍼티에 해당합니다.
      - Relationship: 서로 다른 Entity를 각자의 모델 계층에 추가해 사용하는 방법입니다.
    - ### 코어 데이터에서 데이터를 가져오는 방법(Fetch Request)에 대해 설명해주세요.
      - Core Data에 저장된 데이터를 가져오기 요청 작업을 위한 전용 property wrapper이다.
      - FetchRequest는 SwiftUI 뷰에 별도 로직 없이 직접 추가가 가능하다.
    - ### 코어 데이터 마이그레이션(Migration)은 언제 필요한가요?
      - 마이그레이션은 앱 개발 과정에서 data Model을 변경할 때의 기존의 Data와의 호환성을 유지하면서 새로운 Data Model로 이전하기 위한 과정이다. 앱을 개발하는 동안 새로운 속성이나 엔티티를 추가하거나 기존의 속성과 엔티티를 제거하거나 변경하는 경우가 있다. 이때 기존 사용자가 데이터가 새로운 Data Model과 호환될 수 있도록 이전해주어야한다.
  - ## 17. Swift의 high-order functions에 대해 설명해주세요.
    - 고차함수는 다른 함수를 인자로 받거나, 함수의 결과로 함수를 반환하는 함수를 의미합니다. 스위프트에서는 map, filter, reduce가 콜렉션 타입 내에 정의되어 있습니다.
    - ### map()과 compactMap()의 차이점은 무엇인가요?
      - map은 콜렉션 내부의 데이터를 가공하여 새로운 콜렉션을 생성합니다.
        ```swift
        let numbers = [1, 2,3, 4, 5]
        let numbersPlusOne = numbers.map({ $0 + 1 })
        ```
      - compactMap은 옵셔널 바인딩을 지원하는 map입니다.
      - nil 값을 제외한 새로운 콜렉션을 만들어낼 수 있습니다.
        ```swift
        let students: [String?] =  ["Mike", "Jane", nil, "John", nil]
        let greatStudents = students.compactMap({$0}).map({"Great" + $0})
        ```
    - ### filter()와 reduce()는 어떤 경우에 사용하나요?
      - filter()는 콜렉션 내부에서 조건에 맞는 데이터들만 골라 새로운 콜렉션을 생성합니다.
        ```swift
        let numbers = [1, 2, 3, 4, 5]
        let numberGreaterThanTwo = numbers.filter({ $0 > 2})
        ```
      - reduce()는 콜렉션 내부의 데이터들을 하나로 통합시킵니다. 다른 고차함수들과는 다르게 reduce()는 두 개의 인자를 받습니다. 첫번째 인자는 통합할 데이터의 초기값입니다. 첫번째 인자는 통합할 데이터의 초기값입니다. 두번째 인자는 클로저인데 , 이 클로저에서는 첫번째 파라미터는 바로 이전 값에 대한 통합된 데이터를 의미하고, 두번쨰는 이번에 새로 통합할 데이터를 의미합니다.
        ```swift
        let numers = [1, 2, 3, 4, 5]
        let numberSum = numbers.reduce(0, { $0 + $1 })
        let numberSumShortcut = numbers.reduce(0, +)
        ```
    - ### flatMap()을 사용하는 경우를 예시로 들어주세요.
      - FlatMap은 2차원 배열에 나우어져있는 데이터들을 1차원 배열로 합쳐주는 기능이 포함되어 있습니다.
      ```swift
      let students = [["Mike", nil], [nil, nil, "Jane"], ["John"]]
      let goodStudents = students.flatMap({$0})
      print(goodStudents) // [Optional("Mike"), nil, nil, nil, Optional("Jane"), Optional("John")]
      let greatStudents = students.flatMap({$0}).compactMap({$0})
      print(greatStudents) // ["Mike", "Jane", "John"]
      ```
  - ## 19. iOS 개발을 위한 라이브러리 관리도구(CocoaPods, Carthage, Swift Package Manaer)의 차이점과 사용법을 설명해주세요.
    - ### 1. CocoaPods
      - Swift와 Objc에 사용할 수 있는 중앙 집중식 종속성 관리자로 오픈소스입니다.
      - Ruby로 제작되어 있습니다.
      - Main Repository인 Spaces에 중앙화 되어있습니다.
      - Podfile에 사용할 라이브러리만 명시해주면 바로 사용이 가능합니다.
      - 모든 Apple 플랫폼을 지원합니다.
      - 터미널을 통해 설치 및 사용합니다.
    - ### 2. SPM
      - 3rd party tool이 아닌 1st party입니다.
      - 자체 빌드 시스템이 포함되어 있고, 소프트웨어의 구성과 테스트, 실행까지 포함하고 있습니다.
      - SPM은 내부 모듈에 사용되는 dependency를 자동으로 관리해주고, dependency를 추가 또는 변경할 때마다 pod install이라는 부가 작업을 하지 않아도 됩니다.

