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
- ## View 객체에 대해 설명하시오.
  - 화면에 content 표시, 그리기 및 애니메이션, 오토레이아웃, 제스처 인식 등 화면에 관한 것들을 담당하는 객체입니다. view는 사용자 인터페이스의 기본 구성 요소이며 모든 조작은 main thread에서 해야합니다.
- ## UIView 에서 Layer 객체는 무엇이고 어떤 역할을 담당하는지 설명하시오.Permalink
  - 렌더링에 사용되는 뷰의 CoreAnimation계층 UIView를 지원해주고 실질적으로 뷰위에 컨텐츠와 애니메이션을 그리는 담당
- ## UIWindow 객체의 역할은 무엇인가?
  - 사용자 인터페이스에 배경(backdrop)을 제공하고, 중요한 이벤트 처리 행동(behaviors)을 제공하는 객체
- ## UINavigationController 의 역할이 무엇인지 설명하시오.
  - UINavigationController는 앱의 화면 이동에 대한 관리와 그에 연관된 처리를 담당해주는 컨트롤러입니다. 이는 네비게이션 바와 툴바를 두 가지를 보여주는 역할을 합니다. 네비게이션 바에서는 뒤로 가기 버튼과 커스터마이징한 버튼을 추가할 수 있으며 옵션으로 툴바 뷰도 제공합니다
- ## TableView를 동작 방식과 화면에 Cell을 출력하기 위해 최소한 구현해야 하는 DataSource 메서드를 설명하시오.
  - numberOfRowInSection 섹션에 표시할 행의 개수
  - cellForRowAt 특정 위치에 표시할 셀을 요청하는 메서드
- ## 하나의 View Controller 코드에서 여러 TableView Controller 역할을 해야 할 경우 어떻게 구분해서 구현해야 하는지 설명하시오.
  - func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell 에서 파라미터로 받는 tableView 를 객체 비교를 통해 구분한다.
  - 테이블 뷰의 Tag 를 등록, 비교해서 구분한다.
- ## setNeedsLayout와 setNeedsDisplay의 차이에 대해 설명하시오.
  - setNeedsLayout()메소드와 setNeedsDisplay() 메소드 모두 호출 즉시 실행되지 않고 다음 update cycle에 변경사항이 적용됩니다.
  - setNeedsLayout은 layoutSubview메소드를 setNeedsDisplay는 draw메소드를 시스템이 호출하게끔 유도한다.
  - setNeedsLayout() 메소드는 모든 핸들러가 종료되고 권한이 main run loop로 돌아오는 시점에 view의 position이나 layout에 관한 변화를 적용시키고 setNeedsDisplay() 메소드는 다음 드로잉 사이클이 오면 그 때 쌓여있는 그려야할 컨텐츠들을 동시에 적용시킵니다.
- ## NSCache와 딕셔너리로 캐시를 구성했을때의 차이를 설명하시오.
  - 딕셔너리는 메모리가 부족하면 값을 삭제하는 코드를 작성해야 하지만 NSCache는 메모리가 자동으로 관리된다.
  - NSCache 는Thread-safe하다. 데이터를 쓸때마다 lock을 해줄 필요가 없다.
- ## URLSession에 대해서 설명하시오.
  - 앱과 서버 간 데이터를 주고 받기 위해 사용하는 Apple의 기본 API URLSessionConfiguration 설정하고 URLSession·URLComponents 생성, 이를 통해 URLSessionDataTask 생성 한 뒤, 마지막으로 테스크를 실행하는 과정을 거친다.
- ## prepareForReuse에 대해서 설명하시오.
  - tableView의 cell을 재사용하기 위해 셀 속성을 reset하는 함수입니다. dequeueReusableCell 메서드에서 객체가 반환되기 직전에 호출됩니다.
- ## ViewController의 생명주기를 설명하시오.
  - init ViewController 객체가 생성됩니다.
  - loadView View를 메모리에 로드합니다.
  - viewDidLoad View의 Controller가 메모리에 로드된 뒤 호출됩니다.
  - viewWillAppear View가 표시되기 직전에 호출됩니다.
  - viewDidAppear View가 표시된 후 호출됩니다.
  - viewWillDisappear View가 사라지기 직전 호출됩니다.
  - viewDidDisappear View가 사라지기 직후 호출됩니다.
  - viewDidUnload View가 메모리에서 해제된 뒤 호출됩니다.
