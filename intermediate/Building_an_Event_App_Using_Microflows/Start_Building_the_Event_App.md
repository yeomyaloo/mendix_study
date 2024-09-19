# Learning Objectives - 학습 목표
1. **Create an app**  
   **앱 생성**  
   - 새로운 앱을 생성할 수 있습니다.
2. **Add a feedback widget to your app**  
   **앱에 피드백 위젯 추가**  
   - 앱에 피드백 위젯을 추가할 수 있습니다.
3. **Set up security in your app**  
   **앱의 보안 설정**  
   - 앱의 보안을 설정할 수 있습니다.
4. **Create entities and attributes in your app**  
   **앱에서 엔터티 및 속성 생성**  
   - 앱에서 엔터티와 속성을 생성할 수 있습니다.
5. **Use the Generate Overview Pages function to easily create Overview and NewEdit pages**  
   **Generate Overview Pages 기능을 사용하여 Overview 및 NewEdit 페이지 쉽게 생성**  
   - Generate Overview Pages 기능을 사용하여 Overview 및 NewEdit 페이지를 쉽게 생성할 수 있습니다.
6. **Build a microflow to ensure that for a specific entity, only one instance can exist in your application**  
   **특정 엔터티에 대해 애플리케이션에 하나의 인스턴스만 존재하도록 보장하는 마이크로플로우 빌드**  
   - 특정 엔터티에 대해 애플리케이션에 하나의 인스턴스만 존재하도록 하는 마이크로플로우를 빌드할 수 있습니다.

# 실제 프로젝트 세팅
## 1. 프로젝트 생성
### 1.1 방법
1. **Open Mendix Portal to get started.**  
   **Mendix 포털을 열어 시작합니다.**

2. **In the top-right corner, you see the Create App button, so go ahead and click it.**  
   **오른쪽 상단에서 Create App 버튼을 보게 되며, 클릭합니다.**

3. **Choose the Blank Web App as a starting point.**  
   **시작 지점으로 Blank Web App을 선택합니다.**

4. **Go to Advanced Settings and select Template Version Studio Pro 10.0.0 (Template v10.0.9976), then click on Select This Template.**  
   **Advanced Settings로 이동하여 Template Version Studio Pro 10.0.0 (Template v10.0.9976)을 선택한 후, Select This Template을 클릭합니다.**

5. **Name the app “Event Management”, choose a project icon and then click Create App.**  
   **앱 이름을 “Event Management”로 정하고, 프로젝트 아이콘을 선택한 후 Create App을 클릭합니다.**

6. **You have now created the project, in the next lecture you will open the app in Studio Pro.**  
   **이제 프로젝트를 생성하였으며, 다음 강의에서 Studio Pro에서 앱을 열게 됩니다.**

## 2. Open and Edit Your Project - 프로젝트 열기 및 편집하기
- Mendix 포털을 통해 프로젝트를 여는 방법을 알고 있지만, Mendix Marketplace에서 모든 Studio Pro 버전을 찾을 수 있다는 것도 기억하시나요?
- Mendix Marketplace에서 Mendix Studio Pro 버전 10.0.0을 다운로드하세요.
**Note:** We currently only offer installers for Windows operating systems. If you have a Mac then please use a Windows virtual machine.  
**참고:** 현재 Windows 운영 체제용 설치 프로그램만 제공합니다. Mac을 사용하는 경우 Windows 가상 머신을 사용해 주세요.


## 3. # Adding a Feedback Widget - 피드백 위젯 추가하기
사용자 피드백은 앱 개발 시 중요합니다. 이는 앱을 지속적으로 개선하여 사용자 요구에 더 잘 맞출 수 있게 합니다. 애플리케이션 사용자에게 피드백을 제공할 수 있는 가능성을 주는 것은 좋은 실천입니다. Mendix는 쉽게 구현할 수 있는 위젯을 개발했습니다. 이 위젯은 사용자 역할, 페이지 이름, 화면 해상도와 같은 정보를 자동으로 제공하기 때문에 매우 유용합니다.
재사용 가능하도록, 스니펫을 사용할 것입니다. 스니펫은 페이지와 레이아웃에서 사용할 수 있는 재사용 가능한 인터페이스 부분입니다. 스니펫에 대한 변경 사항은 이 스니펫이 사용된 모든 장소에 적용됩니다. 스니펫의 사용은 "Don't Repeat Yourself (DRY)" 원칙을 기반으로 하며, 이는 인터페이스의 수정할 장소를 줄이고 매끄러운 전환과 사용자 친화적인 경험을 제공합니다.
### 3.1 피드백 위젯 추가하는 방법
1. App Explorer에서 FeedbackWidget 스니펫을 찾을 수 있습니다. 이 스니펫은 자동으로 프로젝트에 추가되었습니다. 도구 상자에서 데이터 뷰, 데이터 그리드 등과 같은 위젯처럼 이 스니펫을 페이지에 추가할 수 있습니다. 이 스니펫은 이미 Atlas_Default 및 Atlas_TopBar 레이아웃의 일부이며, 앱에서는 Atlas_Default 레이아웃을 사용할 것입니다.
2. Feedback Widget의 Advanced 탭으로 가면 App ID가 이미 설정되어 있어야 합니다. 설정되어 있지 않다면, Mendix Portal로 가서 프로젝트의 General Settings를 열어 이 ID를 쉽게 찾을 수 있습니다.
3. Feedback 위젯 속성 창의 Project 탭에서 Allow screenshots 속성이 Yes로 설정되어 있는지 확인합니다. 이 설정을 통해 피드백 항목에 대한 모든 가능한 정보를 얻을 수 있습니다.
4. Authentication 탭에서 Authentication method로 Custom authentication을 선택합니다. 그런 다음 아래 스크린샷에 표시된 대로 User Object (1), User name attribute (2), Email attribute (3)를 입력합니다. 이 속성을 구성하면 피드백을 추가하는 로그인된 사용자에게 자동으로 이 정보가 채워집니다.

