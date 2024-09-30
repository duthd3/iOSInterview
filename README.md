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
# 레벨 0
- ## 1. 컴퓨터 구조와 관련하여 CPU, RAM, 저장장치의 역할과 상호 작용에 대해 설명해주세요.
  - CPU: 명령어 해석과 실행, 산술 및 논리 연산, 제어와 타이밍 등이 있다. 명령어를 실행하기 위해서는 RAM에서 데이터 및 명령어를 가져와 해석하고, 이를 실행하는 역할을 한다. 주요 구성 요소로는 제어장치, 산술 논리 장치, 레지스터 등이 있다.
  - RAM: RAM은 주기억장치로, CPU가 직접 접근하여 데이터를 읽고 쓸 수 있는 메모리다. 프로그램 실행 중에 필요한 데이터와 명령어가 저장되어 있다. RAM은 휘발성 메모리이므로 전원이 꺼지면 내용은 손실된다.
  - 저장장치: 저장장치는 데이처를 영구적으로 저장하고 보전하는데 사용되며 대표적으로 HDD, SSD, 외부 저장장치 등이 있다. 주기억장치와는 달리 저장장치는 바휘발성이므로 전원이 꺼져도 데이터가 유지된다. 주로 운영체제나 응용프로그램 및 사용자 데이터가 저장된다.
  - ### 캐시 메모리의 개념과 종류, 역할에 대해 설명해주세요.
    - 캐시라는 개념은 데이터나 명령어에 대한 빠른 액세스를 위해 사용되는 임시 저장공간을 의미하며 다양한 컨텍스트에서 활용되며 성능 향상을 목적으로 사용된다.
    - 컴퓨터 구조에서의 캐시 메모리란 데이터나 명령어를 일시적으로 저장하는 고속의 임시 메모리로, 주로 CPU와 RAM 사이에 위치하며 CPU가 더 빠르게 데이터에 엑세스 할 수 있도록 한다.
    - 캐시 메모리는 속도가 빠른 장치와 느린 장치 사이에서 속도차에 따른 병목 현상을 줄이기 위한 범용 메모리를 지칭한다. CPU는 고속이지만 RAM은 비교적 저속이기 때문에 병목 현상을 완화해야 할 필요가 있다.
    - L1, L2, L3 캐시 등 다양한 레벨로 구성되어 있다.
    - L1: 일반적으로 CPU칩안에 내장되어 데이터 사용, 참조에 가장 먼저 사용된다. 8~64KB 정도의 용량으로 가장 빠르게 접근할 수 있으며 L1에서 데이터를 찾지 못하면 L2로 넘어간다.
    - L2: 용도와 역할은 L1과 비슷하지만 속도는 비교적 느리다. 일반적으로 64KB~4MB 정도가 사용된다. L1보다는 느리지만 RAM보다는 빠르니 성능 향상에 도움을 준다.
    - L3: 마찬가지로 동일한 원리로 작동하는데 웬만한 프로세서는 L3캐시 메모리를 달고있지 않다고 한다.  
  - ### CPU 아키텍처의 종류(ARM, x86)와 특징에 대해 설명해주세요.
    - ARM 아키텍처는 저전력이고 효율적인 구조로 모바일 기기나 임베디드 시스템에서 널리 사용된다.
    - x86 아키텍처는 주로 데스크톱 및 서버 시스템에 사용되며, intel 및 amd가 이 아키텍처를 기반으로 프로세서를 제공한다.