- ## TableView와 CollectionView의 차이점을 설명하시오.
  - 테이블뷰에서는 하나의 열에 여러 행의 cell을 표현하는 방식이기때문에, cell의 모양은 항상 row에 맞춰서 디자인 해야한다.
  - 컬렉션뷰는 행과 열을 모두 만들 수 있기 때문에 cell의 모양을 자유롭게 디자인이 가능하다.
- ## 오토레이아웃을 코드로 작성하는 방법은 무엇인가? (3가지)
  - 1. NSLayoutConstraint 사용

  - 2. Visual Format Language 사용

  - 3. Anchor 사용
- ## hugging, resistance에 대해서 설명하시오.
  - hugging 우선순위가 클수록 자신의 크기를 유지하려하고, 우선순위가 작을수록 크기가 늘어나는 속성
  - resistance 우선순위가 클수록 자신의 크기를 유지하려하고, 우선순위가 작을수록 크기가 작아지려는 속성
- ## Intrinsic Size에 대해서 설명하시오.
  - Intrinsic Size는 콘텐츠의 본질적인 크기입니다. 모든 view가 Intrinsic Size를 갖는 것은 아니고, 대표적인 예로는 UILabel, UIButton을 들 수 있습니다. 또한, 각각의 view마다 Intrinsic Size가 적용되는 방식이 다릅니다.
- ## 스토리보드를 이용했을때의 장단점을 설명하시오.
  - 장점
    - UI 구성을 한눈에 확인할 수 있다
    - View에 어떤 속성과 값을 설정했는지 확인하기 쉽다
  - 단점
    - StoryBoard 구현을 위해 Xcode 메모리가 올라간다. (이 부분은 기능별로 StoryBoard를 분리하면 해결 가능)
    - 협업시 StoryBoard 충돌 혹은 이슈가 발생할 수 있다
    - 인터페이스빌드와 StoryBoard 간 연결을 추적하기 어려울 수 있다
- ## 코드 기반 UI의 장단점
  - 장점
    - 스토리보드와 비교했을 때 Xcode가 가벼워진다
    - 협업시 충돌 위험도가 낮아진다
    - 스토리보드에 비해 View의 재사용성이 좋다
  - 단점
    - View가 어떤 모습을 갖고 있을지 한눈에 파악하기 어렵다
    - View의 속성 및 기능을 숙지하고 있어야한다 (스토리보드처럼 기능에 대한 표시를 해주지 않음)
    - NSLayoutConstraint를 통해 AutoLayout을 설정해줘야 하는데 귀찮고 복잡하다 (SnapKit 라이브러리를 통해 극복 가능)
- ## Safearea에 대해서 설명하시오.
  - 핸드폰의 전체적인 UI를 통틀어서 컨텐츠가 제대로 보일수 있는 부분에만 우리 뷰를 놓을 수 있도록 도와주는 기능.
- ## Left Constraint 와 Leading Constraint 의 차이점을 설명하시오.
  - Left Constraint는 어떤 객체의 왼쪽을 뜻하고
  - Leading Constraint는 어떤 객체의 앞쪽 가장자리를 뜻한다.
- ## class와 struct와 enum의 차이를 설명하시오.
class 참조 타입
실제 인스턴스(데이터)는 힙에 저장되고, 그 인스턴스를 가리키는 변수에 메모리 주소가 담겨 스택에 저장됨
일반적으로 단일 상속이 가능하지만, 프로토콜을 사용하면 다중 상속도 가능

struct 값 타입
실제 인스턴스의 데이터 자체가 스택에 저장됨
상속이 불가능

enum 값 타입
상속 불가
유사한 종류의 여러 값을 유의미한 이름으로 한 곳에 모아 정의한 것
열거형 자체가 하나의 데이터 타입

- ## class의 성능을 향상 시킬수 있는 방법들을 나열해보시오.
  - heap보다는 stack메모리를 할당하려고 노력한다.
  - reference counting을 적게 만든다.
  - 클래스를 선언할 때 상속되지 않는 클래스에 final을 붙이면 성능이 향상됩니다.
