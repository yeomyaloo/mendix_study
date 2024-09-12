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
6. 각 데이터 그리드 위젯의 상단에 최신 요청을 표시하도록 createdDate(내림차순)를 기준으로 정렬을 적용합니다. (이 작업을 수행하려면 구조 모드(Structure mode)로 전환하고 데이터 그리드에서 정렬 순서(Sort order)를 더블 클릭해야 합니다).
7. 각 데이터 그리드 위젯에서 Status 열을 삭제합니다. 이 정보는 여기서 관련이 없습니다.
8. 각 데이터 그리드 위젯에서 New, Edit, Delete 버튼을 제거합니다. 재무 직원들은 요청을 승인하거나 거절할 수만 있어야 합니다.

## 페이지를 네비게이션 메뉴에 추가하기

1. 네비게이션 설정을 열고 'Approve'라는 이름으로 요청 개요 페이지에 대한 새 네비게이션 항목을 추가합니다.
2. Approver에게 페이지에 대한 접근 권한을 부여합니다.

