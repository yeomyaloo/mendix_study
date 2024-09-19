# Learning Objectives - 학습 목표
1. 앱 생성
   - 새로운 앱을 생성할 수 있습니다.
2. 앱에 피드백 위젯 추가 
   - 앱에 피드백 위젯을 추가할 수 있습니다.
3. 앱의 보안 설정
   - 앱의 보안을 설정할 수 있습니다.
4. 앱에서 엔터티 및 속성 생성
   - 앱에서 엔터티와 속성을 생성할 수 있습니다.
5. Generate Overview Pages 기능을 사용하여 Overview 및 NewEdit 페이지 쉽게 생성 
   - Generate Overview Pages 기능을 사용하여 Overview 및 NewEdit 페이지를 쉽게 생성할 수 있습니다.
6. 특정 엔터티에 대해 애플리케이션에 하나의 인스턴스만 존재하도록 보장하는 마이크로플로우 빌드
   - 특정 엔터티에 대해 애플리케이션에 하나의 인스턴스만 존재하도록 하는 마이크로플로우를 빌드할 수 있습니다.

# 실제 프로젝트 세팅
## 1. 프로젝트 생성
### 1.1 방법
1. Mendix 포털을 열어 시작합니다.

2. 오른쪽 상단에서 Create App 버튼을 보게 되며, 클릭합니다.

3. 시작 지점으로 Blank Web App을 선택합니다.

4. Advanced Settings로 이동하여 Template Version Studio Pro 10.0.0 (Template v10.0.9976)을 선택한 후, Select This Template을 클릭합니다.

5. 앱 이름을 “Event Management”로 정하고, 프로젝트 아이콘을 선택한 후 Create App을 클릭합니다.

6. 이제 프로젝트를 생성하였으며, 다음 강의에서 Studio Pro에서 앱을 열게 됩니다.

## 2. Open and Edit Your Project - 프로젝트 열기 및 편집하기
- Mendix 포털을 통해 프로젝트를 여는 방법을 알고 있지만, Mendix Marketplace에서 모든 Studio Pro 버전을 찾을 수 있다는 것도 기억하시나요?
- Mendix Marketplace에서 Mendix Studio Pro 버전 10.0.0을 다운로드하세요.

**참고:** 현재 Windows 운영 체제용 설치 프로그램만 제공합니다. Mac을 사용하는 경우 Windows 가상 머신을 사용해 주세요.


## 3. # Adding a Feedback Widget - 피드백 위젯 추가하기
### 3.1 피드백 추가와 스니펫 이용
- 사용자 피드백은 앱 개발 시 중요합니다.
- 이는 앱을 지속적으로 개선하여 사용자 요구에 더 잘 맞출 수 있게 합니다.
- 애플리케이션 사용자에게 피드백을 제공할 수 있는 가능성을 주는 것은 좋은 실천입니다.
- Mendix는 쉽게 구현할 수 있는 위젯을 개발했습니다. 이 위젯은 사용자 역할, 페이지 이름, 화면 해상도와 같은 정보를 자동으로 제공하기 때문에 매우 유용합니다.
- 재사용 가능하도록, 스니펫을 사용할 것입니다. 스니펫은 페이지와 레이아웃에서 사용할 수 있는 재사용 가능한 인터페이스 부분입니다.
- 스니펫에 대한 변경 사항은 이 스니펫이 사용된 모든 장소에 적용됩니다.
- 스니펫의 사용은 "Don't Repeat Yourself (DRY)" 원칙을 기반으로 하며, 이는 인터페이스의 수정할 장소를 줄이고 매끄러운 전환과 사용자 친화적인 경험을 제공합니다.

### 3.2 피드백 위젯 추가하는 방법
1. App Explorer에서 FeedbackWidget 스니펫을 찾을 수 있습니다. 이 스니펫은 자동으로 프로젝트에 추가되었습니다. 도구 상자에서 데이터 뷰, 데이터 그리드 등과 같은 위젯처럼 이 스니펫을 페이지에 추가할 수 있습니다. 이 스니펫은 이미 Atlas_Default 및 Atlas_TopBar 레이아웃의 일부이며, 앱에서는 Atlas_Default 레이아웃을 사용할 것입니다.
2. Feedback Widget의 Advanced 탭으로 가면 App ID가 이미 설정되어 있어야 합니다. 설정되어 있지 않다면, Mendix Portal로 가서 프로젝트의 General Settings를 열어 이 ID를 쉽게 찾을 수 있습니다.
3. Feedback 위젯 속성 창의 Project 탭에서 Allow screenshots 속성이 Yes로 설정되어 있는지 확인합니다. 이 설정을 통해 피드백 항목에 대한 모든 가능한 정보를 얻을 수 있습니다.
4. Authentication 탭에서 Authentication method로 Custom authentication을 선택합니다. 그런 다음 아래 스크린샷에 표시된 대로 User Object (1), User name attribute (2), Email attribute (3)를 입력합니다. 이 속성을 구성하면 피드백을 추가하는 로그인된 사용자에게 자동으로 이 정보가 채워집니다.

