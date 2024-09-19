![image](https://github.com/user-attachments/assets/5db0cf55-5c6f-41ff-9981-2ece5fb63a16)# Learning Objectives - 학습 목표
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
1. [Mendix 포털을 열어 시작합니다.](https://sprintr.home.mendix.com/)

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
1. App Explorer에서 FeedbackWidget 스니펫을 찾을 수 있습니다. 이 스니펫은 자동으로 프로젝트에 추가되었습니다. 도구 상자에서 데이터 뷰, 데이터 그리드 등과 같은 위젯처럼 이 스니펫을 페이지에 추가할 수 있습니다. 이 스니펫은 이미 Atlas_Default 및 Atlas_TopBar 레이아웃의 일부이며, 앱에서는 Atlas_Default 레이아웃을 사용할 것입니다.</br>
![image](https://github.com/user-attachments/assets/35b0978b-e3b1-4a14-ac29-cacfb3f824dd)
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
![image](https://github.com/user-attachments/assets/64dfefb3-d8a0-48ae-b3c9-848af6370b59)

### 4.3 보안 설정하기
#### 4.3.1 1단계
- 다시 App Security로 돌아가서 User roles 탭으로 가서 Administration 모듈의 모듈 역할 ‘User’를 사용자 역할 EventManager에 추가합니다.

#### 4.3.2 2단계
- 지금까지는 잘 보이지만, App Security가 아직 완료되지 않았으므로 다시 열어보겠습니다. 이번에는 사용자 역할 ‘User’를 ‘Visitor’로 변경할 것입니다.이 사용자 역할은 이후 학습 경로에서 사용되며 축제에 등록한 사람을 나타냅니다.
- OK를 클릭하여 App Security를 닫고 MyFirstModule 모듈의 Module Security를 엽니다. 여기에서 방금 생성한 모듈 역할 (EventManager)과 User를 볼 수 있어야 합니다. User 모듈 역할을 제거합니다. 사용 중이라는 경고가 표시되지만 문제는 없습니다. 팝업에서 Delete를 클릭합니다.
- 이제 이 모듈에 새로운 모듈 역할을 추가하고 이를 Visitor라고 명명한 후, OK를 클릭하여 모듈 보안을 닫습니다.
- 다시 App Security로 돌아가서 새로운 모듈 역할 Visitor를 사용자 역할 Visitor와 연결한 후, OK를 클릭하여 App Security를 닫습니다.
![image](https://github.com/user-attachments/assets/f2119cf9-3a2c-4cb3-8dd4-2a0864f68577)
- 이제 오류 도크에서 하나의 오류가 나타납니다: 선택된 모듈 역할 ‘MyFirstModule.User’가 더 이상 존재하지 않습니다. 이를 해결하려면 ‘Home_Web’ 페이지를 열고 속성에서 ‘Visible for’ 모듈 역할을 변경해야 합니다.
![image](https://github.com/user-attachments/assets/74e8434b-38c1-417e-a6cb-06b836dbdaa2)
- 먼저 기존 모듈 역할 중 아무것도 선택하지 않고 어떤 일이 발생하는지 봅시다. 결국 홈페이지는 기본 홈페이지로 호출되므로 모듈 역할을 설정할 필요가 없습니다.
- 이제 다른 오류가 나타납니다: 페이지가 탐색 또는 버튼에서 사용되는 경우 허용된 역할 중 하나는 선택해야 한다는 오류입니다. 이는 앱 탐색에 ‘Home_Web’ 페이지를 참조하는 탐색 항목이 있기 때문입니다. 모듈 역할이 연결되어 있지 않으면 아무도 페이지에 접근할 수 없으므로 이 오류는 이해할 수 있습니다.

#### 4.3.3 3단계
- MyFirstModule 모듈의 Module Security를 열어 Page access 탭을 선택하고 두 모듈 역할을 선택합니다. OK를 클릭하여 저장합니다.
- 이제 앱 탐색을 확인하여 EventManager와 Visitor가 ‘Home_Web’ 페이지를 볼 수 있는지 확인합니다.
![image](https://github.com/user-attachments/assets/fff5e449-0236-4705-a030-8b916fc45dad)

## 5. 엔티티와 속성 만들기
- 먼저 MyFirstModule 모듈의 이름을 EventManagement로 변경합니다.
- MyFirstModule이라는 이름은 모듈에서 어떤 기능이 관리되는지에 대해 아무런 정보를 주지 않기 때문에, 모듈의 이름은 해당 기능에 대해 설명할 수 있어야 합니다.
- 이름을 선택한 후 `F2`를 눌러 쉽게 변경할 수 있습니다.
   - 변경할 모듈을 클릭 후 F2키를 누르면 이름 변경이 쉽게 됩니다. 

### 5.1 엔티티와 속성 추가하기
- **EventInformation**  
  - 설명 (문자열)  
  - 시작 날짜 (날짜 및 시간)  
  - 종료 날짜 (날짜 및 시간)  
  - 위치 (문자열)  
  - 하루 허용 방문자 수 (정수)  
- **Artist**  
  - 이름 (문자열)  
  - 전기 (문자열)  
- **Stage**  
  - 이름 (문자열)  
  - 수용 인원 (문자열)  
- **Day**  
  - 시작 날짜 (날짜 및 시간)  
  - 종료 날짜 (날짜 및 시간)  
  - 웹사이트 (문자열)  
![image](https://github.com/user-attachments/assets/75046135-cbae-4d1e-9119-1f32f0722d3b)
![image](https://github.com/user-attachments/assets/c882955a-a8d1-4c15-9a48-90690d9e93e5)

## 6. 페이지 생성 및 프로젝트에 추가하기
이제 도메인 모델에 엔티티를 설정했으니, 이 엔티티의 인스턴스를 유지 관리할 수 있는 `프론트 엔드`를 만들어야 합니다. 따라서 다음 엔티티에 대한 페이지를 생성하겠습니다:
- Artist
- Day
- Stage

### 6.1 페이지 자동 생성 방법
1. 엔티티를 우클릭하고 `Generate Overview Pages…` 옵션을 선택합니다. 이 기능은 선택한 엔티티에 대한 Overview 페이지와 NewEdit 페이지를 생성합니다. **한 번에 하나의 엔티티만 처리**해야 합니다. 그렇지 않으면 Mendix가 모든 페이지에 대한 메뉴 스니펫을 생성하여 특정 페이지에 추가하게 됩니다. 현재 우리는 레이아웃의 일부로 사용하는 앱 네비게이션을 사용하려고 하므로 필요하지 않습니다.
![image](https://github.com/user-attachments/assets/0a5aae09-472e-4523-82e1-56c579420148)
![image](https://github.com/user-attachments/assets/8da558a3-725a-485a-b02a-6c3feb3655df)</br>
개요 페이지가 'OverviewPages' 폴더에 생성되었습니다. 이 개요 페이지 중 하나를 내비게이션 메뉴에 연결하여 선택한 모든 엔티티에 대해 객체를 생성하거나 편집할 수 있습니다.
2. Overview 페이지에는 `Atlas_Default`를 선택하고, NewEdit 페이지에는 `PopupLayout`을 선택합니다. Overview 페이지와 NewEdit 페이지는 동일한 레이아웃을 사용하여 일관된 모양과 느낌을 제공합니다.
![image](https://github.com/user-attachments/assets/ce5b44c9-d831-4b31-a949-8d9f7fcd94eb)
![image](https://github.com/user-attachments/assets/cac2bce7-b3d5-417c-b6bd-48bfd5330539)

3. 1단계와 2단계를 따라 나머지 두 엔티티에 대한 페이지를 생성합니다.

4. 한 번에 하나의 엔티티에 대한 페이지를 생성한 결과, Mendix는 각 Overview 페이지와 NewEdit 페이지 쌍에 대해 3개의 폴더를 생성합니다. 이들을 하나의 폴더로 묶습니다.

5. 이제 3개의 오류가 발생했습니다. EventManager 모듈 역할이 생성된 3개의 NewEdit 페이지를 볼 수 있도록 허용하여 이 오류를 해결합니다. 오류가 없으면 작업 완료? 아니요!

6. Overview 페이지를 앱 네비게이션에 추가해야 합니다. 또한 ‘로그아웃’ 항목을 추가하여 이 기능이 사용 가능하도록 해야 할 수도 있습니다.

7. EventManager가 이러한 페이지에 접근할 수 있도록 하려면 올바른 모듈 역할을 Overview 페이지에 대한 접근 권한을 부여합니다.

결과는 다음과 같아야 합니다:
![image](https://github.com/user-attachments/assets/2b087c9c-72b8-4355-abc5-67553aa22460)
![image](https://github.com/user-attachments/assets/991c571e-fa93-482b-b955-b087be6bad29)

8. 작업이 완료되면 프로젝트에서 “No read access to attribute ‘Name’ in entity ‘EventManagement.Artist’ for user role ‘EventManager’ (with role ‘EventManager’ in module ‘EventManagement’)”와 같은 오류가 여러 개 발생합니다. 이는 보안 오류로, 사용자가 정보를 볼 수 있는 페이지를 허용했지만 엔티티 보안이 아직 구성되지 않았기 때문입니다.

9. 이를 해결하려면 EventManagement 모듈의 Module Security로 이동하여 Entity access 탭을 엽니다.

10. 액세스 규칙을 설정할 엔티티를 선택합니다.

11. 3개의 엔티티를 선택하고 EventManager 모듈 역할을 체크합니다. EventManager는 3개의 엔티티를 생성 및 삭제할 수 있으며 모든 멤버에 대해 읽기 및 쓰기 권한을 가져야 합니다.
![image](https://github.com/user-attachments/assets/c436a257-e699-41b6-b1f1-13a028cb02c2)

## 7. 단일 객체 생성하기
이전 강의에서는 `Generate Overview Pages` 기능을 사용하여 Overview 페이지와 NewEdit 페이지를 쉽게 생성하는 방법을 배웠습니다.

### 7.1 단일 인스턴스 생성하기
- 이번에는 `EventInformation` 엔티티에 대해 애플리케이션 내에서 단 하나의 인스턴스만 존재하도록 설정하고자 합니다.
- 이를 어떻게 달성할 수 있는지 알아보겠습니다! 이 정보를 위해 엔티티를 생성하는 이유는 애플리케이션이 라이브 상태에서 새로운 버전을 배포하지 않고도 이 정보를 변경할 수 있기 때문입니다.
- 여러 가지 방법이 있지만, 먼저 인스턴스가 이미 존재하는지 확인한 후 생성하는 방법을 살펴보겠습니다.

#### 7.1.1 마이크로플로우 생성하기
- 이를 위해 마이크로플로우를 생성해야 합니다.
- 앱 내비게이션에서 ‘Event Information’이라는 캡션과 적절한 아이콘이 있는 내비게이션 항목을 추가합니다.
- ‘on click’ 액션을 ‘call a microflow’로 설정합니다.

#### 7.1.2 마이크로플로우 명명규칙
- 마이크로플로우의 이름을 ‘ACT_EventInformation_Open’으로 설정합니다.</br>
![image](https://github.com/user-attachments/assets/814b12bb-162d-4c1f-8fd8-42a6682d82f7)

#### 7.1.3 마이크로플로우 접근 권한 설정
이제 이 마이크로플로우에 대한 접근 권한을 설정하여 발생한 오류를 해결합니다. EventManager만 접근할 수 있어야 합니다!</br>
![image](https://github.com/user-attachments/assets/100119b8-e922-41e5-95eb-81886009b6b4)

#### 7.1.4 마이크로플로우 편집
다음으로 새로 생성된 마이크로플로우를 다음과 같이 편집합니다:
1. 마이크로플로우는 단일 `EventInformation` 객체를 검색해야 합니다(범위를 `first`로 설정). 객체가 존재하지 않으면 새 인스턴스를 생성합니다.
![image](https://github.com/user-attachments/assets/f414ee66-fa3a-4623-8840-f2aa424db1e4)
2. 다음 단계는 발견된 또는 생성된 `EventInformation` 객체를 표시할 페이지를 여는 것입니다. 정보를 표시하기 위해 `EventInformation_NewEdit` 페이지를 생성할 수 있습니다.
**참고:** 이 접근 방식은 동시에 여러 사용자가 이 마이크로플로우를 호출할 가능성이 매우 낮은 경우에 유용합니다. 여러 사용자가 이 액션을 호출하면 여러 개의 객체가 생성될 수 있습니다.
- 마이크로플로우는 다음과 비슷해야 합니다:
- ![image](https://github.com/user-attachments/assets/546c965c-423b-4066-891b-6583558d545f)
- ![image](https://github.com/user-attachments/assets/b64a03dd-495f-43d3-a73a-68b17a9a2ab0)
- ![image](https://github.com/user-attachments/assets/d66e7d08-8fb0-41ee-992f-c5f59055e6a3)
   - `$EventInformation != empty`

#### 7.1.5 오류 해결
- 이제 6개의 오류가 발생합니다. 이 오류가 발생한 이유를 아실 수 있을 것입니다. 이제 모듈 보안으로 가서 `EventInformation` 엔티티에 대한 새로운 접근 규칙을 추가합니다.
- 이 접근 규칙을 설정하는 방법에 대해 생각해 봅시다. 이는 다른 엔티티와 다릅니다. 현재 우리는 마이크로플로우를 사용하여 이 객체를 생성하고 있으므로 ‘Allow creating new objects’ 체크박스를 선택할 필요가 없습니다. 이 옵션은 기본 ‘Create’ 버튼에만 영향을 미칩니다. ‘Allow deleting existing objects’를 선택해야 할까요? 이 경우 객체를 한 번만 생성하고 이후에는 업데이트만 하므로 이 옵션이 필요하지 않습니다. 이 옵션은 기본 ‘Delete’ 버튼에만 영향을 미칩니다. 마이크로플로우를 통해 객체를 삭제하는 것은 여전히 가능합니다. EventManager는 모든 속성에 대해 읽기 및 쓰기 권한이 필요합니다.
**참고:** ‘Default rights for new members’를 ‘None’으로 항상 설정하는 것이 좋습니다. 이렇게 하면 보안 오류가 발생할 때 항상 신중하게 생각하게 되며, 애플리케이션의 접근성이 과도하게 설정되지 않도록 할 수 있습니다.
**참고:** Mendix에서 특정 오류가 표시되는 순서에 계층 구조가 있음을 눈치챘나요? 이는 일부 오류는 다른 오류가 해결된 후에만 검증될 수 있기 때문입니다.
이제 애플리케이션 내에서 이벤트 정보를 유지 관리할 수 있습니다. 이 모듈에서 남은 일은 계정을 유지 관리할 수 있도록 하는 것입니다.
- ![image](https://github.com/user-attachments/assets/035a544a-d7bd-4681-b1ee-a4f5d736fe2c)
  
## 8. 계정 유지 관리
기능을 테스트할 수 있도록 계정을 생성할 수 있어야 합니다. Mendix에는 이를 위한 페이지가 있으므로, 내비게이션에 추가하기만 하면 됩니다.
1. 내비게이션 항목을 추가합니다.
2. 클릭 시 액션을 '페이지 표시'로 변경합니다.
3. Administration 모듈 내에서 `Account_Overview` 페이지를 찾습니다.
![image](https://github.com/user-attachments/assets/ac1a9569-a9ba-4a60-9b94-ccb0bbd58f9e)

--- 
# troubleshooting
## 1. JDK 버전 문제 해결 방법(멘딕스 안에서..) 
### 1.1 문제상황
![image](https://github.com/user-attachments/assets/ce0bbf35-73fe-4a50-9159-78cc4247c267)
- JDK 21 버전이 필요한 상황이기 때문에 이를 받아서 넣어주기만 하면 된다

### 1.2 해결 방법
![image](https://github.com/user-attachments/assets/cdd7f17f-aa57-4d53-a1ad-0fb6692cebd3)
- [JDK 21버전 다운 받는 곳](https://adoptium.net/temurin/releases/?version=21)

## 2. Gradle 버전 문제 해결 방법(JDK 21버전 이상 사용시에 해결방법..) 
### 2.1 문제상황
![image](https://github.com/user-attachments/assets/318c8432-bb0d-4ae8-aa1b-91c2cbf9cfb7)

### 2.2 해결 방법
- [Gradle 릴리즈된 버전 별 다운 받는 곳](https://gradle.org/releases/)
- JDK 21의 경우라면 gradle 7.6 이상 버전을 사용해야 하기 때문에 해당 페이지에서 원하는 버전을 받아서 원하는 위치에 해당 zip 파일을 두고 이를 gradle 위치로 잡아주면 됩니다.

----
# 퀴즈 
## Question 1
### 문제
앱 내에서 사용자 피드백을 수집하는 가장 쉬운 방법은 무엇입니까?
- 제공된 "문의하기" 링크를 사용
- Mendix 앱에 자동으로 포함된 피드백 기능 사용
- **Feedback 위젯을 사용** (정답)
- 사용자가 피드백을 작성하고 제출할 수 있는 페이지 만들기
### 해석 및 설명
가장 효율적인 방법은 Mendix에서 제공하는 **Feedback 위젯**을 사용하는 것입니다. Feedback 위젯은 사용자가 앱 내에서 간단하게 피드백을 남길 수 있도록 설계된 기능입니다. "문의하기" 링크를 사용하는 방법은 직접적으로 피드백을 수집하는 것이 아니라, 외부 경로로 연결되는 방식이며, 페이지를 만드는 것은 비효율적일 수 있습니다. Mendix 앱에 자동으로 포함된 피드백 기능이 있다고 말하는 선택지는 부정확합니다. 따라서, Feedback 위젯을 사용하는 것이 가장 빠르고 쉬운 방법입니다.

## Question 2
### 문제
페이지 접근 권한은 어디에서 설정됩니까?
- 모듈 보안 (Module Security)
- **앱 보안 (App Security)** (정답)
- 엔티티 속성 (Properties of Entity)
- 도메인 모델 (The Domain Model)

### 해석 및 설명
페이지 접근 권한은 사용자가 앱에서 어떤 페이지에 접근할 수 있는지 관리하는 부분입니다. 이는 **App Security(앱 보안)**에서 설정되며, 앱의 보안 수준과 사용자 역할에 따라 페이지 접근 권한을 부여할 수 있습니다. 모듈 보안은 페이지가 아닌 모듈 내의 보안을 관리하며, 엔티티 속성이나 도메인 모델에서는 페이지 접근 권한을 설정하지 않습니다. 따라서 페이지 접근 권한 설정은 **App Security**가 맞는 답입니다.

## Question 3
### 문제
AllowedNumberOfVisitorsPerDay에 사용할 수 있는 적절한 검증 규칙은 무엇입니까?
- 고유 (Unique)
- 최대 길이: 20 (Maximum length: 20)
- 정규 표현식: 숫자 문자만 (Regular Expression: numeric characters only)
- **범위 <= 1000 (Range <= 1000)** (정답)

### 해석 및 설명
`AllowedNumberOfVisitorsPerDay` 속성은 하루에 허용되는 방문자의 수를 나타냅니다. 이 값은 정해진 범위 내에서 숫자 값으로 제한되는 것이 가장 적합합니다. 따라서, 방문자의 수가 1000명을 초과하지 않도록 **범위 <= 1000** 규칙을 적용하는 것이 올바른 방법입니다. '고유(Unique)'나 '최대 길이'는 숫자가 아닌 문자열의 특성에 맞는 규칙이며, 정규 표현식도 이 경우 보다는 숫자 범위 설정이 더 적합합니다.

## Question 4
### 문제
앱의 계정을 쉽게 관리하는 방법은 무엇입니까?
- 로그인 및 계정 관리 페이지를 만듭니다.
- 데이터베이스를 수동으로 편집합니다.
- **내장된 Account_Overview 페이지에 네비게이션을 연결합니다** (정답)
- 항상 슈퍼유저로 로그인합니다.

### 해석 및 설명
Mendix는 계정을 관리하기 위한 내장 페이지를 제공합니다. **Account_Overview** 페이지는 이러한 내장 페이지 중 하나로, 계정 관리를 쉽게 할 수 있도록 도와줍니다. 이 페이지에 네비게이션을 연결하면 사용자 계정을 관리하기 위해 별도의 페이지를 만들 필요가 없습니다. 데이터베이스를 수동으로 편집하거나 항상 슈퍼유저로 로그인하는 방식은 비효율적이고 실수의 위험이 큽니다. 따라서 **내장된 Account_Overview 페이지에 네비게이션을 연결하는 것**이 가장 효율적인 방법입니다.

## Question 5
### 문제
엔티티를 하나의 객체로 제한하는 것이 가능합니까?
- 모듈 보안 (Module Security)에서 가능합니다.
- **마이크로플로우 (Microflow)에서 가능합니다** (정답)
- 불가능합니다.
- 엔티티 속성 (Entity Properties)에서 가능합니다.

### 해석 및 설명  
엔티티를 하나의 객체로 제한하는 것은 Mendix에서 가능합니다. 이를 위해 **마이크로플로우**를 사용할 수 있습니다. 마이크로플로우를 통해 새로운 객체를 생성하기 전에 기존 객체가 존재하는지 확인할 수 있으며, 이미 존재하는 경우 새로운 객체를 생성하지 않도록 제어할 수 있습니다. 모듈 보안이나 엔티티 속성에서는 객체 수를 제한할 수 없으며, 이 작업은 기본적으로 **마이크로플로우**에서 이루어집니다.