- ## Copy On Write는 어떤 방식으로 동작하는지 설명하시오.
  - Copy On Write는 A라는 변수에 B라는 변수를 할당해주었을 때, 새로 메모리에 할당하는 것이 아니라, B의 메모리를 A가 공유하는 형태로 구성됩니다. 그러다가 A가 값이 수정될 때 새로 메모리에 할당이 되는 식으로 동작합니다.
- ## Convenience init에 대해 설명하시오.
  - 보조 이니셜라이저로, 클래스의 원래 이니셜라이저인 init을 도와주는 역할을 합니다.
  - convenience init은 같은 클래스에서 다른 이니셜라이저를 호출해야한다는 규칙이 있습니다.
- ## AnyObject에 대해 설명하시오.
  - AnyObject는 모든 클래스 타입의 인스턴스를 나타낼 수 있는 프로토콜입니다.
  - AnyObject로 선언 시, “클래스 타입”만 저장할 수 있습니다.
- ## Optional 이란 무엇인지 설명하시오.
  - 래핑된 값 또는 값이 없는 nil 상태를 표현하는 형식이며, enum 구조를 뛰고 있다. 값이 있고 래핑된 some case 제네릭 형태 그리고 값이 없는 nil상태 none 케이스
- ## Struct 가 무엇이고 어떻게 사용하는지 설명하시오.
  - 인스턴스의 값(프로퍼티)을 저장하거나, 기능(메소드)를 제공하고 이를 캡슐화할 수 있도록 스위프트가 제공하는 타입입니다.
- ## Subscripts에 대해 설명하시오.
   - Class, Struct, Enum에서 collection, 순열, list, sequence 등 집합의 특정 멤버 요소에 쉽게 접근하기 위한 방법입니다.
  - 이것을 이용하면 추가적인 메소드없이 특정 값을 할당(set)하거나 가져(get)올 수 있습니다.
  - 인스턴스 이름 뒤에 대괄호로 감싼 값을 써줌으로써 인스턴스 내부의 특정 값에 접근할 수 있습니다.
- ## String은 왜 subscript로 접근이 안되는지 설명하시오.
  - Swift에서 Character는 1개 이상의 Unicode Scalar로 이루어져 있다. 즉 크기가 가변적이다.
- ## instance 메서드와 class 메서드의 차이점을 설명하시오.
  - Instance Method 클래스를 통해 호출할 수 없고, 클래스의 인스턴스를 만들어 실체하여 생성된 인스턴스를 통해서 호출할 수 있는 메소드 입니다.
  - Class Method  인스턴스를 만들어 실체화 하지 않아도 클래스를 통해 직접적으로 호출 할 수 있습니다.
- ## class 메서드와 static 메서드의 차이점을 설명하시오.
  - class메서드는 오버라이딩 가능하지만 static메서드는 오버라이딩이 불가능합니다.
- ## Delegate 패턴을 활용하는 경우를 예를 들어 설명하시오.
  - 객체지향 프로그래밍에서 하나의 객체가 모든 일을 처리하는 것이 아니라 해야할일 중 일부를 다른 객체에게 넘기는 것(위임하는 것)
  - 대표적으로 TableViewDelegate가 있다 뷰컨트롤러에 딜리게이트 함수를 정의하고 테이블뷰의 동작이 일어나면 해당 딜리게이트 함수를 호출하고 뷰컨트롤러가 대신 처리해줌
- ## Singleton 패턴을 활용하는 경우를 예를 들어 설명하시오.
  - 인스턴스가 하나만 존재하는 것을 보증하고 싶을 경우에 사용
  - 메모리 낭비를 방지할 수 있고 데이터를 공유할 수 있다는 대표적인 장점
  - URLSession.shared 네트워크 처리를 할 때 URLSession 객체를 이용하는데, 이미 만들어져있는 shared 객체에 접근해 메서드를 수행한다.
