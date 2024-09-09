# 더 복잡한 제한 사항 사용하기
## 1. 학습 목표
By the end of this module, you will be able to:
1. Constrain data using the UserRole system variable
- 사용자 역할 시스템 변수를 사용하여 데이터 제한하기
2. Write XPaths using Operators and Functions
- 연산자와 함수를 사용하여 XPath 작성하기
3. Use DateTime tokens in XPaths
- XPath에서 DateTime 토큰 사용하기
4. Perform an empty check on data using XPaths
- XPath를 사용하여 데이터의 비어있는지 확인하기

# 사용자 역할 시스템 변수란? (What is the UserRole System Variable?)
## 1. 의의
- 이전 모듈에서는 '[%CurrentObject%]'와 '[%CurrentUser%]'와 같은 Mendix XPath 변수를 배웠습니다. 또한, 플랫폼이 열거형을 사용하여 XPath를 구성하는 데 어떻게 도움을 줄 수 있는지 배웠습니다. 이번 모듈에서는 **사용자 역할 시스템 변수를 사용**하여 계정을 역할에 따라 제한하는 방법을 배울 것입니다.
- 보안 문서에서 사용자 역할을 생성하면, Mendix는 자동으로 해당 역할에 대한 시스템 변수를 생성합니다. 예를 들어 '[%UserRole_Manager%]'와 같은 변수가 생성됩니다. 이 변수는 XPath가 시스템 모듈의 UserRole 엔터티와의 연관으로 끝날 때만 자동 완성 메뉴에 나타납니다.
    - 사용자 역할 생성 -> 멘딕스가 자동으로 해당 역할에 대한 시스템 변수를 생성한다.
- 이 연관성은 계정 선택을 특정 사용자 유형으로 제한하는 데 유용합니다. 다음 강의에서는 이 기능을 사용하여 사용자가 자신의 휴가 요청을 승인할 승인자를 선택할 수 있도록 하는 방법을 배울 것입니다.
## 2. 사용법
### 2.1 UserRole 변수를 사용하여 데이터 제약하기
현재 애플리케이션에서는 사용자가 새로운 휴가 요청을 생성할 수 있지만, 승인자를 선택할 수 있는 메커니즘이 없습니다. 첫 번째 반복에서는 비즈니스 결정으로 관리자가 자신의 승인자를 선택할 수 있어야 하며, 다른 사용자의 승인자로는 오직 관리자만 선택할 수 있어야 합니다.

이를 구현하기 위해 애플리케이션에서 Reference Selector에서 선택할 수 있는 객체를 XPath를 사용하여 제한합니다. 그 후, VacationRequest_NewEdit 페이지에서 저장 버튼을 수정하여 마이크로플로우를 호출하고 휴가 요청의 상태를 'Submitted'로 설정하도록 합니다.

### 2.2 올바른 Reference Selector 찾기
1. VacationRequest_NewEdit 페이지를 엽니다.
2. 이 페이지에서 VacationRequest_Submitter 연관 관계를 설정하는 Reference Selector 위젯을 찾습니다. 두 개의 Account 위젯의 속성을 열어야 할 수 있습니다. 이 위젯들은 페이지가 생성될 때 자동으로 생성된 것입니다.
3. Submitter 위젯의 Edit Reference Selector 팝업을 엽니다.
    - 기본적으로 이 필드는 "Account"라는 레이블이 붙어 있습니다. 레이블 캡션 속성을 "Submitter"로 변경합니다.
    - OK를 클릭합니다.
4. VacationRequest_Approver 연관 관계에 대해서도 같은 절차를 수행합니다.
    - 레이블 캡션을 "Approver"로 변경합니다.

### 2.3 XPath를 사용하여 선택 가능한 계정 제한하기
1. VacationRequest_Approver Reference Selector 위젯의 속성 창에서 Selectable objects 탭을 클릭합니다.
2. 이 탭에서 Source를 XPath로 설정합니다.
3. XPath 자동 완성 도구를 사용하여 모든 시스템 사용자 역할에 해당하는 시스템 변수를 확인할 수 있습니다. "Manager" 역할에 대한 변수를 선택합니다. 즉, 완성된 XPath는 다음과 같아야 합니다:
```xpath
[System.UserRoles='[%UserRole_Manager%]']
```
4. OK를 클릭합니다.
이제 관리자로 로그인한 사용자가 이 페이지를 열어 요청에 대한 'Approver'를 선택할 때, 드롭다운 목록에는 'Manager' 사용자 역할이 할당된 사용자만 표시됩니다!

### 2.4 기능 테스트하기
이 기능을 테스트하려면 'Employee' 사용자 역할을 가진 사용자로 로그인할 수 있어야 합니다. 계정을 만들려면 Administration.AccountOverview 페이지를 애플리케이션 탐색에 추가합니다. 탐색에도 로그아웃 액션을 추가하는 것을 잊지 마세요!
- ![image](https://github.com/user-attachments/assets/7330b237-ac21-42c7-9977-e010ec103a4e)
- ![image](https://github.com/user-attachments/assets/23839218-9d5a-4a4a-b1e7-901564f6ea69)
- ![image](https://github.com/user-attachments/assets/532b421b-d6df-4921-928d-2df04d93e0e8)
    - 해당 페이지에 해당 권한을 넣어주면 navigation에 해당 User Roles가 들어갑니다.

이제 MxAdmin 사용자로 로그인하고 해당 페이지에서 계정을 생성할 수 있습니다. 두 개의 'Employee' 역할을 가진 계정과 두 개의 'Manager' 역할을 가진 계정을 생성하여 수행한 작업을 테스트해 보세요.

- 'Employee' 역할을 가진 사용자로 로그인하고 요청을 제출합니다.
- 로그아웃한 후 MxAdmin으로 다시 로그인합니다.
- 관리자는 제출된 요청 목록을 보고 요청을 열어 'Approver' 레이블이 붙은 드롭다운을 사용하여 승인자를 지정할 수 있습니다. 필드에 나타나는 이름은 'Manager' 사용자 역할이 할당된 계정만 포함됩니다.

# XPath 표현식
- [XPath 표현식 공식 문서](https://docs.mendix.com/refguide/xpath-expressions/)
 
# XPath 함수
- [XPath 함수 공식 문](https://docs.mendix.com/refguide9/xpath-constraint-functions/)

