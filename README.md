# Unity-Study

studies of unity and C#

- 유니티 기본 인터페이스

  - Project(프로젝트): 게임을 구성하는 파일들을 관리하는 영역
  - Hierachy(계층구조): 게임 오브젝트 확인/생성
  - Scene(장면): 게임 오브젝트들이 보이는 공간
  - Inspector(인스펙터): 게임 오브젝트들의 속성 확인

- Scene

  - Q: 뷰 이동
  - W: 오브젝트 이동
  - E: 오브젝트 회전
  - R: 크기 조절
  - T: 사각툴, 크기 조절과 UI에 주로 사용

  - 카메라 제어
    - Mouse_Right: 카메라 회전
    - Alt + Mouse_Left: 바라보고 있는 오브젝트를 기준으로 카메라 축 이동
    - 방향키: 카메라 자유이동

- 스크립트 파일 생성

  - 스크립트 파일은 C# Script

- 스크립트 파일 주기

  - Hierachy에서 오브젝트 더블클릭으로 선택 -> 인스펙터 창에 Drag & Drop

- 클래스와 변수

  - 클래스 내에서 선언한 변수는 default로 'private'라는 접근자를 달고 있음
  - 다른 클래스에서 클래스 내의 멤버 변수를 사용하려면 'public'이라는 접근자를 달아주어야 함
  - public으로 설정된 멤버 변수는 외부 클래스에 공개 상태로 전환됨

- 클래스의 상속

  - 클래스의 상속(Inheritance)는 부모 클래스와 자식 클래스간의 관계이다.
  - 자식 클래스는 부모 클래스의 속성을 모두 물려받는다.
  - 부모 클래스의 모든 멤버 변수와 함수를 사용할 수 있으면서도, 자기 자신의 새로운 멤버 변수와 함수를 사용할 수 있다.

  - NewBehaviourScript 앞에 붙은 : MonoBehaviour는 유니티 게임의 오브젝트 클래스이다.

- 게임 오브젝트의 흐름

  - 초기화 영역

    - Awake(): 게임 오브젝트를 생성할 때 최초 실행하는 함수, 최초 1회 실행
    - Start(): 업데이트 시작 직전, 최초 1회 실행

  - 활성화 영역
    - OnEnable: 게임 오브젝트가 활성화되었을 때마다 실행
  - 비활성화
  - 프레임 단위 실행

    - 물리 영역

      - FixedUpdate(): 물리 연산 업데이트, 고정된 실행 주기(초당 50번)로 CPU 사용
        - 주로 물리 연산과 관련된 로직만 넣음

    - 게임로직 영역

      - Update(): 게임 로직 업데이트
      - 컴퓨터 환경에 따라 실행 주기가 달라질 수 있음

    - LateUpdate(): 모든 로직들이 끝난 뒤에 마지막으로 실행되는 함수
      - 로직 후처리, 카메라 제어 등

  - 비활성화 영역

    - 게임 오브젝트가 비활성화될 때마다 실행

  - 해체 영역
    - OnDestroy(): 게임 오브젝트가 삭제될 떄

- Input과 Key 종류

  - Parameter 없음:

    - anyKey: 마우스 및 키보드
      - anyKeyDown
      - anyKey
      - anyKeyUP

  - Parameter로 키 종류를 받음

    - Parameter 전달 방식

      - KeyCode.{키 이름}
      - "Input Manager의 Axe 이름"

    - GetKey: 키보드 버튼

      - GetKeyDown
      - GetKey
      - GetKeyUp

    - GetMouseButton: 마우스 버튼

      - GetMouseButtonDown
      - GetMouseButton
      - GetMouseButtonUp

      - MouseButton(0): 왼쪽 버튼
      - MouseButton(1): 오른쪽 버튼

  - GetAxis
    - GetAxis: 가중치를 포함한 값을 리턴
    - GetAxisRaw: 가중치를 무시하고 값을 리턴

- Transform

  - 오브젝트 형태에 대한 기본 component

  -transform.Translate(Vector3);

  - transform에 Vector3로 정의된 벡터 값을 더함

  - Vector3 정의
    ```cs
      Vector3 vec = new Vector3(0, 0, 0);
    '''
    ```

- 목표 지점까지의 이동: Vector3 내장 메소드 활용

  - MoveTowards: 등속 이동

    ```cs
      transform.position =
          Vector3.MoveTowards(transform.position, target, 1f);
    ```

    - Parameters
      - 현재 위치
      - 목표 위치
      - 속도

  - SmoothDamp: 부드러운 이동

    ```cs
      transform.position =
            Vector3.SmoothDamp(transform.position, target, ref velo, 1f);
    ```

    - Parameters
      - 현재 위치
      - 목표 위치
      - 참조 속도
      - 속도
    - 4번째 parameter와 속도가 반비례함

  - Lerp: 선형 보간, SmoothDamp보다 감속시간이 길다

    ```cs
      transform.position =
            Vector3.Lerp(transform.position, target, ref velo, 1f);
    ```

    - Parameters
      - SmoothDamp와 같다
    - 4번째 parameter와 속도가 비례함, 최대값은 1f

  - SLerp: 구면 선형 보간, 원호를 그리며 이동
    ```cs
    transform.position =
            Vector3.Slerp(transform.position, target, ref velo, 1f);
    ```

- Time.deltaTime
  - deltaTime 값은 프레임이 작으면 크고, 프레임이 크면 작음
  - 프레임률에 따라 실행 결과가 달라지지 않게 하기 위함

