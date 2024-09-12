[Adding Requests](https://academy.mendix.com/link/modules/184/lectures/5075/Learning-Objectives)

# 학습 목표
- Mendix 마법사 페이지 템플릿 중 하나를 사용하여 요청 마법사를 설정할 수 있습니다.
- 참조 세트 선택기를 구성할 수 있습니다.
- 데이터 그리드에서 단일 및 다중 선택을 설정할 수 있습니다.
- 최종 제출 전 요청을 확인하는 페이지를 구성할 수 있습니다.
- 사용자 정의 탐색 레이아웃을 동적으로 만들 수 있습니다.

#  기본 사항 설정하기
## 1. 선행작업
마법사를 만들기 전에, 도메인 모델을 확장하여 앱에서 요청과 프로젝트를 동적 데이터로 처리할 수 있도록 해야 합니다.

## 2. 진행 과
1. **Expenses 모듈의 도메인 모델을 엽니다.**

2. **Project 엔터티 추가:**
    - 속성:
        - Number (Autonumber)
        - Name (String)
    - Project 엔터티의 액세스 규칙 구성:
        - Requestor 사용자 역할: Create 및 Read, Write 액세스 부여. Autonumber 속성은 자동으로 Read 액세스만 부여됩니다.
        - Approver 사용자 역할: Read 액세스 부여.

3. **Request 엔터티 추가:**
    - 속성:
        - Title (String)
        - Status (Enumeration | ENUM_Status; 'New', 'Approved', 'Rejected', 기본값 'New')
        - Location (Enumeration | ENUM_Location; 'Boston', 'Rotterdam')
        - TotalAmount (Decimal)
    - 시스템 멤버 선택:
        - 'createdDate' 저장
        - 'changedDate' 저장
        - 'owner' 저장
        - 'changedBy' 저장
    - Project 엔터티와 *-* 연관 관계 추가. Request가 연관 관계의 소유자가 됩니다.
    - Request 엔터티의 액세스 규칙 구성:
        - Requestor 사용자 역할: Create 액세스 부여. TotalAmount 및 RequestID에 Read 액세스 부여. Title, Status, Location 속성과 Request_Project 연관 관계에 대해 Read, Write 액세스 부여. 이 구성은 Requestor가 해당 객체의 소유자인 경우에만 액세스할 수 있도록 합니다.
        - Approver 및 Administrator 사용자 역할: Read 액세스 부여.

4. **RequestLine 엔터티 추가:**
    - 속성:
        - Description (String)
        - Price (Decimal)
    - Request 엔터티와 1-* 연관 관계 추가. 1개의 Request가 여러 RequestLines를 가질 수 있습니다.
    - RequestLine 엔터티의 액세스 규칙 구성:
        - Requestor 사용자 역할: Create, Delete 및 Read, Write 액세스 부여.
        - Approver 사용자 역할: Read 액세스 부여.

#  The Wizard Page Template
## 1. wizard 생성하기(Creating the Wizard)
이제 페이지의 기초를 구축하고 각 페이지가 어떻게 상호작용할지를 설정해 보겠습니다. 이 기능은 앱에서 독립적인 기능으로 식별되기 때문에, 페이지 및 마이크로플로우와 같은 관련 문서를 저장할 새 폴더를 생성하는 것이 좋습니다.
### 1.1 생성 순서
1. **새 폴더 생성:**
   - `Expenses` 모듈에 `Request`라는 새 폴더를 추가합니다.

2. **세 페이지 생성:**
   - 마법사 양식 페이지 템플릿을 사용하여 세 페이지를 만듭니다.
     - 이름: `Request_Wizard_Step1`, `Request_Wizard_Step2`, `Request_Wizard_Step3`
     - 네비게이션 레이아웃: `Atlas_TopBar`
     - 새로 생성된 `Request` 폴더에 저장합니다.

3. **페이지 단계 설정:**
   - 각 페이지의 단계가 올바른 클래스 이름을 갖도록 해야 합니다. 기본적으로 템플릿에서는 2단계에 `wizard-step wizard-step-active` 클래스가 설정되고 1단계에는 `wizard-step wizard-step-visited` 클래스가 설정됩니다. 이 클래스 이름은 단계 번호를 감싸는 컨테이너에 설정됩니다. 아래 단계를 따라 설정하세요:
     - 모든 페이지에서 4단계 컨테이너를 제거합니다.
     - 첫 번째 페이지에서 1단계에 `wizard-step wizard-step-active`, 2단계와 3단계에 `wizard-step` 클래스 이름을 설정합니다.
     - 두 번째 페이지는 클래스 이름을 변경할 필요가 없습니다.
     - 세 번째 페이지에서는 1단계와 2단계에 `wizard-step wizard-step-visited`, 3단계에 `wizard-step wizard-step-active` 클래스를 설정합니다.

4. **헤더를 스니펫으로 변환:**
   - 페이지 상단의 헤더를 스니펫으로 변환하여, 한 번만 입력하고 세 페이지에서 재사용할 수 있도록 합니다. 스니펫을 사용하면 내용을 변경했을 때 앱 전체에서 자동으로 업데이트되므로, 나중에 마법사의 헤더를 변경해야 할 경우 한 번만 수정하면 됩니다.
     - 마법사 헤더를 감싸는 가장 바깥쪽 컨테이너를 선택합니다.
     - 컨테이너를 우클릭하고 `Extract snippet...`을 클릭합니다.
     - 스니펫 이름: `Wizard_Header`
     - 스니펫의 텍스트를 수정합니다.
     - 스니펫을 `Request` 폴더의 `Resources` 하위 폴더로 이동합니다.
     - 각 마법사 페이지에서 현재 헤더를 스니펫으로 교체합니다 (`Snippet call` 위젯을 사용하거나 App Explorer에서 `Wizard_Header` 스니펫을 드래그 앤 드롭합니다).

5. **데이터 뷰 연결:**
   - 각 페이지의 데이터 뷰를 `Request` 엔터티에 연결합니다.
     - 데이터 소스: `Context`
     - 데이터 뷰의 내용을 자동으로 채우지 않습니다.
     - 데이터 뷰의 내용을 비웁니다.

## 2.  마법사에 내비게이션 추가하기
### 2.1 필요성
- 마법사에서 중요한 것은 사용자가 다음 단계로 어떻게 이동할지, 어떤 데이터를 전달할지, 그리고 언제 데이터를 데이터베이스에 저장할지를 고려하는 것입니다.
### 2.2 순서
다음 단계를 따라 마법사의 버튼을 조정하세요. 각 페이지에는 진행을 위한 두 개의 버튼이 필요하며, 하나는 앞으로 이동하고 다른 하나는 뒤로 이동합니다. 첫 번째와 마지막 페이지는 각각 취소(Cancel)와 완료(Finalize) 버튼이 필요합니다.
1. **1단계: 요청 취소**
   - 직원이 1단계에 있을 때는 요청을 취소할 수 있어야 합니다. 이를 위해 Previous 버튼의 설정을 다음과 같이 변경합니다:
     - 캡션을 "Cancel Request"로 변경
     - 스타일을 Default로 선택
     - 클릭 시 액션을 "Cancel changes"로 설정하고, 페이지 닫기 옵션을 Yes로 설정합니다.
2. **3단계: 요청 완료**
   - 직원이 3단계에 있을 때는 요청을 완료하고 이를 데이터베이스에 저장할 수 있어야 합니다. 이를 위해 Next 버튼을 기본 Save 버튼으로 변경하고, 캡션을 "Finalize request"로 변경합니다.
3. **페이지 간 이동:**
   - 각 단계에서 다음 페이지로 이동하기 위해 다음 작업을 수행하세요:
     - 마법사의 현재 단계를 닫는 "Close page" 활동과 다음 단계를 여는 "Show page" 활동을 포함하는 마이크로플로우를 생성합니다. Show page 활동에서는 Request 객체가 변수 `$Request`로 자동 전달됩니다.
   - 이전 페이지로 돌아가기 위해서는 비슷한 마이크로플로우를 생성하되, 이번에는 다음 페이지가 아닌 이전 페이지를 엽니다.
   - Requestor 모듈 역할에 생성된 마이크로플로우에 대한 액세스 권한을 부여합니다.
4. **버튼 스타일 변경:**
   - 각 페이지에서 버튼 스타일을 아래와 같이 설정합니다:
   - **1단계 버튼:**
     - 취소 버튼: 기본 스타일(Default)로 설정
     - 다음 버튼: 기본 스타일(Default)로 설정
   - **2단계 버튼:**
     - 이전 버튼: 기본 스타일(Default)로 설정
     - 다음 버튼: 기본 스타일(Default)로 설정
   - **3단계 버튼:**
     - 이전 버튼: 기본 스타일(Default)로 설정
     - 완료 버튼: 기본 스타일(Default)로 설정
# Reference Set Selector
## 1. 설명
- 이제 Request Wizard의 기본 구성을 완료했으니, 1단계를 마무리할 차례입니다. 이 페이지에서는 직원들이 필요한 물품의 위치(보스턴 또는 로테르담)를 선택하고, 요청이 속하는 프로젝트를 선택하게 됩니다.
- 직원들은 요청에 대해 여러 프로젝트를 선택할 수 있으며, 필요시 새로운 프로젝트를 바로 생성할 수 있어야 합니다. 여러 프로젝트를 선택하는 기능은 **Reference Set Selector** 위젯을 통해 구현할 수 있습니다.
- Reference Set Selector는 Mendix에서 연관된 객체를 선택하는 데 사용하는 위젯입니다. 이 옵션은 다중 선택이 가능한 경우, 즉 * - * 관계가 있을 때 사용할 수 있습니다.
- 이 위젯을 구성할 때 옵션을 드롭다운 또는 선택 페이지에 표시할 수 있습니다. 선택할 객체의 목록이 매우 길 경우, 선택 페이지에 표시하는 것이 좋습니다. 이렇게 하면 목록이 나중에 로드되어 초기 페이지 로딩 속도가 빨라지며, 사용자에게는 더 친숙한 방식이 됩니다. 긴 드롭다운 목록을 스크롤할 필요가 없어지기 때문입니다.

## 2. Complete the First Page of the Wizard
### 2. 단계 설명
1. **Request_Wizard_Step1 페이지 열기:**
   - 페이지의 제목을 "Select the project"와 같은 적절한 제목으로 변경하세요.

2. **Radio buttons 위젯 추가:**
   - Location 속성에 대해 Radio buttons 위젯을 추가합니다.

3. **Text box 위젯 추가:**
   - Radio buttons 위젯 아래에 Text box 위젯을 추가하고, 캡션을 "Request Title"로 설정합니다.
   - 데이터 소스를 Data view의 Title 속성에 연결합니다.

4. **Input reference set selector 추가:**
   - Text box 위젯 아래에 Input reference set selector를 추가합니다. 이를 통해 사용자가 하나 이상의 프로젝트를 선택할 수 있습니다.
   - Input reference set selector를 Project 엔터티의 Name 속성에 연결합니다 (Request_Project 연관을 사용).

5. **Input Reference Set Selector에서 선택 페이지 생성:**
   - Input Reference Set Selector 위젯을 우클릭하고 **Generate select page...**를 클릭합니다.
   - 페이지 이름: Project_Select
   - 네비게이션 레이아웃: PopupLayout
   - 페이지 템플릿: Select With Data Grid

6. **Project_Select 페이지 열기:**
   - Select 버튼을 우클릭하고, 그 오른쪽에 Create 버튼을 추가합니다.

7. **새로운 버튼 속성 설정:**
   - 버튼 스타일을 성공(Success)으로 설정합니다.
   - 편집 위치를 "Inline at top"으로 설정합니다.

8. **Name 열을 편집 가능하게 설정:**
   - Name 열을 더블 클릭하여 열을 편집 가능하게 만듭니다.

# Single and Multi-Select on a Data Grid
- 이제 마법사의 두 번째 페이지를 마무리할 시간입니다. 이 페이지에서 요청자는 하나 이상의 요청 라인을 요청에 추가할 수 있습니다. 또한, 기존 요청 라인을 하나씩 편집할 수 있어야 하며, 마지막으로 기존 요청 라인을 여러 개 한 번에 삭제할 수 있어야 합니다.
- 이 기능을 구축하려면 단일 및 다중 선택을 지원하는 데이터 그리드를 추가해야 합니다. 여기서 단일 선택(편집) 및 다중 선택(삭제)을 지원하는 버튼을 추가해야 합니다.
- 다중 선택을 지원하는 데이터 그리드에서는 기본 편집(Edit) 및 삭제(Delete) 버튼이 작동하지 않습니다. 이러한 기본 버튼은 단일 선택 모드의 데이터 그리드에서만 작동합니다. 여전히 편집 및 삭제 기능을 제공하기 위해서는 두 개의 액션 버튼을 추가하고, 각각의 버튼이 마이크로플로우를 트리거하도록 설정해야 합니다.
