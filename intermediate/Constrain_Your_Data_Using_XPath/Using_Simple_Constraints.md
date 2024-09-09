# 단순 제약 조건 사용하기(Using Simple Constraints)
- 모든 path에 나온 예제를 캡처해서 올리지 않고 부분 부분 이해가 잘 되지 않거나 하는 부분만 따로 캡쳐해서 올리도록 하겠습니다.
- https://academy.mendix.com/link/modules/220/lectures/1719
## 학습 목표
- Enumeration이란 무엇인지 설명할 수 있다: Enumeration은 데이터의 특정 집합을 정의하고, 각 항목에 고유한 값을 부여하는 방법입니다. 이는 선택 항목이 제한된 목록을 제공할 때 유용합니다.
- Enumeration 값을 사용하여 데이터를 제약할 수 있다: Enumeration 값을 활용하여 데이터 필터링 및 제약을 설정할 수 있습니다. 이를 통해 특정 범위의 값만을 선택하여 데이터를 더 정밀하게 관리할 수 있습니다.
- Mendix 시스템 변수를 사용하여 제약할 수 있다: Mendix 시스템 변수를 사용하여 데이터 제약을 설정할 수 있습니다. 시스템 변수를 통해 현재 사용자나 시스템의 상태에 따라 동적인 제약 조건을 적용할 수 있습니다.
- XPath 제약을 사용하여 보안 규칙을 적용할 수 있다: XPath 제약을 통해 데이터 접근 및 보안 규칙을 설정할 수 있습니다. 이를 통해 사용자나 역할에 따라 데이터 접근을 제한하고, 보안 규칙을 효과적으로 적용할 수 있습니다.

