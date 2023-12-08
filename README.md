# iOSInterview
iOS 면접 질문 정리


# iOS
- ## Bounds와 Frame의 차이를 설명하시오.
  - frame과 bounds는 view의 위치와 크기를 나타낸다.
  - frame은 super view 좌표계에서 view의 위치와 크기를 나타낸다.
  - frame의 origin(x,y) 좌표는 super view의 원점을(0,0)으로 놓고, 원점으로부터 얼마나 멀어져있는지를 나타낸다.
  - frame의 size는 view 영역을 모두 감싸는 사각형의 크기이다.
  - bounds의 origin은 자신의 좌표계를 기준, 처음엔 (0,0)으로 초기화
  - bounds의 size는 view 자체의 영역을 나타냄
  - frame의 origin을 변경하면 subview도 그만큼 같이 움직인다.
  - bounds의 origin을 변경하면 내 view의 viewport좌표가 움직인다.
  - frame은 view의 위치와 크기를 나타낼 때 사용
  - bounds는 view를 회전한 후 view의 실제 크기를 알고싶을 때, view 내부에 그림을 그릴 때, scroll view에서 스크롤링 할 때 사용.
    
- ## 실제 디바이스가 없을 경우 개발환경에서 할 수 있는 것과 할 수 없는 것을 설명하시오.
  - 하드웨어
    - 가속도 센서, 가압계 센서, 주변광 센서, GPS 센서 기능 불가
    - 마우스로 터치를 하기에 두 손가락으로 하는 줌인, 줌아웃을 할 수 없음
    - 카메라 불가
    - 마이크 불가
    - 전화기능 불가
  - API
    - Apple의 푸시 알림 받기, 보내기 불가
    - 사진, 연락처, 캘린더에 엑세스하기 위한 개인 정보 보호 알림 지원안함
    - Handoff 기능 불가
    - MessageUI 기능 불가
  - 그 외
    - 맥의 성능이 아이폰보다 뛰어나 CPU나 메모리에 얼마나 부담되는지 알 수 없음
    - 네트워크 속도 체크 불가
    - 페이스 아이디는 직접 얼굴 인식이 안되지만 인식됨, 안됨 처리는 가능
- ## 앱의 콘텐츠나 데이터 자체를 저장/보관하는 특별한 객체를 무엇이라고 하는가?
  - UserDefaults
    - 애플에서 기본 제공됨
    - key-value 쌍으로 저장하는 인터페이스
    - 런타임 환경에서만 동작하면서 앱이 실행되는 동안 기본저장소에 접근해 데이터를 기록하고 가져오는 역할을 함
    - 대용량의 데이터보다 단일 데이터(ex 사용자 기본 설정, 로그인 여부 등)를 저장하는데 더 적합
    - 싱글톤 패턴으로 설계되어 앱 전체에 단 하나의 인스턴스만 존재
  - CoreData
    - 애플에서 기본 제공됨
    - UserDefaults와 비교하여 좀 더 방대하고 복잡한 데이터를 저장하는데 적합
    - DataModel을 생성한 후 Entity를 생성한다.
  - SQLite
    - 애플에서 기본 제공되는 것이 아닌 외부 라이브러리이며, 비교적 가벼운 데이터 처리가 필요할 때 적합
    - CoreData는 프레임워크인것에 반해 SQLite는 데이터베이스임
    - C언어로 작성되어 있어 매우 가벼움
    - 전체 데이터베이스를 디스크 파일 1개에 저장하고, 설정 자체가 매우 간편하기에 관리하기가 수월
    - iOS, Android, Linux, Window 등과 같이 다양한 운영체제에서 사용됨
  - Realm
    - 빠른속도이지만 용량이 큼
    - 설치가 쉽고 대용량의 데이터에 대해 무료로 사용 가능
    - 용량에 관계없이 속도와 성능이 유지됨
    - 코드가 짧고 간결함
    - 메인스레드에서 데이터의 읽기, 쓰기 작업 가능
  ```
  속도: Realm > CoreData > SQLite
  메모리 및 저장공간 사용: Realm > CoreData > SQLite
  ```