- ## 2. 운영체제의 역할과 iOS에서의 운영체제 구조에 대해 설명해주세요.
  - 운영체제는 자원관리, 자원보호, 하드웨어 / 소프트웨어 인터페이스를 제공하며 효율성, 안정성, 확장성, 편리성을 목표로 동작합니다.
  - iOS에서의 운영체제는 하위 계층부터 Core OS / Core Service / Media / Cocoa Touch / Application으로 구성되어 있으며, 하위 계층일수록 하드웨어에 가깝고 기본이 되는 층이며, 상위로 갈수록 사용자와 관련있는 계층입니다.
  - ### 프로세스와 스레드의 차이점, iOS에서의 프로세스와 스레드 관리 방법에 대해 설명해주세요.
    - 프로세스는 운영체제로부터 자원을 할당받는 작업의 단위이고, 스레드는 프로세스가 할당받은 자원을 이용하는 실행의 단위입니다.
    - 즉, 프로세스는 실행파일이 메모리에 적재되어 CPU를 할당받아 실행된느 것이고, 스레드는 한 프로세스 내에서 실행되는 동작의 단위입니다.
    - 프로세스는 메모리 공간에 code, data, heap, stack 영역이 있는데, 스레드는 프로세스내에서 stack영역을 제외한 code, data, heap 영역을 공유합니다.
    - iOS에는 Main과 Global Thread가 있으며 애플에서 제공하는 API인 GCD, NSOperation을 활용해 Multi Threading을 관리합니다.
  - ### 메모리 관리 기법 중 iOS에서 사용되는 방식과 그 특징에 대해 설명해주세요.
    - Swift에서는 ARC를 활용한다.
    - ARC는 메모리의 참조 횟수를 계산하여 참조 횟수가 0이 되면 메모리에서 해제하는 방식을 통해 메모리 관리를 하며 메모리 중 Heap 영역을 관리합니다.
  - ### iOS의 샌드박스 개념과 역할, 앱 간 데이터 공유 방법에 대해 설명해주세요.
    - iOS는 기본적으로 앱 마다 별도의 파일을 생성하여 공유되지 않도록 한다. 외부의 공격으로부터 앱이 손상된 경우, 시스템과 사용자 데이터의 피해를 최소화한다. 추가로 앱스토어를 통해 배포되는 모든 앱들은 App SandBox를 적용해야 한다. 다른 곳으로 유통하는 앱도 마찬가지이다.
    - 앱 간 데이터 공유 방법: AirDrop, URL Scheme, Document Interaction
- ## 3. iOS에서의 메모리 구조와 관리 방식에 대해 자세히 설명해주세요.
  - 1.메모리 구조
    - 프로그램이 실행되면 운영체제는 메모리(RAM)에 이 프로그램을 위한 공간을 할당해준다.
    - 그 공간은 4가지(Code, Data, Heap, Stack)으로 나뉘어져 있다.
    - 코드(Code)영역: 소스코드가 기계어 형태로 저장된다. 컴파일 타임에 결정되고, 중간에 코드가 변경되지 않도록 Read-Only 형태로 저장된다.
    - 데이터(Data)영역: 전역변수, static변수가 저장된다. 프로그램 시작과 동시에 할당되고, 프로그램이 종료 되어야 메모리가 해제된다. 실행 도중 변수 값이 변경될 수 있으니 Read-Write로 지정된다.
    - 힙(Heap)영역: 프로그래머가 할당/해제 하는 메모리영역. 유일하게 런타임 시 결정되기 때문에 데이터의 크기가 확실하지 않을 때 사용한다. 사용하고 난 후에는 반드시 메모리 해제를 해줘야한다.(leak 발생 가능). 스위프트에서는 클래스 인스턴스, 클로저 같은 참조 타입의 값들은 모두 힙에 자동 할당 된다. 스위프트는 ARC를 통해 힙에 할당된 메모리가 더 이상 쓸모 없어지면(참조되지 않으면) 자동으로 해제해준다. 메모리 크기에 대한 제한이 없고 본질적인 범위가 전역이기 때문에, 프로그램의 모든 함수에서 액세스 할 수 있다. 
    - 스택(Stack)영역: 함수 호출 시 함수의 지역변수, 매개변수, 리턴 값 등등이 저장되고, 함수가 종료되면 저장된 메모리도 해제된다. 컴파일 타임에 결정되기 때문에 무한히 할당할 수 없다. CPU가 스택 메모리를 효율적으로 구성하기 때문에 속도가 매우 빠르고 메모리를 직접 해제 하지 않아도 된다. 메모리 크기에 대한 제한이 있고, 지역 변수만 액세스 가능하다.
    - 데이터의 크기를 모르거나, 스택에 저장하기엔 큰 데이터의 경우엔 힙에 할당하고 그 외엔 스택에 할당한다.
    - 힙과 스택은 같은 메모리 공간이지만 힙 영역은 낮은 메모리 주소부터 할당 받는 것이고, 스택 영역은 높은 메모리 주소부터 할당 받는 것이다.
  - 2. 메모리 관리
  ```swift
    class Human {
        var name: String?
        var age: Int?
        init(name: String?, age: Int?) {
            self.name = name
            self.age = age
        }
    }
    let sodeul = Human(name: "Sodeul", age: 26)
  ```
  위 코드에서 sodeul이란 변수는 스택영역, Human 인스턴스는 힙영역에 저장된다. 따라서 사용하고 난 후에는 반드시 메모리 해제를 해줘야 하는데 스위프트에서는 ARC가 자동으로 관리해준다.
    - ARC는 클래스 인스턴스가 더 이상 필요하지 않을 때 메모리를 자동으로 해제한다.
  - ### 힙 영역에서 객체가 어떻게 할당되고 관리되는지 설명해주세요.
    - 참조타입의 값들이 힙에 자동할당되고, ARC를 통해 자동으로 관리된다.
  - ### 스택 영역에서 함수 호출과 로컬 변수의 메모리 할당 및 해제 과정을 설명해주세요.
    - 함수 호출 시 자동으로 메모리가 할당 및 해제된다.