- ## KVO 동작 방식에 대해 설명하시오.
  - 모델 객체의 어떤 값이 변경되었을 경우 이를 UI에 반영하기 위해서 컨트롤러는 모델 객체에 Observing을 도입하여 델리게이트에 특정 메시지를 보내 처리할 수 있도록 하는 것
  - 즉, 변수에 코드를 붙여 변수가 변경될 때마다 코드가 실행되도록 하는 방법을 의미
- ## Delegates와 Notification 방식의 차이점에 대해 설명하시오.
  - 가장 큰 차이점은 Notification과 다르게 Delegate의 경우에는 수신자가 발신자의 정보를 알고 있어야한다는 것이다.
  - delegate 방식은 주로 이벤트를 1:1로 전달할 때 많이 사용됩니다. 주로 protocol을 정의하고 이를 이벤트를 대신 처리할 객체가 채택하여 사용하게 됩니다. 이에 따라 제 3 객체를 필요로 하지 않으며 확실한 처리가 가능하지만, 많은 줄의 코드를 필요로 하며 많은 객체에게 이벤트를 알리고 싶을 경우 비효율적이라는 단점이 있습니다.
  - notification 방식은 이벤트를 1:N으로 전달할 때 용이합니다. NotificationCenter라는 싱글톤객체를 기반으로 이벤트 발생여부를 옵저버를 등록한 객체에게 전달하는 방식으로 구성됩니다. 따라서 다수의 객체에게 손쉽게 이벤트 전달이 가능합니다. 하지만 제 3 객체를 필수적으로 필요로 하며, key값으로 Notification의 이름을 사용하기 때문에 컴파일 중 구독이 제대로 이루어져있는지 확인할 수 없다는 단점이 존재합니다.
- ## 멀티 쓰레드로 동작하는 앱을 작성하고 싶을 때 고려할 수 있는 방식들을 설명하시오.
  - UI업데이트에 관한 작업들은 메인스레드
  - 동기로 할지 비동기로 할지를 명확하게 정의해야함
  - 어떤 작업을 글로벌 큐에 넣어야 할지 정확히 알아둬야 함
  - 글로버 큐에 작업을 배치할 때, 작업에 따라 QoS를 적절하게 사용해야함
  - 상황에 따라 작업간의 인과관계를 설정하거나 특정 시간 이후에 처리하도록 설정해야함
- ## 프로토콜이란 무엇인지 설명하시오.
  - 프로토콜은 class나 struct의 행동을 정의하는 역할을 합니다. 프로토콜은 행동을 정의하기만 할 뿐 구현하지 않습니다. 어떠한 클래스나 구조체가 해당 프로토콜을 따른다는 것은 프로토콜에 정의된 행동들을 구현해야함을 의미합니다.
- ## POP(프로토콜 중심 프로그래밍)과 OOP(객체 중심 프로그래밍)의 차이점을 설명하시오.
  - POP는 프로토콜 중심 프로그래밍으로, 슈퍼클래스와 서브클래스의 사이가 독립적이고 reference 타입과 value 타입을 모두 지원하여 OOP의 단점들을 모두 보완할 수 있다. 또한, 합성으로 객체를 묘사하는 수평적인 구조를 가지고 있어 상속과는 다르게 다수의 프로토콜을 가지는 것이 가능하다.
  - OOP는 객체중심 프로그래밍으로, 상속을 통해 타입을 확장하는 수직적인 구조를 가지고 있다. 그렇기 때문에 슈퍼클래스를 그대로 상속받아 필요없는 메소드와 변수를 모두 물려받아야 한다는 단점이 있다. 또한 상속구조를 사용하기 위해서는 value type으로 정의해도 되는 모델들을 reference 타입으로 정의해야하는 불편함이 있다.
