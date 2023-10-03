# iOSInterview
iOS 면접 질문 정리


# iOS
- Bounds와 Frame의 차이를 설명하시오.
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
    
- 실제 디바이스가 없을 경우 개발환경에서 할 수 있는 것과 할 수 없는 것을 설명하시오.