- ## 4. 네트워크 프로토콜 스택과 iOS에서의 네트워크 통신 방식에 대해 설명해주세요.
  - 네트워크 프로토콜은 네트워크 통신을 위한 약속이다. 프로토콜 스택은 TCP/IP 4 계층과 OSI 7 계층 모델이 있다.
  - TCP/IP 4계층
    - Application: 웹 브라우징, 파일 전송, 이메일 등 애플리케이션에서 사용되는 프로토콜(HTTP, FTP, DNS등)
    - Transport: 프로세스를 식별하는 Port번호를 사용하여 데이터 전송, TCP와 UDP 같은 프로토콜을 사용하여 신뢰성을 보장
    - Internet: 큰 데이터를 작은 Packet으로 나누어 전송하거나 도착한 Packet을 다시 조립하는 역할, 서로 다른 네트워크를 연결하고 데이터를 라우팅하기 위해 IP 주소를 사용
    - Network Interface: 네트워크 매체에서 데이터 전송, MAC 주소를 사용하여 데이터 전송을 제어
  - ### HTTP와 HTTPS의 차이점, iOS에서의 보안 통신 방법에 대해 설명해주세요.
    - HTTP는 웹 브라우저와 웹 서버 간 데이터 전송을 위한 프로토콜로 사용자의 요청과 서버의 응답을 주고 받는다.
    - HTTPS는 Secure이 추가된 것으로 데이터 전송을 보호하는 프로토콜이다.
    - SSL/TLS 프로토콜을 사용하여 통신을 암호화 하여 개인정보 유출을 방지한다.
    - Apple은 ATSAPP Transport Security라는 네트워크 기능이 개인 정보 보호 및 데이터 무결성을 향상시킨다. 네트워크 통신을 HTTPS로 강제화 한다. 필요한 경우에는 예외를 등록할 수 있지만, 보안을 저하시키는 문제가 있다.
  - ### TCP와 UDP의 차이점에 대해서 설명해주세요.
    - 데이터를 보내기 위해 사용하는 프로토콜이다.
    - TCP는 1:1 통신방식으로 연결지향적이다. 연결지향적은 두 개체 간 연결 상태를 유지하고 교환이 가능한 것으로 논리적으로 이루어진 것이다. 쉽게 이야기하면 양측 협상으로 설정하고 데이터를 교환하고 연결을 종료한다. 신뢰성이 높지만 속도가 느리다. TCP/IP로 쓰이며, IP가 데이터의 배달을 처리한다면 TCP는 Packet을 추적하고 관리한다.
    - UDP는 비연결형 서비스로 순서화되지 않은 데이터그램 방식을 제공한다. 정보를 주고 받을 때 정보를 보내거나 받는다는 신호절차를 거치지 않는다. TCP보다 속도가 빠르지만 신뢰성이 낮다. 1:1뿐만 아니라 N:M등으로 연결될 수 있다.
  - ### 소켓 통신에 대해 설명해주세요.
    - 네트워크에서 두 개의 프로그램 간 양방향 데이터 전송을 가능하게 하는 통신 방식이다.
    - 클라이언트-서버 모델을 기반으로 작동하며, TCP/IP에서 Transport에 해당한다.
    - 파일 전송, 온라인 게임, 채팅, 원격 제어 등 다양하게 활용된다.
    - Socket을 생성하고 IP주소와 Port 번호를 가지고 통신하게 된다. 서버 측에서는 연결을 수락하고 데이터를 받은 뒤 연결을 끊는다.
  - ### REST API와 iOS에서의 네트워크 요청 및 응답 처리 방법에 대해 설명해주세요.
    - REST 아키텍처 스타일의 디자인 원칙을 준수하는 API이다. 이러한 이유로 RESTful API라고도 한다. HTTP 요청을 통해 통신함으로써 리소스 내에서 레코드의 작성, 읽기, 업데이트 및 삭제 등의 표준 데이터베이스 기능을 수행한다. GET 요청을 사용하여 레코드를 검색하고 POST로 요청을 PUT으로 업데이트를 DELETE로 레코드를 삭제한다.
    - 요청 헤더와 매개변수 역시 메타데이터, 권한 부여, URI, 캐싱, 쿠키 등의 식별자 정보를 포함하기에 REST API 호출에서 중요하다.
    - 요청 헤더와 응답 헤더는 일반적인 HTTP 상태 코드와 함께 사용된다.