- ## Hashable이 무엇이고, Equatable을 왜 상속해야 하는지 설명하시오.
  - Hashable은 "정수 hash값을 제공하는 타입"으로 정의된 프로토콜입니다.
  - hash란, 해시 함수에 의해 얻어지는 값으로 해시값, 해시코드, 해시 체크섬으로도 불립니다.
  - 해시함수 : 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수
  - hashValue : 어떠한 데이터를 Hash 함수에 넣게 되면 반환해주는 값
  - 해쉬값은 고유값이어야 하므로 고유값이지 식별해 줄 수 있는 "=="함수가 필요합니다. 이 함수는 Equatable 프로토콜 안에 정의되어 있으니 hashable은 equatable프로토콜을 따라야합니다. 기본 데이터 타입도 ==을 통해 비교가 가능하므로 equatable프로토콜을 따릅니다.
  - HashTable에서 hash값을 찾기 위해선 key가 필요하고 이 key는 식별할 수 있도록 unique해야 합니다.
 - ## mutating 키워드에 대해 설명하시오.
  - 값 타입의 속성은 기본적으로 인스턴스 메서드 내에서 수정할 수 없습니다.
  - mutating을 선언한 메서드는 메서드 내에서 프로퍼티를 변경할 수 있고, 메서드가 종료될 때 변경한 모든 내용을 원래 struct에 다시 기록합니다. 또한 메서드는 self property에 새 인스턴스를 할당할 수도 있습니다.
- ## 탈출 클로저에 대하여 설명하시오.
  - 비동기 작업을 하기 위해서 탈출 시키는 클로저
  - 함수의 인자로 전달된 클로저가 함수가 반환된 후 실행 되는 클로저
  - 전달인자로 받은 클로저가 함수 종료 후에 호출될 경우 "클로저가 함수를 탈출한다"로 표현합니다.
- ## Extension에 대해 설명하시오.
  - 수평적 확장이다.
  - extension은 기존 존재하는 클래스, 구조체, 열거형, 프로토콜 타입에 새로운 기능을 추가할 수 있게 해준다.
  - 내부 소스를 접근할 수 없는 원본 타입들에 대해 새로운 기능을 부여할 수 있고, 특정 타입의 기능 및 준수하는 프로토콜별 구현부를 분리해서 보다 코드 가독성을 높일 수 있습니다.
- ## Extension 내부에서 함수를 override 할 수 있는지 설명하시오.
  - 새로운 기능을 정의하는 것은 가능하지만 override할 수는 없습니다.
  - override는 부모클래스의 메서드를 자식 클래스가 재정의하여 사용하는 것을 의미하지만, extension은 수평적인 확장이기 때문에 override라는 개념이 어울리지 않습니다.
- ## 접근 제어자의 종류엔 어떤게 있는지 설명하시오.
  - open: 다른 모듈에서도 접근가능 / 상속 및 재정의도 가능(제한 낮음)
  - public: 다른 모듈에서도 접근가능(상속 / 재정의 불가)
  - internal: 같은 모듈 내에서만 접근가능(기본 설정 값)
  - fileprivate: 같은 파일 내에서만 접근가능
  - private: 같은 scope내에서만 접근가능(제한 높음)
- ## defer란 무엇인지 설명하시오.
  - 현재 코드 블록을 나가기 전에 꼭 실행해야 되는 코드를 작성하여 코드가 블록을 어떻게 빠져 나가든 꼭 마무리 해
- ## property wrapper에 대해서 설명하시오.
  - 프로퍼티를 감싸 특별한 타입으로 만들어준다.
  - 어떤 로직들을 매번 동일하게 지정해주지 않고 Property Wrapper로 만든 타입으로 프로퍼티를 선언해 동일 로직을 수행한다.
  - 지역변수에만 사용가능합니다.
- ## Genericc에 대해 설명하시오.
  - 제네릭이란 타입에 의존하지 않는 범용 코드를 작성할 때 사용한다.
  - 제네릭을 사용하면 중복을 피하고, 코드를 유연하게 작성할 수 있다.
- ## some 키워드에 대해 설명하시오.
  - some 키워드는 return값에 불투명한 타입이 있음을 나타냅니다. 불투명한 타입이란 어떠한 타입을 리턴할지 모른다는 것입니다. some 키워드를 사용하면 함수 내부의 리턴 값에 따라 리턴 타입이 지정됩니다.
- ## Result 타입에 대해 설명하시오.
  - Result 타입은 Generic Enumeration로 선언되어 있고, 경우에 따른 연관값을 포함하여, 성공과 실패를 나타내는 값입니다.
- ## Codable에 대하여 설명하시오.
  - 기존의 Encodable과 Decodable이 합쳐진 프로토콜 입니다.
  - Encodable -> data를 Encoder에서 변환해주려는 프로토콜로 바꿔주는 것
  - Decodable -> data를 원하는 모델로 Decode 해주는 것