## 휴가 요청 앱 만들기 시작하기(Start Building the Vacation Request App)
### 1. 새로운 앱 만들기(Create a New App)
- [create app 링크](https://academy.mendix.com/link/modules/220/lectures/1706/3.1-Start-Building-the-Vacation-Request-App)
- [멘딕스 포](https://sprintr.home.mendix.com/index.html)
- ![image](https://github.com/user-attachments/assets/776706aa-ce61-4128-952f-fd66955681bd)
- ![image](https://github.com/user-attachments/assets/faf4cb3e-bd1f-4b93-ab69-e8cd1dd74cc0)

### 2. Mendix Version Error
- ![image](https://github.com/user-attachments/assets/0b6702fa-eceb-40ef-b1b4-042e7100dbc1)
- [멘딕스 릴리즈 버전별 다운 받는 방법](https://marketplace.mendix.com/link/studiopro)
- ![image](https://github.com/user-attachments/assets/0db74280-cc58-4ddf-977b-2264b73c5dc3)
- 후에 해당 버전 mendix 다운로드 창이 나옵니다 그것까지 해주면 됩니다.

### 3. Enumeration
- 현재 상태의 앱에 로그인하는 사용자는 메인 대시보드에서 혼란을 느낄 수 있습니다. 직원이 만든 모든 요청을 한 화면에서 보는 것은 유용하지 않습니다. 더 나은 대시보드를 제공하기 위해 홈 화면의 보기를 '제출된' 요청만 표시하고, 나머지 요청들은 '보관함' 탭에 표시하도록 제한할 것입니다. 이를 달성하기 위해 '상태(Status)' 열거형(Enumeration)을 사용할 것입니다.
- ![image](https://github.com/user-attachments/assets/ee55d013-fe90-4e48-b12c-a343a37e59bf)
- 해당 작업을 통해서 XPath를 통해 제약 조건을 걸어서 해당 status attribute가 submitted 상태인 경우에안 화면에 노출되게 됩니다.


### 4. Mendix 시스템 변수를 사용하기(Using Mendix System Variables)
- 열거형 자동 완성 외에도, Mendix 플랫폼에는 XPaths를 작성할 때 사용할 수 있는 여러 시스템 변수가 있습니다.
- 여기에는 현재 사용자, 사용자 역할, 현재 세션, 여러 날짜 및 시간을 참조하는 변수가 포함되어 있어 데이터를 더 잘 제어할 수 있게 합니다.
- 이러한 변수는 항상 [%로 시작하며, Ctrl + Space 자동 완성 메뉴를 통해 찾을 수 있습니다.

##### 가장 유용한 시스템 변수 중 두 가지는 [%CurrentObject%]와 [%CurrentUser%]입니다.
**참고: XPath 변수에 대한 전체 목록은 XPath 키워드 및 시스템 변수 참조 자료에서 확인할 수 있습니다.**

##### Current Object (현재 객체)
[%CurrentObject%] 변수는 현재 컨텍스트 객체의 고유 식별자를 나타냅니다. 실질적으로, 이 변수는 데이터 뷰에 포함된 데이터 그리드의 경우 데이터 뷰의 객체를 나타냅니다. 데이터 뷰의 객체는 컨텍스트 객체라고 불립니다. 만약 컨텍스트 객체가 없다면, 이 변수는 자동 완성 메뉴에 나타나지 않습니다.

##### Current User (현재 사용자)
CurrentObject와 마찬가지로, Mendix 플랫폼은 애플리케이션의 현재 사용자를 간단히 참조할 수 있는 방법을 제공합니다. 이는 [%CurrentUser%] 변수를 통해 이루어지며, Ctrl + Space 드롭다운 메뉴에서 찾을 수 있습니다. [%CurrentUser%]는 XPaths가 사용되는 모든 위치에서 사용할 수 있으며, 보안 제약 조건을 만들 때도 유용합니다. 우리는 이 변수를 사용하여 애플리케이션의 보안을 강화할 것입니다.

**참고: [%CurrentUser%] 변수는 예약된 이벤트(Scheduled Events) 및 After Startup 마이크로플로우와 같은 시스템 프로세스에서는 사용하지 마세요. 그 시점에는 사용자가 존재하지 않습니다!**

#### 4.1 Mendix 시스템 변수를 사용한 제약 조건 추가하기 (Using Mendix System Variables)

#### 4.2 Role Security 추가하기
![image](https://github.com/user-attachments/assets/91dd9b1c-487d-4d73-8107-4f1866e1eb6f)

#### 4.3 

## 퀴즈
### Question 1
How do you begin typing an XPath?

Your answer: [

Explanation: To start typing an XPath expression in Mendix, you begin with an open bracket [. This signals the beginning of an XPath constraint where you will specify conditions to filter data.

해설: XPath 표현식을 작성할 때, 브래킷 [로 시작하여 데이터 필터링 조건을 지정합니다. 이는 XPath 제약조건의 시작을 나타내며, 조건을 입력할 준비가 됨을 의미합니다.

### Question 2
If you want to open the XPath auto-complete menu, you need to press:

Your answer: Ctrl + Space

Explanation: Pressing Ctrl + Space opens the XPath auto-complete menu in Mendix. This feature helps you to see available attributes, associations, and system variables as you type, making it easier to construct valid XPath expressions.

해설: Ctrl + Space를 누르면 XPath 자동 완성 메뉴가 열립니다. 이 기능은 입력 중에 사용 가능한 속성, 연관관계 및 시스템 변수를 보여줘서 유효한 XPath 표현식을 더 쉽게 구성할 수 있도록 도와줍니다.

### Question 3
Say you are writing an XPath in a Retrieve action for the VacationRequest entity in a Microflow. If you write in the XPath window [Status = ‘Cancelled’], what will be returned?

Your answer: A list of all requests with the status set to ‘Cancelled’.

Explanation: The XPath [Status = ‘Cancelled’] will filter and return only those VacationRequest entities where the Status attribute is set to 'Cancelled'. This means that you will get a list of vacation requests that have been cancelled.

해설: XPath [Status = ‘Cancelled’]는 Status 속성이 'Cancelled'로 설정된 VacationRequest 엔티티만 필터링하여 반환합니다. 따라서, 취소된 휴가 요청의 목록이 반환됩니다.

### Question 4
Say you are writing an XPath in a Retrieve action on the VacationRequest entity in a Microflow. If you write in the XPath window [VacationRequest.VacationRequest_Submitter='[%CurrentUser%]'], what will be returned?

Your answer: A list of all vacation requests submitted by the current user.

Explanation: The XPath [VacationRequest.VacationRequest_Submitter='[%CurrentUser%]'] will filter the VacationRequest entities to only those where the VacationRequest_Submitter attribute is equal to the current user. This will return a list of vacation requests that have been submitted by the currently logged-in user.

해설: XPath [VacationRequest.VacationRequest_Submitter='[%CurrentUser%]']는 VacationRequest_Submitter 속성이 현재 사용자와 동일한 VacationRequest 엔티티만 필터링하여 반환합니다. 따라서, 현재 로그인한 사용자가 제출한 휴가 요청 목록이 반환됩니다.