- ## 5. iOS에서 메모리 사이즈와 관련된 개념과 고려 사항에 대해 설명해주세요.
  - 디바이스마다의 실제 메모리 RAM이 존재하고 앱이 실행되면 메모리를 사용하며 실행된다. 사용하려는 시스템은 메모리를 사용하다
  - ### 포인터 크기에 따른 메모리 사용량 차이와 고려사항
    - 64비트 포인터를 사용하면 개별 포인터 변수 크기가 증가하는 만큼 전체 메모리 사용도 늘어나겠지만, 메모리 주소 공간이 넓기에 활용적으로 사용 가능하다.
  - ### iOS 앱에서 대용량 데이터를 다룰 때 메모리 사이즈를 고렿나 최적화 방안 
    - 구조체 안에 포인터 변수가 많으면 메모리 사용량이 증가하기 때문에 데이터 구조의 선택에 있어서 맞게 선택해야 한다.
- ## 6. 알고리즘의 시간 복잡도와 공간 복잡도의 개념, 빅오 표기법에 대해 설명해주세요.
- ## 7. 자료구조의 종류와 iOS 개발에서 자주 사용되는 자료구조에 대해 설명해주세요.
  - 자료구조는 데이터를 효율적으로 사용할 수 있도록 정리하는 방법이다. 데이터 간의 관계 그리고 적용할 수 있는 함수나 명령을 의미한다.
  - 선형 자료구조와 비선형 자료구조로 나눌 수 있으며, 선형 자료구조는 데이터 요소를 순서대로 정렬하고 비선형 자료구조는 데이터를 비연속적으로 연결한다. 개별 요소에 접근하는 작업에는 선형 자료구조가 더 효율적이지만, 네트워크 연결과 같은 특정 문제를 효율적으로 해결하기 위해서는 비선형 자료구조가 더 알맞다.
  - ### 배열, 연결 리스트, 스택, 큐의 특징과 iOS에서의 구현 방법을 설명해주세요.
    - 배열은 연속적인 메모리 블록에 요소를 저장한다. 각 0부터 인덱싱된다.
    - swift에서는 capacity가 초기화 돨 때 일정 크기의 메모리 공간을 할당받으며, capacity보다 요소가 많이 추가되면 2배로 늘어난다.
    ```swift
      var arr = [Int]() // capacity = 0
      arr.append(1) // capacity = 1
      arr.append(2) // capacity = 2
      arr.append(4) // capacity = 4

      var newArr: [Int] = [1, 2, 3, 4, 5] // capacity = 5
    ```
    - 배열의 크기가 동적으로 변경될 수 있다는 말은 메모리 힙 영역에 저장된다는 말과 같다. 여기서 힙 영역에 저장되는 것은 배열의 데이터이며, 인스턴스 자체는 스택에 할당된다.
    - 연결 리스트는 배열과 마찬가지로 선형 데이터 구조이다. 인접한 메모리 주소로 저장되지 않는 점이 배열과 다르다. 다음 요소에 대한 주소 참조를 저장하는 entity와 데이터를 가지는 node로 연결되어 있다.
    ```swift
    class Node<T> {
      var value: T
      var next: Node?

      init(_ value: T) {
        self.value = value
      }
    }

    class List<T> {
      private var head: Node<T>?
      func append(_ value: T) {
        let newNode = Node(value)
        if head == nil {
          head = newNode
          return
        }

        var current = head
        while let next = current?.next {
          current = next
        }
        current?.next = newNode
      }
    }
    ```
    - 스택은 LIFO(후입선출) 규칙을 따르는 추가된 마지막 요소는 스택에서 제거하는 첫번째 요소이다.
    - 데이터를 넣는 push, 데이터를 제거하는 pop, 스택의 마지막 요소를 반환하는 peek이 있다.
    - 데이터 삽입, 삭제의 시간 복잡도는 O(1)이다.
    ```swift
    struct Stack<T> {
      private var array: [T] = []

      var peek: T? {
        return array.last
      }

      mutating func push(_ element: T) {
        array.append(element)
      }
      mutating func pop(_ element: T) {
        array.popLast(element)
      }
    ```
    - 큐는 FIFO(선입선출) 규칙을 따르는 가장 먼저 추가된 요소는 큐에서 제거하는 첫 번째 요소이다.
    - 데이터를 추가하는 enqueue, 데이터를 제거하는 dequeue, 큐의 앞쪽 데이터를 반환하는 front가 있다.
    - Queue에서 enqueue와 dequeue의 시간 복잡도는 O(1)이다.
    ```swift
    struct Queue<T> {
      private var array: [T] = []
      private var frontIndex = 0

      mutating func enqueue(_ element: T) {
        array.append(element)
      }

      mutating func dequeue() -> T? {
        guard !array.isEmpty else {
          return nil
        }

        if frontIndex < array.count {
          frontIndex += 1
          return array[frontIndex - 1]
        } else {
          return nil
        }
      }
    }
    ```
    - ### 해시 테이블의 개념, 충돌 해결 방법을 설명해주세요.
      - HashTable은 Key로부터 매핑된(key-value) 자료구조로 Hashing이라는 기술을 사용합니다.
      - 해시는 O(1)을 지향합니다. 데이터 개수 N과 무관하게 단번에 값을 찾아내겠다는 것입니다.
      - 주어진 키를 사용해서 실제 레코드의 주소를 직접적으로 계산해내는 것을 해시라고 합니다.
      - 해시 함수에 주어진 레코드의 키에 해시 함수를 가하면 그 레코드가 저장되어야 할 인덱스가 나오고, 키에 해시 함수를 가하여 채운 도표가 해시 테이블입니다.
      - 개방형 주소지정, 별도의 연결
      - 
    - ### 트리 자료구조의 종류를 설명해주세요.
        - 트리 구조는 하나의 루트 노드를 가지며, 0개 이상의 자식 노드를 갖고 있습니다. 그 자식 노드 또한 0개 이상의 자식 노드를 갖고 있는 계층적 관계를 표현합니다.
        - 이진 트리는 자식 노드가 왼쪽 그리고 오른쪽 노드 최대 2개가를 갖는 트리 자료구조입니다.
        - 이진 탐색 트리는 노드의 값이 유일한 특성이 있습니다. 왼쪽 자식 노드는 루트 노드보다 값이 작고, 오른쪽 자식 노드는 루트 노드의 값보다 큽니다. 검색, 삽입, 삭제 연산의 시간 복잡도는 O(logN)입니다.
        - AVL 트리는 모든 노드의 왼쪽 서브 트리와 오른쪽 서브 트리의 높이 차이가 최대 1이어야 합니다. 조건을 만족하기 위해 노드의 회전 연산을 통해 트리를 재구성합니다. 검색, 삽입, 삭제의 시간 복잡도는 O(logN)으로 유지할 수 있습니다.
- ## 8. 동시성 프로그래밍의 개념과 iOS에서의 동시성 처리 방식에 대해 설명해주세요.
  - 여러 계산이 순차적이지 않고 겹치는 기간 동안 동시에 실행되어 다음 계산이 시작되기 전에 하나가 완료되는 프로그래밍의 한 형태이다.
  - ### 병렬 처리와 동시 처리의 차이, iOS에서의 멀티코어 활용 방안에 대해 설명해주세요.
    - 병렬 처리는 동일한 물리적 순간에 발생한다. 실제로 동시에 수행하기 위해 멀티 코어를 이용하여 작업을 분산화하여 처리한다. 동시처리는 여러 작업이 시간적으로 겹쳐서 진행되는 것처럼 보이는 것을 의미한다. 즉, 하나의 CPU 코어가 여러 작업을 교차실행하는 방식이다.
    - 멀티 코어를 사용하는 경우는 GPU를 사용하는 경우에 사용될 수 있다. 그래픽 작업을 하는 Metal 혹은 머신 러닝 관련 작업을 하는 CoreML에 사용된다. 
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
        
