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
