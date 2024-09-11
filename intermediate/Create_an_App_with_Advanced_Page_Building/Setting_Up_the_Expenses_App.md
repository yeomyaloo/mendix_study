
# 앱 탐색기 구조화
## 1. 의의
- 앱의 기초를 만들 때, 앱 탐색기(App Explorer)를 구조화하는 것이 중요합니다.
- 페이지, 마이크로플로우와 같은 문서를 추가하기 시작하면, 문서를 조직적으로 관리하는 데 약간의 노력을 기울이는 것이 중요합니다.
- 그렇지 않으면, 애플리케이션의 앱 탐색기가 혼잡해져 앱을 빠르게 구축하기 어려워질 수 있습니다.
## 2. 필요성
- 문서의 구조는 폴더를 명확하게 구분하는 것부터 시작합니다.
- 좋은 폴더 구조를 사용하면 애플리케이션의 유지보수성을 향상시킬 수 있습니다.
- 필요한 문서를 더 빠르게 찾을 수 있으며, 따라서 개발과 수정 작업도 더 신속하게 진행할 수 있습니다.
- 문서는 일반적으로 프로세스 관련 소스와 엔티티 관련 소스로 폴더에 그룹화할 수 있습니다.

## 3. 프로세스 관련 소스
모든 앱은 프로세스로 구성됩니다. 이러한 프로세스를 반영한 폴더에 문서를 구조화합니다. 각 개별 프로세스와 그 단계에 따라 폴더를 만들어 문서를 정리합니다.

## 4. 엔티티 관련 소스
- 모든 앱에는 특정 엔티티에 필요한 문서가 있습니다.
  - 예를 들어, 유지보수용 개요 페이지,
  - 커밋을 방지하는 유효성 검사 마이크로플로우,
  - 또는 기타 이벤트 트리거와 같은 문서가 있습니다. 
- 이러한 문서는 엔티티 이름을 따서 명명된 폴더에 구조화합니다.

## 5. 앱 생성 및 구조화
### 5.1 생성 방법
#### 5.1.1 새로운 빈 웹 앱 생성
- 빈 웹 앱을 새로 생성합니다.
- 고급 설정에서 템플릿 버전으로 Studio Pro 10.3.0을 선택합니다.
- 앱이 빌드되면 Studio Pro에서 편집을 클릭하여 앱 구축을 시작합니다.

#### 5.1.2 기존 모듈 이름 변경
- 기존의 MyFirstModule 모듈 이름을 Expenses로 변경합니다. 모듈 이름이 기능을 설명하도록 합니다.

#### 5.1.3 폴더 추가:
- Expenses 모듈을 우클릭하고 폴더 추가를 클릭합니다.
- 폴더 이름을 TeamMember로 지정하여 팀원 관리와 관련된 문서를 저장합니다.
- 또 다른 폴더를 추가하고 이름을 Resources로 지정합니다.
- Pages라는 폴더도 추가합니다.

#### 5.1.4 앱 구조 유지
- 학습 경로를 진행하면서, Expenses 모듈에 폴더와 하위 폴더를 추가하여 앱 구조를 계속해서 유지합니다.

# 도메인 모델 (The Domain Model)
## 1. 필요성
- 잘 구조화된 App Explorer만큼이나, 잘 구조화된 도메인 모델을 갖는 것이 중요합니다.
- 애플리케이션의 데이터 요구 사항을 고려하여 엔티티와 연관 관계를 도메인 모델 내에서 적절히 구성해야 합니다.
- 도메인 모델에서 일반화를 활용하는 것도 중요합니다.
- 이러한 내용은 고급 도메인 모델 기술 학습 경로에서 더 자세히 다룰 수 있습니다.
- 도메인 모델에는 속성, 연관 관계, 이벤트 및 기타 속성이 포함됩니다.

