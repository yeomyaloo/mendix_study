[Approving Requests](https://academy.mendix.com/link/modules/185/lectures/5076/Learning-Objectives)
# 학습 목표
이 모듈이 끝날 때까지, 다음을 할 수 있게 됩니다:
- 요청을 관리하고 승인하는 프로세스 구축하기
- 팝업 페이지 만들기
# 소개(Introduction)
## 1. 탭 방식의 개요 페이지
### 1.1 만드는 방법
개요 페이지를 작업해 봅시다:
1. Request 폴더에 새 페이지를 추가합니다.
   - 이름: Request_Overview_Approver
   - 네비게이션 레이아웃: Atlas_Custom
   - 템플릿: Tabs Fullwidth (Tabs 섹션에 있음)  
2. 헤더는 이미 네비게이션 레이아웃에 있으므로, 헤더 컨테이너와 포함된 행을 제거합니다. 또한 첫 번째 탭의 데이터 뷰도 제거합니다.
3. 세 개의 탭 이름을 다음과 같이 변경합니다: 
   - New requests
   - Approved requests
   - Rejected requests
4. 각 탭에 해당하는 요청을 보여주는 데이터 그리드(Data grid) 위젯을 추가합니다.
5. 각 데이터 그리드의 데이터 소스를 Expenses 모듈의 Request 엔티티로 설정합니다. 각 탭이 올바른 데이터베이스 제약 조건으로 구성되었는지 확인합니다:
   - 상태(Status) = New (탭 1)
   - 상태(Status) = Approved (탭 2)
   - 상태(Status) = Rejected (탭 3)
다음 이미지는 첫 번째 탭에 대해 제약 조건을 추가한 방법을 보여줍니다. 또한 데이터 그리드의 내용을 자동으로 채웁니다.
![image](https://github.com/user-attachments/assets/e8556dea-ce61-4ddc-8e48-3c2222abf19c)

6. 각 데이터 그리드 위젯의 상단에 최신 요청을 표시하도록 createdDate(내림차순)를 기준으로 정렬을 적용합니다. (이 작업을 수행하려면 구조 모드(Structure mode)로 전환하고 데이터 그리드에서 정렬 순서(Sort order)를 더블 클릭해야 합니다).
7. 각 데이터 그리드 위젯에서 Status 열을 삭제합니다. 이 정보는 여기서 관련이 없습니다.
8. 각 데이터 그리드 위젯에서 New, Edit, Delete 버튼을 제거합니다. 재무 직원들은 요청을 승인하거나 거절할 수만 있어야 합니다.

## 페이지를 네비게이션 메뉴에 추가하기
1. 네비게이션 설정을 열고 'Approve'라는 이름으로 요청 개요 페이지에 대한 새 네비게이션 항목을 추가합니다.
2. Approver에게 페이지에 대한 접근 권한을 부여합니다.

# 팝업 사용 방법(Working With Popups)
## 1. Working With Popups
### 1.1 요청 승인 및 거부 기능
- **목표**: 승인자는 요청의 세부 정보를 팝업 창에서 보고 승인 또는 거부할 수 있어야 합니다.
- **팝업 창의 하단**: 승인, 거부 또는 취소 버튼을 배치합니다.

### 1.2 팝업 크기 조정
- **기본 설정**: Mendix의 팝업 창은 기본적으로 크기 조정이 가능하며, 자동으로 크기가 결정됩니다.
- **고정 크기 설정**: 페이지의 속성에서 팝업 창에 고정된 너비와 높이를 설정하고, resizable 속성을 "no"로 설정하여 항상 지정된 크기로 유지합니다.

### 1.3 팝업 하단 고정
- **기본 레이아웃**: 기본적으로 Mendix의 팝업 창은 레이아웃 그리드를 가장 바깥 레이어로 사용하여 페이지 전체가 스크롤 가능하게 합니다. 이 경우, 하단의 버튼이 스크롤 영역에 포함되어 바로 보이지 않을 수 있습니다.
- **하단 버튼 고정**: 페이지가 길거나 고정 크기의 팝업 창이 있는 경우, 하단의 버튼을 항상 보이도록 설정할 수 있습니다. 이를 위해 외부 레이아웃 그리드를 제거하여 하단 버튼을 “sticky” 상태로 만들어 항상 보이게 합니다.

## 2. 팝업 창 구축
### 2.1 데이터 그리드에 액션 버튼 추가
- **페이지**: Request_Overview_Approver 페이지의 첫 번째 탭에서 새로운 요청을 보여주는 데이터 그리드
- **버튼 설정**:
  - **Caption**: Details
  - **Button style**: Primary
  - **Is default button**: Yes

### 2.2 클릭 이벤트 설정
- **On click 이벤트**: Request_Details_Approver 페이지를 표시하도록 설정
- **네비게이션 레이아웃**: PopupLayout
- **템플릿**: Form Vertical (Forms 섹션에서 선택)

### 2.3 팝업 페이지 설정
- **데이터 뷰 이동**: 데이터 뷰를 레이아웃 그리드에서 드래그한 후 레이아웃 그리드를 삭제하여 팝업 하단을 "sticky"로 만듭니다.
- **페이지 속성 설정**:
  - **Title**: Request Details
  - **Resizable**: No
  - **Width (픽셀 단위)**: 500
  - **Height (픽셀 단위)**: 800
- **Status 위젯 삭제**: 이 페이지에서는 항상 새로운 요청 상태이므로 Status 위젯을 삭제합니다.
- **데이터 뷰 속성 설정**: **Editable**을 No로 설정하여 Approver가 요청을 수정하지 못하게 합니다.

### 2.4 팝업 페이지 빌드
- **데이터 그리드 추가**: Location 위젯 아래에 **Data grid**를 배치하고, 데이터 소스를 **RequestLine_Request** > **RequestLine** 엔터티로 연결
   - ![image](https://github.com/user-attachments/assets/dc13ecf1-4f19-45c1-b9a3-0995488cab7d)
- **구조 모드 사용**: Cancel 버튼을 Approve 및 Reject 버튼과 같은 줄에 배치

### 2.5 승인/거부 버튼의 동작 설정
- **Approve 버튼**:
  - **Microflow**: ACT_Request_StatusApproved
  - **동작**:
    - 요청 상태를 Approved로 설정
    - 요청을 커밋하고 클라이언트 새로고침
    - 페이지 닫기
    - ![image](https://github.com/user-attachments/assets/f2289f29-8d16-4ea5-a913-e13e8bae3d71)
    - ![image](https://github.com/user-attachments/assets/d62e0ee8-3e90-4b86-8828-27aff0695cb1)

- **Reject 버튼**:
  - **Microflow**: ACT_Request_StatusRejected
  - ![image](https://github.com/user-attachments/assets/80cc57c4-4074-4356-a6df-f6db6efe7dc4)
  - **동작**:
    - 요청 상태를 Rejected로 설정
    - 요청을 커밋하고 클라이언트 새로고침
    - 페이지 닫기
      ![image](https://github.com/user-attachments/assets/35f174fb-f014-4beb-aacc-328d9d0712ce)
      ![image](https://github.com/user-attachments/assets/726d0e14-ff1b-4276-adfe-9d4fe9e85ed7)

### 2.6 권한 설정
- Approver에게 팝업 페이지와 두 Microflow에 대한 접근 권한을 부여합니다.
![image](https://github.com/user-attachments/assets/d0df86b3-b463-499d-8c4b-e739d0f0a803)

### 2.7 홈 페이지에 버튼 추가
- **버튼 추가 위치**: List view
- **버튼 설정**:
  - **Caption**: Approve/Reject
  - **Render mode**: Link
  - **권한**: Approver 모듈 역할만 버튼을 볼 수 있도록 설정
   ![image](https://github.com/user-attachments/assets/706feaf8-4af3-4cd7-a211-2895be5d0e22)

## 3. 기능 테스트
### 3.1 애플리케이션 배포
- 새 기능을 테스트하려면 애플리케이션을 배포하세요. (로컬에서 실행하는 것을 잊지 마세요!)

## 3.2 승인자 사용자로 로그인
- 로그인한 후 **demo_approver** 사용자로 전환하여 요청 개요 페이지로 이동합니다.

## 3.3 요청 승인 및 거부
- 몇 가지 요청을 승인하고 거부하여 어떻게 작동하는지 확인하세요!

## 3.4 주의사항
- 헤더 데이터에 있는 승인된 금액은 화면을 새로 고친 후에만 업데이트됩니다.

# 퀴즈
# 질문과 답변

## Question 1:
**How is the size of popup windows set to fixed?**

- By manually setting the size of page columns.
- By setting the resizable property of the page to No.
- By selecting Atlas_Fixed layout.
- Automatically.

- **Answer**: **By setting the resizable property of the page to No.**
- **Explanation**: To fix the size of the popup window, you need to set the **Resizable** property of the page to **No** and define a fixed width and height. The other options are unrelated to setting the popup size.

- **한글 번역**:
  - **답변**: **페이지의 resizable 속성을 No로 설정합니다.**
  - **설명**: 팝업 창의 크기를 고정하려면 페이지의 **Resizable** 속성을 **No**로 설정하고 고정된 너비와 높이를 지정해야 합니다. 나머지 선택지는 팝업 크기 설정과 관련이 없습니다.
![image](https://github.com/user-attachments/assets/c4fd1e29-85c6-42f0-a97e-8614c8cb0d61)

---

## Question 2:
**How can you ensure that the buttons in the footer area of the relatively long and scrollable pop-up page are always visible?**

- By setting the floating property of the footer to No.
- By removing a scroll container.
- By fixing the size of the scroll container.
- By removing the outer layout grid.

- **Answer**: **By removing the outer layout grid.**
- **Explanation**: Removing the outer layout grid ensures that the footer buttons are "sticky" and remain visible even when scrolling. Other options do not relate to this feature in Mendix.

- **한글 번역**:
  - **답변**: **외부 레이아웃 그리드를 제거합니다.**
  - **설명**: 외부 레이아웃 그리드를 제거하면 하단의 버튼이 "sticky" 상태가 되어 스크롤 시에도 항상 보입니다. 다른 선택지는 Mendix에서 팝업 하단을 고정하는 기능과 관련이 없습니다.

---

## Question 3:
**What constraint can you use to show the most recently created items at the top of the page?**

- createdDescend (date created)
- dateCreated (descending)
- createdDate (descending)
- createdAscend (descending)

- **Answer**: **createdDate (descending)**
- **Explanation**: `createdDate (descending)` sorts requests by creation date, ensuring the most recent items appear at the top of the page. The other options are either incorrect or contain syntax errors.

- **한글 번역**:
  - **답변**: **createdDate (내림차순)**
  - **설명**: `createdDate (내림차순)`은 요청이 생성된 날짜를 기준으로 정렬하여 가장 최근 항목이 페이지 상단에 나타나도록 합니다. 다른 선택지는 잘못되었거나 구문 오류가 있습니다.
---

## Question 4:
**What are the default Mendix options for the popups?**

- Resizable with size determined automatically, with layout grid as the most outer layer of the page.
- Resizable with size determined automatically, with layout grid as the most inner layer of the page.
- Fixed size determined automatically, with layout grid as the most inner layer of the page.
- Fixed size determined automatically, with layout grid as the most outer layer of the page.

- **Answer**: **Resizable with size determined automatically, with layout grid as the most outer layer of the page.**
- **Explanation**: By default, Mendix popups are resizable, with their size determined automatically, and a layout grid is used as the outermost layer. Other answers either incorrectly describe the grid position or the size behavior.

- **한글 번역**:
  - **답변**: **크기 조정 가능하며 크기는 자동으로 결정되고, 레이아웃 그리드가 페이지의 가장 바깥 레이어로 설정됩니다.**
  - **설명**: 기본적으로 Mendix 팝업 창은 크기 조정이 가능하며, 크기는 자동으로 결정됩니다. 레이아웃 그리드는 가장 바깥 레이어로 설정됩니다. 다른 답변은 그리드 위치 또는 크기 동작을 잘못 설명하고 있습니다.

---

## Question 5:
**How to make the popup window always visible?**

- Choose a different popup style.
- Change the layer grid.
- Remove the outer layer grid.
- Add a button to “glue” them.

- **Answer**: **Remove the outer layer grid.**
- **Explanation**: By removing the outer layout grid, the footer becomes sticky, ensuring that the popup's important buttons are always visible. The other answers either don't apply to this situation or involve incorrect steps.

- **한글 번역**:
  - **답변**: **외부 레이아웃 그리드를 제거합니다.**
  - **설명**: 외부 레이아웃 그리드를 제거하면 팝업 창의 하단 버튼이 "sticky" 상태가 되어 항상 보입니다. 다른 답변은 이 상황에 맞지 않거나 잘못된 절차를 포함하고 있습니다.