- ## 앱 화면의 콘텐츠를 표시하는 로직과 관리를 담당하는 객체를 무엇이라고 하는가?
  - UIViewController
    - UIKit 앱의 뷰 계층 구조를 관리하는 객체이다. 뷰의 사용자 상호 작용에 응답한다. 전체 인터페이스의 레이아웃을 관리한다. 앱에서 다른 ViewController를 포함한 다른 객체들과 조정을 한다. 데이터가 변경되면 뷰의 콘텐츠를 업데이트 할 수 있다.
- ## App thinning에 대해서 설명하시오.
  - 애플리케이션이 디바이스에 설치될 때, 앱 스토어와 운영체제가 디바이스의 특성에 맞게 설치되도록 하는 설치 최적화 기술을 의미한다.
  - 최소한의 디스크 사용과 빠른 다운로드를 제공한다.
  - 구성으로는 슬라이싱(Slicing), 비트코드(bitcode), 주문형 리소스(on-demand resource)가 있다.
  - 슬라이싱: 다양한 기기와 운영체제 버전에 대하여 여러 가지 app bundle의 변형(variants)을 생성하고 전달하는 과정
  - 비트코드: 비트코드는 컴파일된 프로그램의 중간표현(Intermediate Representation)이다.
  - 주문형 리소스: 이미지나 사운드 같은 리소스를 키워드로 태그할 수 있고, 태그별로 그룹을 요청할 수 있다.
- ## 앱이 foreground에 있을 때와 background에 있을 때 어떤 제약사항이 있나요?
  - foreground mode는 메모리 및 기타 시스템 리소스에 높은 우선순위를 가지며 시스템은 이러한 리소스를 사용할 수 있도록 필요에 따라 background 앱을 종료합니다.
  - background mode는 가능한 적은 메모리공간을 사용해야 합니다.(시스템 리소스 해제, 메모리에서 해제 후 데이터를 디스크에 작성) 사용자 이벤트를 받기 어렵고 공유 시스템 리소스를 해제하고 이미지 객체 참조 등 메모리 제한
- ## 상태 변화에 따라 다른 동작을 처리하기 위한 앱델리게이트 메서드들을 설명하시오.
  - 애플리케이션이 InActive 상태로 전환되기 직전에 홏출되는 applicationWillResignActive,
  - 애플리케이션이 백그라운드 상태로 전환된 뒤 호출되는 applicationDidEnterBackground,
  - 애플리케이션이 Active상태가 되기 전에 호출되는 applicationWillEnterForegroundm
  - 애플리케이션이 Active상태로 전환된 후 호출하는 applicationDidBecomeActive,
  - 애플리케이션이 종료되기 직전에 호출되는 applicationWillTerminate
- ## 앱이 In-Active 상태가 되는 시나오리를 설명하시오.
  - 1. 사용자가 앱을 실행한다: Not running >> In-Active >> Active
    2. 앱 실행 도중 홈버튼을 누른다: Active >> In-Active >> Background
    3. 앱을 다시 켠다: Background >> In-Active >> Active
    4. 앱이 백그라운드에 있다가 Suspended 상태로 전이: Active >> In-Active >> Background >> Suspended
       
    <img width="373" alt="스크린샷 2023-10-16 오후 5 28 38" src="https://github.com/duthd3/iOSInterview/assets/79510152/1f3246ea-0f54-4d4c-8bbf-4d6f3d3fa7d0">
- scene delegate에 대해 설명하시오.
  - iOS 13 이후 SceneDelegate가 등장하면서 AppDelegate는 Process Lifecycle과 Session Lifecycle을 담당하고, SceneDelegate는 UI와 관련된 Lifecycle을 담당하는 것으로 변경되었습니다.

- ## UIApplication 객체의 컨트롤러 역할은 어디에 구현해야 하는가?
  - UIApplicationMain 함수
- ## App의 Not running, Inactive, Active, Background, Suspended에 대해 설명하시오.
  - Not running : app이 실행되지 않은 상태.
  - Inactive : app이 실행중이지만 사용자로부터 event를 받을 수 없는 상태.
  - Active : app이 실제 실행중이고 사용자 event를 받아서 상호작용할 수 있는 상태.
  - background : 홈화면으로 나가거나 다른 app으로 전환되어 app이 보이지 않는 곳에서 코드를 실행하고 있는 상태.
  - suspended : 앱이 background 상태이며 앱이 메모리에 남아 있긴하나 코드를 실행하고 있지 않은 상태.