## 4. Creating the User Roles - 사용자 역할 만들기
### 4.1 시나리오
- 어느 시점에서 이 앱을 라이센스가 있는 환경에 배포할 계획이 있다고 가정해 보겠습니다. 이 경우, 프로젝트 시작 시 앱 보안 수준을 Production으로 설정하는 것이 좋습니다.
-  이렇게 하면 Mendix Studio Pro가 개발 중에 보안 문제를 지적하는 데 도움이 됩니다. 이 권장 사항을 무시하면 나중에 수백 개의 오류를 수정해야 할 수 있습니다.
-  이는 빌드된 모델이 아직 프로덕션 보안에 맞게 구성되지 않았기 때문입니다.
-  Mendix Studio Pro가 가능한 보안 문제를 찾도록 하려면 Check security 옵션을 Yes로 설정하는 것이 중요합니다.

**참고:** Mendix 앱은 App Security 수준이 ‘Production’으로 설정되어 있어야만 라이센스가 있는 환경에서 실행될 수 있습니다. 이 보안 수준이 올바르게 설정되지 않으면 앱이 비로컬 환경에 배포되지 않습니다.

### 4.2 사용자 역할 만들기
1. App Security로 이동하여 보안 수준을 ‘Off’에서 ‘Production’으로 변경합니다.
2. User roles 탭으로 이동하여 ‘EventManager’라는 새로운 사용자 역할을 생성하고 MyFirstModule 모듈에 해당하는 모듈 역할을 생성합니다.
3. OK를 클릭하여 앱 보안을 닫습니다.

### 4.3 보안 설정하기
#### 1단계
- 다시 App Security로 돌아가서 User roles 탭으로 가서 Administration 모듈의 모듈 역할 ‘User’를 사용자 역할 EventManager에 추가합니다.

#### 2단계
- 지금까지는 잘 보이지만, App Security가 아직 완료되지 않았으므로 다시 열어보겠습니다. 이번에는 사용자 역할 ‘User’를 ‘Visitor’로 변경할 것입니다.이 사용자 역할은 이후 학습 경로에서 사용되며 축제에 등록한 사람을 나타냅니다.
- OK를 클릭하여 App Security를 닫고 MyFirstModule 모듈의 Module Security를 엽니다. 여기에서 방금 생성한 모듈 역할 (EventManager)과 User를 볼 수 있어야 합니다. User 모듈 역할을 제거합니다. 사용 중이라는 경고가 표시되지만 문제는 없습니다. 팝업에서 Delete를 클릭합니다.
- 이제 이 모듈에 새로운 모듈 역할을 추가하고 이를 Visitor라고 명명한 후, OK를 클릭하여 모듈 보안을 닫습니다.
- 다시 App Security로 돌아가서 새로운 모듈 역할 Visitor를 사용자 역할 Visitor와 연결한 후, OK를 클릭하여 App Security를 닫습니다.
- 이제 오류 도크에서 하나의 오류가 나타납니다: 선택된 모듈 역할 ‘MyFirstModule.User’가 더 이상 존재하지 않습니다. 이를 해결하려면 ‘Home_Web’ 페이지를 열고 속성에서 ‘Visible for’ 모듈 역할을 변경해야 합니다.
- 먼저 기존 모듈 역할 중 아무것도 선택하지 않고 어떤 일이 발생하는지 봅시다. 결국 홈페이지는 기본 홈페이지로 호출되므로 모듈 역할을 설정할 필요가 없습니다.
- 이제 다른 오류가 나타납니다: 페이지가 탐색 또는 버튼에서 사용되는 경우 허용된 역할 중 하나는 선택해야 한다는 오류입니다. 이는 앱 탐색에 ‘Home_Web’ 페이지를 참조하는 탐색 항목이 있기 때문입니다. 모듈 역할이 연결되어 있지 않으면 아무도 페이지에 접근할 수 없으므로 이 오류는 이해할 수 있습니다.

#### 3단계
- MyFirstModule 모듈의 Module Security를 열어 Page access 탭을 선택하고 두 모듈 역할을 선택합니다. OK를 클릭하여 저장합니다.
- 이제 앱 탐색을 확인하여 EventManager와 Visitor가 ‘Home_Web’ 페이지를 볼 수 있는지 확인합니다.