- ## Clousre에 대하여 설명하시오.
  - 참조타입이다.
  - 클로저는 사용자의 코드 안에서 전달되어 사용할 수 있는 로직을 가진 중괄호 {} 로 구분된 코드의 블럭이며, 일급 객체의 역할을 할 수 있다.
- ## Clousre와 함수와의 관계에 대해 설명하시오.
  - 함수는 클로저의 한 형태로, 이름이 있는 클로저이다.


# ARC
- ## ARC란 무엇인지 셜명하시오.
  - heap 영역에 참조형 자료들이 얼마나 참조되고 있는지를 카운팅하고 이에따라 자동으로 메모리 할당 및 제거 한다.
- ## Retain Count 방식에 대해 설명하시오.
  - compile time에는 코드를 분석하고 예측하여 적절한 위치에 retain, release 를 삽입해준다.
  - run time에 삽입된 코드가 실행되면서 retain, release에 의해 reference count를 증감하고 count가 0이 되었을 때 메모리에서 제거한다.
- ## Strong과 Weak 참조 방식에 대해 설명하시오.
  - Strong은 해당 인스턴스의 소유권을 가진다. 자신이 참조하는 인스턴스의 reference count를 증가시킨다. 값 지정 시점에 retain되고, 참조가 종료되는 시점에 release가 된다. 메모리릭이 발생할 수 있다(순환 참조). 해결책이 바로 약한참조(weak, unowned)이다.
  - Weak는 해당 인스턴스의 소유권을 가지지 않고, 주소값만 가지고 있는 포인터 개념이다. 자신이 참조하는 인스턴스의 reference count를 증가시키지 않는다(release도 발생하지 않음.). 자신이 참조는 하지만 weak 메모리를 해제시킬 수 있는 권한은 다른 클래스에 있다. 메모리가 해제될 경우 자동으로 레퍼런스가 nil로 초기화를 해준다. weak 속성을 사용하는 객체는 항상 optional 타입이어야 한다(해당 객체가 nil일 수 있기 때문에)
  - Unowned는 Weak와 비슷하지만 인스턴스를 참조하는 도중에 해당 인스턴스가 메모리에서 사라질 일이 없다고 확신하는 것이 핵심이다. 참조하던 인스턴스가 메모리에서 해제되도, nil을 할당받지 못하고 해제된 메모리 주소값을 계속 가지고 있다.
- ## 순환 참조에 대하여 설명하시오.
  - 순환 참조란 여러 클래스 인스턴스가 서로간에 강한 참조상태(Strong Reference)를 가질 때 발생하고, 순환 참조가 발상하게되면 서로간의 참조가 해제되지 않기 때문에 메모리 누수(Leak)가 발생할 수 있다.
```swift
class Person {
  var name: String
  var puppy: Puppy?

  init(name: String) {
    self.name = name
  }

  deinit {
    print("Person deinit")
  }
}
class Puppy {
  var name: String
  var owner: Person?

  init(name: String) {
    self.name = name
  }

  deinit {
    print("Puppy deinit")
  }
}

var john: Person? = Person(name: "John")
var jackson: Puppy? = Puppy(name: "Jackson")

john?.puppy = jackson
jackson?.owner = john
```
위의 코드의 클래스 인스턴스 프로퍼티를 보면 변수로만 정의되어 있다. 이는 Strong이 생략된 상태이다. 따로 정의한 키워드가 없다면 default값은 Strong이다.
- ## 강한 순환 참조(Strong Reference Cycle)는 어떤 경우에 발생하는지 설명하시오.
```swift
john = nil
jackson = nil
```
아직 클래스 인스턴스가 메모리에서 해제되지 않아 deinit이 호출되지 않는다,.
클래스 인스턴스의 프로퍼티끼리 서로를 참조하는데 이것들이 있으므로 RC가 0이 되지 않아 deinit을 호출하지 않고, 정상적으로 메모리에서 해제되지 않아 메모리 누수가 발생하고 있는 것이다.
weak 키워드를 붙임으로써 약한 참조임을 선언할 수 있다. 클래스 인스턴스를 참조해도, RC를 증가시키지 않는다. 서로 참조하던 클래스 인스턴스 중 하나가 메모리에서 해제되면, 다른 클래스 인스턴스에도 자동으로 nil이 할당되어 메모리에서 해제된다.