## 2. 애플리케이션을 위한 도메인 모델 구성
### 2.1 Administration 및 System 모듈 활용
- 모든 Mendix 애플리케이션에는 Administration 및 System 모듈이 포함되어 있습니다.
- 이 모듈들을 활용하여 애플리케이션에 특화된 두 개의 엔티티를 생성할 것입니다.
### 2.2 Account 엔티티 상속
- 사용자는 Account 엔티티와 같은 속성(예: 전체 이름, 이메일 주소, 사용자 이름)을 가지게 됩니다.
### 2.3 Image 엔티티 상속
- 사용자 계정에 프로필 사진을 연결할 수 있습니다.
- 특화된 엔티티 사용 이유
### 2.4 Administration 모듈의 변경 불가
- Administration 모듈은 Marketplace 모듈로, 모듈 자체를 변경하는 것은 모범 사례가 아닙니다. retrieve를 누르고 해당 속성에서 아래와 같이 설정해주면 리스트로 바뀌는 것을 볼수 있다.
- ![image](https://github.com/user-attachments/assets/8d15bcfe-a57d-4bf9-9281-a68797a6f0f6)

### 2.5 System 모듈의 접근 권한 변경 불가
- System 모듈의 접근 권한은 변경할 수 없지만, 특화된 엔티티는 접근 권한을 변경할 수 있습니다.

## 3. Creating Entities and Attributes
![image](https://github.com/user-attachments/assets/7927cb48-eea1-4a74-b2f2-3d7762f5ef38)
- 해당 문양이 없더라도 오브젝트로 List로 넘어갈 값을 주면 해당 문양이 제시된 예시 이미지와 같아진다.

# 보안(App Security)
## 1. 사용자 역할
### 1.1 앱에서 사용할 수 있는 사용자 역할 만들기
1. Administrator: 사용자 관리 업무를 처리하는 사용자.
2. Requestor: 요청을 입력하고 자신의 요청만 볼 수 있는 사용자.
3. Approver: 요청을 승인하거나 거부할 수 있으며 시스템의 모든 요청을 볼 수 있는 사용자.

### 1.2 역할 설정 방법
1. `App Security -> Security Level -> production` 선택
  - ![image](https://github.com/user-attachments/assets/95dd1a97-ecb9-40c2-b148-53c4f5e1d5a9)
3. 모듈 및 사용자 역할을 적절히 구성한다.
  - 모듈 역할의 경우에는 필요한 곳에만 설정한다.
  - 참고: Marketplace 모듈의 경우엔 모듈 역할을 추가하지 않는 것을 권장한다. 언제든 변경될 수 있기 때문에 변경 후에 추가한 모든 모듈 역할이 사라질 수 있어 모듈 역할 추가를 권하지 않는다.
  - ![image](https://github.com/user-attachments/assets/a8e859e4-8be8-4ec8-ab39-b60e490abaa2)
3. 각 사용자 역할에 데모 사용자를 추가해야 한다.
  - 이 경우라면 Administrtaion.Account 엔티티를 사용한다. 
## 2. 앤티티 접근(Entity Access)
- TeamMember에 관한 Administation 권한 부여
  - ![image](https://github.com/user-attachments/assets/a8fae772-2104-4a52-9b8e-1c5ce34d0c7a)
- ProfilePicture 엔티티에 접근 권한 설정
  - ![image](https://github.com/user-attachments/assets/3cf18dba-ad97-4152-9d6e-a884737ca27b)

# Team Member 관리 페이지 생성(Team Member Management Pages)
## 1. 시나리오
- 이제 Domain Model과 보안 설정이 완료되었으므로, Andrea가 자신의 팀을 관리할 수 있도록 페이지를 구축해야 합니다.
-  Andrea는 특히 팀 구성원 전체를 볼 수 있는 개요 페이지와, 새로운 팀원을 생성하거나 기존 팀원을 편집할 수 있는 상세 페이지를 원합니다.
## 2. 페이지 명명규칙
페이지는 다음과 같이 이름을 지정합니다
### 2.1 Entity_PageType
- 특정 사용자 역할에 대한 페이지는 `Entity_PageType_UserRole`
### 2.2 페이지 생성 단계
#### TeamMember_Overview Page:
- 이름: TeamMember_Overview
- 페이지 유형: 데이터 그리드(Data Grid)로 모든 팀 구성원의 목록을 표시.
#### TeamMember Detail Page:
- 이름: TeamMember_Detail
- 페이지 유형: 데이터 뷰(Data View)로 개별 팀원의 세부 정보를 표시하고, 새 팀원을 추가하거나 기존 팀원을 편집할 수 있도록 구성.

## 1. 개요 페이지 만들기(Create the Overview Page)
다음은 Andrea가 원하고 있는 팀 구성원 개요 페이지 디자인입니다. 커스텀 색상 테마와 로고는 Mendix에서 가능한 커스터마이징 예시일 뿐이므로 신경 쓰지 않아도 됩니다.

```plaintext
참고: 이 학습 경로의 대부분의 연습은 디자인 모드에서 진행됩니다. 작업 환경이 기본적으로 디자인 모드에서 열리도록 설정하고 싶다면, Edit > Preferences > Work environment > Default Page Editor > Design mode에서 기본 페이지 편집기를 변경할 수 있습니다.
```
## 2. 페이지 생성 단계
### 2.1 새 페이지 추가
- 페이지 이름: TeamMember_Overview_Administrator
- 내비게이션 레이아웃: Atlas_Topbar
- 페이지 템플릿: Lists > List Columns

### 2.2 헤더 수정
- <Back 링크 버튼과 액션 버튼 하나 삭제.
- 남은 액션 버튼의 캡션을 New Team Member로 변경 (나중에 기능 추가 예정).
- 페이지 제목을 Team Member Management로 변경하고, 서포팅 텍스트 삭제.

### 2.3 리스트 뷰에 TeamMember 엔티티 연결
- Studio Pro가 자동으로 리스트 뷰의 콘텐츠를 채우지 않도록 설정.
  - 자동 채우기를 허용하면 페이지 템플릿의 디자인이 변경될 수 있습니다.

### 2.4 리스트 뷰 정렬 순서 추가:
- Sort order 더블 클릭 → 정렬 순서 추가.
  - ![image](https://github.com/user-attachments/assets/0bdfb2e0-ef58-482a-8d2a-6d3715808e8b)
- FullName 속성 선택 → Select 및 OK 클릭.

### 2.5 리스트 뷰 검색 필드 추가:
- Search on 더블 클릭 → 검색 필드 추가.
- FullName 속성 선택 → Select 및 OK 클릭.

### 2.6 내비게이션 추가
- App 모듈의 내비게이션으로 이동 → New item 추가, 캡션은 Team Members로 설정하여 새로 만든 팀 구성원 개요 페이지 연결.
  - ![image](https://github.com/user-attachments/assets/c7d9e224-4553-4c66-ac59-939d97ccb1a6)

### 2.7 Administrator 권한 부여
- 이 페이지에 Administrator 역할만 접근할 수 있도록 설정.
  - ![image](https://github.com/user-attachments/assets/fac5ef73-b750-4b71-803c-a179f2adc240)
  - ![image](https://github.com/user-attachments/assets/80340b72-a092-4ca1-8886-158f225dcfd0)

## 3. 리스트 뷰 항목 구축(Build the List View Item)
### 3.1 시나리오
이제 리스트 뷰 항목에 동적 데이터를 추가할 시간입니다! Andrea는 각 팀원의 가장 관련된 정보(이름, 이메일 주소, 앱에서의 역할)를 보고 싶어합니다. 또한 빠르게 성장하는 회사에서 모든 사람의 이름을 기억하기 어려우므로 프로필 사진도 함께 보고 싶어합니다.

현재 리스트 뷰 항목에는 정적인 이미지가 있습니다. 각 팀원의 동적 이미지(프로필 사진)를 표시하려면, 이 정적 이미지를 동적 이미지로 교체해야 합니다.

### 3.2 단계별 작업
1. Toolbox의 Widgets 탭에서 Dynamic Image 위젯을 검색합니다.
2. 리스트 뷰 항목에 있는 정적 이미지 왼쪽에 Dynamic Image를 배치합니다.
3. 기존 정적 이미지를 삭제합니다.
4. Dynamic Image를 더블 클릭하여 속성 창을 엽니다. 다음 이미지를 사용하여 속성을 구성합니다.
  - 구성 후 OK 클릭. Dynamic Image의 내용이 자동으로 채워지지 않도록 설정합니다.
5. 리스트 뷰 항목 나머지 구성
- 가운데 열의 텍스트 위젯 아래에 컨테이너를 추가한 후, 그 안에 두 개의 버튼을 추가합니다.
- Edit 버튼의 클래스명은 btn-block, Delete 버튼의 클래스명은 spacing-outer-left-large로 설정합니다.
- 컨테이너에는 클래스명 spacing-outer-bottom-large를 설정하고, Align content는 Left align as row로 설정합니다.
- 세 번째 열에 있는 Chevron 링크 버튼은 삭제합니다.
- Delete 버튼의 On click 이벤트는 Delete로 설정합니다.

## 4. 디테일 페이지 생성 및 설정
### 4.1 시나리오
이제 Andrea에게 앱 내 팀원들을 생성하고 편집할 수 있는 디테일 페이지가 필요합니다. 이 페이지에서는 새 팀원을 생성하고, 생성된 후에는 수정 기능을 제공하게 됩니다. 새 페이지에서는 비밀번호를 바로 입력할 수 있고, 수정 페이지에서는 '비밀번호 변경' 버튼을 통해 비밀번호를 변경할 수 있게 설계됩니다.

### 4.2 새 페이지 생성
- 페이지 이름: TeamMember_New_Administrator
- 레이아웃: Atlas_Topbar
- 페이지 템플릿: Blank
### 4.3 헤더 추가
- 페이지 상단에 Pageheader 빌딩 블록을 사용하여 헤더를 추가합니다.
- 제목을 New Team Member로 변경하고, 부제목은 삭제합니다.
  - ![image](https://github.com/user-attachments/assets/0367f5b6-94df-4ac0-b106-04049440443b)

### 4.4 데이터 뷰 설정
- 레이아웃 그리드에 Data view 위젯을 추가하고, Data Source를 Marketplace modules Administration.AccountPasswordData로 설정합니다.
  - 이때 내용 자동 채우기는 "No"를 선택합니다.
  - ![image](https://github.com/user-attachments/assets/775ca621-5246-4b33-8b90-fba3bb7605ff)
  - 이떄 Marketplace modules Administration.AccountPasswordData가 없다면? ![image](https://github.com/user-attachments/assets/49e849fc-5785-46e1-87bb-3ac21817b2b5)
- Data view 위젯 내에 또 다른 Data view 위젯을 추가하고, Data Source는 TeamMember 엔티티로 설정하되, AccountPasswordData_Account 연관성을 사용하여 설정합니다. 이때 내용 자동 채우기는 "Yes"로 설정합니다.
    - AccountPasswordData_Account association 설정 ![image](https://github.com/user-attachments/assets/983f56a2-d5a9-4052-ac36-3866187c7e7f)
- Page Explorer를 사용하여 layout grid를 추가하고, 모든 속성을 이 그리드로 이동합니다. 그런 다음 layoutGrid2의 오른쪽에 열을 추가합니다. 각 열은 classname을 col-xs-12로 설정합니다.
- 이름 속성의 캡션을 Username으로 변경합니다.
- User role Input reference set selector는 Administration 모듈 내 User Management > Admin 폴더에서 기존 UserRole_Select 페이지를 사용합니다.
- Blocked 및 Active 라디오 버튼 속성은 Switch 위젯으로 대체하고, 필요 없는 속성은 삭제합니다.

### 4.5 프로필 이미지 섹션 추가
1. Page Explorer를 사용하여 Profile Picture 엔티티에 대한 Data view 위젯을 추가합니다. 연관성은 TeamMember_ProfilePicture입니다. 이때 내용 자동 채우기는 "Yes"로 설정합니다.
    - ![image](https://github.com/user-attachments/assets/44d5ce7e-7cb9-4bd4-be85-b93f4b288726)
2. Name 및 Size 속성 텍스트 상자는 삭제합니다.
3. Dynamic Image 위젯 설정
    - 기본 이미지: Atlas_Web_Content.Content.user
    - Data Source Entity: ProfilePicture under Expenses
4. Container 위젯을 추가하고 Profile Image 레이블을 추가합니다. 그 아래에 Dynamic Image 및 Upload image 위젯을 이동합니다.
5. 각 요소의 속성 설정
    - Container2: 클래스는 form-group
        - ![image](https://github.com/user-attachments/assets/e5526498-73b2-4cb1-b1f7-a68f021f0cb8)
    - Profile Image 레이블: 왼쪽 간격은 Inner large, 클래스는 control-label
    - Dynamic Image: 너비와 높이 비율은 70%, 아래쪽 간격은 Outer large, 스타일은 Circle, 중앙 정렬은 "Yes"로 설정합니다.
### 4.6 비밀번호 섹션 추가
1. 기존 layoutGrid2 아래에 2열 레이아웃 그리드를 추가합니다.
2. Text Box Input 위젯 두 개를 추가하고 NewPassword 및 ConfirmPassword 속성에 연결합니다.
### 4.7 저장 및 취소 버튼 추가
1. Data View footer에 Save 및 Cancel 버튼을 추가합니다.
2. Save 버튼은 Administration 모듈의 기존 SaveNewAccount 마이크로플로우를 트리거합니다.
3. Cancel 버튼은 변경 사항을 취소합니다.


## 5. 새 팀 구성원 버튼 구성 – 세부 페이지 구축
### 5.1 시나리오
Andrea가 새로운 팀 구성원을 생성할 수 있도록, New Team Member 버튼을 기능적으로 만드는 것이 필요합니다. 이를 통해 Andrea가 팀 구성원을 생성할 수 있도록 설정을 진행합니다.

### 5.2 설정 방법
1. TeamMember_Overview_Administrator 페이지에서 New Team Member 버튼의 클릭 액션을 설정합니다.
    - 클릭 시 수행할 작업을 microflow 호출로 설정합니다.
2. 새로운 microflow를 생성하고 이름을 ACT_TeamMember_Create로 지정합니다.
3. microflow 안에서 다음 단계를 추가합니다
    1. 새로운 ProfilePicture 객체를 생성합니다.
    2. 새로운 TeamMember 객체를 생성하고 이를 ProfilePicture 객체에 연결합니다.
    3. 새로운 AccountPasswordData 객체를 생성하고 이를 TeamMember 객체에 연결합니다.
    4. TeamMember_New_Administrator 페이지를 열고 AccountPasswordData 객체를 전달합니다.
   ![image](https://github.com/user-attachments/assets/5c24db52-9e5d-470d-b15a-0b39da7cf355)
4. Administrator 역할에 해당 microflow에 대한 접근 권한을 부여합니다.

## 6. 세부 페이지 구축 – 편집 페이지 생성(Build the Detail Pages – Create the Edit Page)
### 6.1 시나리오
Andrea가 팀 구성원 정보를 편집할 수 있는 페이지는 새로운 팀 구성원을 생성하는 페이지와 거의 동일합니다. 이제 새 페이지를 복제하고 필요한 부분을 변경해보겠습니다.

### 6.2 단계별 작업
1. TeamMember_New_Administrator 페이지를 복제하고 이름을 TeamMember_Edit_Administrator로 변경합니다.
2. 다음 이미지에 따라 페이지를 필요한 부분만 수정합니다
    - Expenses 모듈에 있는 TeamMember 엔티티로 페이지 파라미터를 설정합니다.
    - AccountPasswordData 페이지 파라미터를 삭제합니다.
    - Active Switch 위젯 아래에 Change Password 버튼을 추가하고 캡션을 "Change Password"로 설정합니다. 이 버튼은 Administration 모듈의 User Management > Admin 아래에 있는 ShowPasswordForm 마이크로플로우를 호출합니다.
    - Page Explorer를 사용하여 TeamMember 객체를 보여주는 내부 데이터 뷰를 AccountPasswordData 데이터 뷰 외부로 이동합니다.
    - 데이터 뷰의 페이지 파라미터를 TeamMember로 구성합니다.
    - AccountPasswordData 데이터 뷰와 하단의 텍스트 입력 위젯 두 개가 있는 레이아웃 그리드를 삭제합니다.
    - TeamMember 데이터 뷰의 하단에 Save 및 Cancel 버튼을 재생성합니다. 남은 데이터 뷰에서 푸터가 보이도록 설정해야 할 수 있습니다.
    - Save 버튼은 기본 저장 작업을 수행합니다.
      ![image](https://github.com/user-attachments/assets/1ecc0d51-ef37-45da-8236-f23c8b3fb16c)
3. 팀 구성원 개요 페이지의 Edit 버튼을 이 페이지에 연결합니다.
4. Administrator에게 페이지 접근 권한을 부여합니다.

# 퀴즈 
## Question 1
What is the correct way of structuring resources within the App Explorer?

Your answer: Manually

번역: 앱 탐색기 내에서 리소스를 구성하는 올바른 방법은 무엇인가요?

답변: 수동으로

해설: 앱 탐색기에서 리소스를 구성하는 방법은 수동으로 폴더와 서브폴더를 추가하고 각 기능이나 엔티티와 관련된 문서들을 적절히 배치하는 것입니다. 올바르게 폴더를 구조화하면 유지보수 및 개발 속도를 높일 수 있습니다.

## Question 2
When structuring the App Explorer, which of the following subfolders would be the best choice to store things like Enumerations and Regular Expressions?

Your answer: Resources

번역: 앱 탐색기를 구조화할 때, Enumerations(열거형)과 Regular Expressions(정규 표현식)과 같은 항목을 저장하는 데 가장 적합한 서브폴더는 무엇인가요?

답변: Resources

해설: 열거형, 정규 표현식과 같은 공통적인 리소스는 Resources 폴더에 저장하는 것이 좋습니다. 이는 이러한 리소스가 특정 프로세스나 엔티티에 속하지 않으며, 여러 곳에서 사용되기 때문에 적절하게 분류해두면 찾기 쉽습니다.

## Question 3
How can you connect a profile picture to the account of a team member in a way that allows the picture to be altered?

Your answer: Create a ProfilePicture entity and configure the Image entity in the System module as its generalization.

번역: 프로필 사진을 팀 구성원의 계정에 연결하고, 이 사진이 변경 가능하도록 하려면 어떻게 해야 하나요?

답변: ProfilePicture 엔티티를 생성하고 System 모듈의 Image 엔티티를 그 일반화로 설정합니다.

해설: 사진을 변경 가능하게 만들기 위해서는 ProfilePicture라는 새로운 엔티티를 만들고, 이를 System 모듈의 Image 엔티티에서 상속받도록 구성합니다. 이렇게 하면 사용자는 프로필 사진을 쉽게 변경할 수 있습니다.

## Question 4
Which widget needs to be used inside of a List View for visualizing a dynamic image?

Your answer: Dynamic Image

번역: 동적 이미지를 시각화하기 위해 List View 내에서 어떤 위젯을 사용해야 하나요?

답변: Dynamic Image 위젯

해설: 동적 이미지를 표시하려면 Dynamic Image 위젯을 사용해야 합니다. 이 위젯은 데이터베이스의 이미지 데이터를 연결하여 각 사용자나 항목에 대해 다른 이미지를 표시할 수 있도록 합니다.