- ## iOS 앱을 만들고, User Interface를 구성하는데 필수적인 프레임워크 이름은 무엇인가?
  - UIKit
    - UIKit Framework는 Gesture 처리, Animation, 그림 그리기, 이미지 처리, 텍스트 처리 등 UserEvent 처리.
    - TableView, Slider, Button, TextField, Alert등 Application의 화면을 구성하는 요소 포함
    - UIResponder에서 파생된 클래스나 UserInterface에 과련된 클래스는 Application의 Main Thread(Main Dispatch Queue)에서만 사용해야 함
    - iOS, tvOS에 사용
    - UserInterface
      - View and Control: 화면에 콘텐츠 표시
      - View Controller: 사용자 인터페이스 관리
      - Animation and Haptics: 애니메이션과 햅틱을 통한 피드백 제공
      - Window and Screen: 뷰 계층을 위한 윈도우 제공
    - User Action
      - Touch, Press, Gesture: 제스처 인식기를 통한 이벤트 처리 로직
      - Drag and Drop: 화면 위에서 드래그 앤 드롭 기능
      - 
- ## Foundation Kit은 무엇이고 포함되어 있는 클래스들은 어떤 것이 있는지 설명하시오.
  - Foundation Kit은 Cocoa Touch framework에 포함되어 있는 프레임워크 중 하나로 String, Int 등의 원시 데이터 타입과 컬렉션 타입 및 운영체제 서비스를 사용해 앱의 기본적인 기능을 관리하는 프레임워크입니다.
  - iterator, jsonEncoder, jsonDecoder 와 같은 데이터 관련 클래스가 정의되어 있습니다.
    - iterator: 배열이나 그와 유사한 자료 구조의 내부의 요소를 순회(traversing) 하는 객체이다.
    - jsonEncoder: 데이터 유형의 인스턴스에서 JSON 개체로 변환하는 객체
    - jsonDecoder: JSON 개체에서 데이터 유형의 인스턴스로 변환하는 객체
      
- ## Delegate란 무엇인지 설명하고, retain 되는지 안되는지 그 이유를 함께 설명하시오.
  - Delegate란 객체 지향 프로그래밍에서 하나의 객체가 모든 일을 처리하는 것이 아니라 처리해야 할 일 중 일부를 다른 객체에게 넘기는 것을 의미한다.
  - retain(유지하다): 메모리가 해제되지 않아서 낭비되는 현상을 의미(Memory Leak), Delegate는 객체 간의 작업이여서 참조 값을 사용하기 때문에 retain 현상이 일어난다.
  - 해결방법: weak: 약한참조, unowned: 약한 참조이고 해제된 메모리 영역에 재접근하지 않는다는 확신이 있을 때
    
- ## NotificationCenter 동작 방식과 활용 방안에 대해 설명하시오.
  - NotificationCenter란?
    - observer(관찰자)에게 정보를 전달해주는 알림 발송 메커니즘
  - 언제 NotificationCenter를 사용?
    - 앱 내에서 공식적인 연결이 없는 두 개 이상의 컴포넌트들이 상호작용이 필요할 때
    - 상호작용이 반복적으로 그리고 지속적으로 이루어져야 할 때
    - 일대다 또는 다대다 통신을 사용하는 경우
  - Observer(관찰자) 등록
    ```swift
    NotificationCenter.default.addObserver(
      self,
      selector: #selector(scrollToBottom), //알림을 받을 때 수행할 action
      name: NSNotification.Name("TestNotification"),
      object: nil
    )
    ```
    - 알림을 받고 싶은 부분에 observer를 등록한다.
      
  - 알림 발송
    ```swift
    NotificationCenter.default.post(
      name: NSNotification.Name("TestNotification"),
      object: nil
    )
    ```
    - observer에게 알림을 발송한다. 이때 object에 데이터도 함께 전달할 수 있다.

  - Observer 제거  
    ```swift
    NotificationCenter.default.removeObserver(
      self,
      name: NSNotification.Name("TestNotification"),
      object: nil
    )
    ```
    - observer를 제거하지 않으면 메모리에 계속 남아있기 때문에 remove 해준다.
  - extension을 활용하여 NotificationName 관리
    ```swift
    extension Notification.Name {
      static let testNotification = Notification.Name("TestNotification")
    }
    ```