# Functional Programming
- ## 순수함수란 무엇인지 설명하시오.
  - 입력값이 같으면 항상 같은 결과값을 반환하고, 부작용(Side Effect)이 없는 함수를 의미한다.
  - 부작용이란 함수 외부의 어떤 상태를 변경하거나 함수 외부와 상호작용을 하는 것을 의미한다.
  - 순수 함수를 작성할 때에는 입력값과 출력값만으로 모든 것을 처리해야 하므로, 함수 내부에서 외부의 상태를 변경하지 않아야 한다.
- ## 함수형 프로그래밍이 무엇인지 설명하시오.
  - 프로그램이 상태의 변화 없이 데이터 처리를 수학적 함수 계산으로 취급하고자 하는 프로그래밍
  - 값이나 상태의 변화보다는 함수 자체의 응용을 중요하게 여긴다.
  - 코드 이해와 실행 결과의 관점에서, 순수하게 함수에 전달된 인자 값만 결과에 영향을 주기 때문에 상태 값을 갖지 않고 순수하게 함수만으로 동작 -> 어떤 상황에서 프로그램을 실행하더라도 일정하게 같은 결과를 도출할 수 있다.
  - 필요한 만큼 함수를 나누어 처리할 수 있도록 스케일업 할 수 있기 때문에 대규모 병렬처리에 큰 강점을 가진다.
- ## 고차 함수가 무엇인지 설명하시오.
  - 하나 이상의 함수(클로저)를 인자로 받거나, 함수(클로저)를 반환 하는 함수를 의미한다.
  - Swift의 함수(클로저)는 일급객체이기 때문에, 함수의 전달인자로 전달하거나, 결과값으로 반환할 수 있다. 참고로 클로저는 `named, unnamed 두 종류`가 있고, `함수가 named 클로저`이다.
- ## map, filter, reduce, compactMap, flatMap에 대하여 설명하시오.
  - map: 컨테이너 내부의 기존 데이터를 변형하여 새로운 컨테이너를 생성
  - filter: 컨테이너 내부의 값을 걸러서 새로운 컨테이너로 추출, 요소가 반환된 배열에 포함되어야 하는지 여부를 Bool 값으로 반환 하는 클로저
  - reduce: 컨테이너 내부의 콘텐츠를 하나로 통합
  - flatMap: map과 동일하지만, 차원을 한단계 낮춘 새로운 컨테이너를 생성
  - compactMap: map과 동일하지만, 결과값에서 nil을 제거하고 옵셔널 바인딩을 적용시킨 새로운 컨테이너를 생성
- ## Either type이란?
  - 값이 두 가지 타입 중 하나 단일 타입의 값이 두 가지 의미 중 하나를 갖도록 지정할 수 있을 때 사용.

# Architecture
- ## MVVM, MVC, VIPER 아키텍쳐를 설명하시오.
  - MVVM: Model, View, ViewModel로 구성되고, ViewModel이 중간 역할, View와 ViewModel 사이에 binding이 있다. ViewModel은 Model에 변화를 주고 ViewModel을 업데이트 하는데 이 바인딩으로 인해 View도 업데이트. ViewModel은 View에 대해 아무것도 모르기 때문에 테스트가 쉽고 바인딩으로 인해 코드 양이 많이 줄어든다.
  - MVC: Model, View, Controller로 구성되고, model에서는 애플리케이션이 사용할 데이터들을 관리하고, View는 유저 인터페이스를 표현 및 관리한다. Controller는 View와 Model의 다리 역할을 해 View의 입력을 Model이 반영하고, Model의 변화를 View에 갱신한다.
  - VIPER: View, Interactor, Presenter, Entities, Router로 구성되고, MVC 패턴을 대체하기 위해 만들어진 패턴. Entity는 그저 모델 객체이다. 단순하게 어떤 모델의 속성들만 있는 Dumb Model이라고 부를 수 있다. 이 모델 객체를 조작하는 것이 바로 Interactor이다. 어떤 행동에 따라서 모델 객체를 조작하는 로직이 담겨있다. 작업이 완료되어도 View에 아무런 영향 없이 오로지 데이터 작업만 한다. Presenter는 데이터를 Interactor에서 가져오고, 언제 View에 보여줄 지 결정한다. View에 보여주기 전 내용을 준비하는 로직을 담당한다. View는 Presenter에서 어떻게 보여줘야 할 지 요청대로 디스플레이하고, 사용자의 입력을 받으면 다시 Presenter로 넘긴다. Router는 화면 전환을 담당한다. Presenter가 언제 화면을 전환해야 하는지 안다면 Router는 화면 전환을 어떻게 하는지 알고 있다.
# Autolayout
- ## 오토레이아웃을 코드로 작성하는 방법은 무엇인가?(3가지)
  - NSLayoutConstraint 사용
  - Visual Format Language 사용
  - Anchor 사용(코드가 더 clean해지고, 더 간결해지고, 더 읽기 쉬워진다.)
  - 이외에 SnapKit과 같은 라이브러리 사용
- ## hugging, resistance에 대해서 설명하시오.
  - hugging: 두 오브젝트 중에 한 쪽이 커져야 하는 상황일 때 어떤 오브젝트가 Intrinsic Size를 유지 못하고 늘어날지를 결정한다. 우선순위가 높은 오브젝트가 Intrinsic Size를 유지, 낮은 오브젝트가 늘어난다.
  - resistance: 두 오브젝트 중에 한 쪽이 작아져야 하는 상황일 때 어떤 오브젝트가 Intrinsic Size를 유지 못하고 줄어들지 결정한다. 우선순위가 높은 오브젝트가 Intrinsic Size를 유지, 낮은 오브젝트가 줄어든다.
- ## Intrinsic Size에 대해서 설명하시오.
  - Intrinsic Size는 콘텐츠의 본질적인 크기이다. 자신의 컨텐츠 사이즈에 따라서 결정되는 뷰 사이즈를 말한다. 모든 view가 Intrinsic Size를 갖는 것은 아니고, 대표적인 예로는 UILabel, UIButton을 들 수 있다.
- ## 스토리보드를 이용했을때의 장단점을 설명하시오.
  - 장점:
    - 앱의 흐름을 직관적으로 볼 수 있음
    - 드래그 앤 드롭으로 UI구성 가능
    - 개발이 빠름
  - 단점:
    - 충돌시 해결어려움
    - 스토리보드에 많은 컴포넌트들이 있으면 로딩시간이 오래걸림
    - 컴포넌트가 많아질수록 세밀한 조정이 어렵다.
- ## SafeArea에 대해서 설명하시오.
  - 시스템에 의해 가려질 수 있는 부분에 대한 margin을 자체적으로 가지고 있는 영역을 뜻한다. 주로 해당 구역 내부에 view를 그려 노치 등에 의한 view의 가려짐을 방지한다.
- ## Left Constraint와 Leading Constraint의 차이점을 설명하시오.
  - Left와 Right는 절대적이며 뷰를 기준으로 각각 왼쪽과 오른쪽을 뜻한다. leading과 trailing은 각각 글자가 시작하는 방향과 끝나는 방향으로 device locale에 따라 leading이 left가 되기도 하고 right가 되기도 한다. 따라서 애플리케이션의 지역화를 지원해야 하는 경우 leading과 trailing의 사용을 권장한다. 추가로 WWDC 15 Mysteries of Auto Layout에 left/right보다 leading/trailing을 사용하라는 내용이 포함되어 있다.
- ## Auto Layout과 Frame-based Layout의 차이점은 무엇인가?
  - AutoLayout은 제약 조건을 이용해서 View의 위치나 크기를 정한다. 따라서 상대적으로 제약을 준다. 화면의 해상도에 따라 Frame이 동적으로 달라질 수 있다.
  - Frame-based Layout은 무조건 원점에서 원하는 위치만큼 떨어진 곳에 view를 그린다. 어떤 해상도에서도 같은 크기와 위치를 유지한다. 따라서 기기가 변해도 frame은 절대 변하지 않는다.
    