- ## UIKit 클래스들을 다룰 때 꼭 처리해야하는 애플리케이션 쓰레드 이름은 무엇인가?
  - Main Thread
    UIApplication의 인스턴스가 main thread에 붙고(attach), 이 UIApplication은 앱을 시작할 때 인스턴스화 되는 앱의 첫번째 부분이고
    앱의 run loop를 포함하여 main event loop를 설정하고 event 처리를 시작함.
    앱의 main event loop는 touch, gesture등의 모든 UI event를 수신함.
    모든 UI작업은 main thread의 '일부'라고 할 수 있다. 따라서 모든 이벤트는 main thread의 일부가 되며, main thread에서 처리해야 한다.
    UIKit은 Thread-safe 하지 않다. 그래서 모든 처리를 Serial 하게 처리해줘야 한다. 그래서 UI는 main thread에서 synchronously하게 동작해야 한다.
    
- ## App Bundle의 구조와 역할에 대해 설명하시오.
  - App Bundle은 iOS 앱을 실행하는데 필요한 모든 파일과 리소스가 포함된 특별한 유형의 폴더이다.
  - Excudable file:
    - 앱을 실제로 실행하는 파일이다. ".app" 확장자가 없는 앱과 이름이 동일하다. 예를 들어 앱 이름이 "MyCoolApp"인 경우 실행 파일 이름은 "MyCoolApp"이다.
  - Info.plist:
    - 앱에 대한 메타데이터가 포함된 속성 목록 파일이다. 여기에는 앱 이름, 버전 번호, 번들 식별자 등이 포함된다. 앱이 화면에 표시되는 방식과, 앱 아이콘, 필수 기기 기능, 접근 권한을 포함한다.
  - Frameworks:
    - 앱에서 타사 프레임워크를 사용하는 경우 AppBundle에 포함된다. "Frameworks" 폴더에서 찾을 수 있다.
  - Resources:
    - 앱의 모든 비 코드 파일이 저장되는 곳이다. 여기에는 이미지, 사운드, 지역화된 문자열 등이 포함된다. "Resouce" 폴더에서 찾을 수 있다.
  - Storyboards & Xibs:
    - 앱에서 스토리보드 또는 Xib를 사용하여 사용자 인터페이스를 정의하는 경우 AppBundle에 포함된다.
  - Launch Screen:
    - 앱이 실행될 때 표시되는 화면이다. "LaunchScreen.storyboard" 또는 "LaunchScreen.xib"라는 파일에 정의되어 있으며 AppBundle에 포함되어 있다.
  - Plugins:
    - 앱에서 플러그인을 사용하는 경우 AppBundle에 포함된다. "Plug-in" 폴더에서 찾을 수 있다.
  - Excutable dependecies(실행 가능한 종속성):
    - 앱이 외부라이브러리 또는 프레임워크에 연결되면 App Bundle에 포함된다.
  - DataFiles:
    - 앱이 런타임에 생성된 데이터 파일을 사용하는 경우 "Documents"폴더에 저장된다.
    - 이 폴더는 앱이 설치될 때 생성되며 앱이 샌드박스에 있다.
  이러한 모든 파일과 폴더는 AppBundle 내에 특정 방식으로 구성된다. 실행 파일은 info.plist 파일과 함께 최상위 수준에 있다.
- ## 모든 View Controller 객체의 상위 클래스는 무엇이고 그 역할은 무엇인가?
  - UIViewController
  - 뷰의 내용을 업데이트하고, 뷰와 사용자의 상호 작용에 응답하고, 기본 데이터의 변경에 대한 응답으로 뷰의 콘텐츠를 업데이트 하고, 뷰 크기 조정 및 전체 인터페이스의 레이아웃을 관리합니다.
- ## 자신만의 CustomView를 만들려면 어떻게 해야하는지 설명하시오.
  - Xib을 이용해서 별도의 Storyboard처럼 관리 가능
    - Xib을 생성하고 또한 별도의 UIView을 상속받은 Class을 생성한다. 그리고 Xib에서 owner로 해당 클래스를 임명하고 커스텀 클래스 내에서 초기화 시, Xib 파일을 불러와 view로 임명하는 코드 추가를 하고 원하는 작업들을 Storyboard 와 동일하게 수행하면 된다.
  - UIView을 상속해서 코드로만 구현
    - UIView을 상속받는 클래스를 생성해 코드로만 원하는 작업들을 설정한다.
    
