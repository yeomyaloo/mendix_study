# 학습 목표
이 모듈을 완료하면 다음을 할 수 있습니다:
- Mendix에서 제공하는 언어 설정을 설명할 수 있다.
- Mendix에서 사용할 수 있는 번역 도구를 나열할 수 있다.
- 선택한 언어로 애플리케이션을 번역할 수 있다.

# 언어 설정
- 국제 비즈니스 세계에서 우리는 전 세계의 사용자 및 고객과 소통하게 됩니다.
- 가능한 한 많은 사람들을 위해, Mendix를 사용하여 애플리케이션을 여러 언어로 제공할 수 있습니다.
- Mendix는 애플리케이션을 쉽게 확장할 수 있도록 지원합니다.
- Mendix는 번역 가능한 텍스트를 사용하여 라벨, 버튼 캡션, 데이터 그리드 열, 메뉴 항목 등을 손쉽게 번역할 수 있게 합니다.
- 완성된 애플리케이션은 영어에서 프랑스어로, 또는 스페인어에서 독일어로 빠르게 번역할 수 있습니다.
- 번역 가능한 텍스트는 프로젝트에 저장되며 언제든지 번역에 사용될 수 있습니다.

## 1. 프로젝트 언어
- 여러 언어를 추가할 수 있으며, 하나를 기본 언어로 설정할 수 있습니다.
- 기본 언어는 사용자가 애플리케이션을 사용할 때 볼 언어입니다.

## 2. 개발 언어
- 앱 개발을 시작하면 기본 언어가 설정됩니다.
- 기본적으로는 영어(US)로 설정되지만, 필요에 따라 다른 언어로 변경할 수 있습니다.
- 최선의 방법은 프로젝트를 시작할 때 개발 언어를 설정하는 것입니다. 왜냐하면 새로운 라벨, 메시지 등이 선택한 언어 라이브러리에 추가되기 때문입니다.
- 만약 영어(US)를 개발 언어로 설정해두고 네덜란드어로 모델링을 시작하면, 영어 라이브러리 파일에 네덜란드어 단어가 혼합될 수 있습니다.
- 이는 나중에 수정할 수 있지만, 처음부터 올바르게 설정하는 것이 더 쉽습니다.
- 개발 콘텐츠 언어는 툴바에서 변경할 수 있습니다.

## 3. 번역 가능한 텍스트
- 개발 언어를 변경하면 페이지는 선택된 언어로 라벨과 콘텐츠를 표시합니다.
- 아직 선택된 언어로 번역되지 않은 라벨은 기본 언어 텍스트를 꺾쇠 괄호(< Requests >) 안에 표시합니다.
- 애플리케이션이 아직 번역되지 않은 라벨과 함께 배포되면, 해당 라벨은 기본 언어로 표시되지만 꺾쇠 괄호는 표시되지 않습니다.
- 프로젝트의 언어 설정에서 번역 체크의 엄격성을 구성할 수 있습니다.

# 번역 도구
Mendix는 기본적으로 사용할 수 있는 여러 번역 도구를 제공합니다:

## 일괄 번역
각 라벨을 번역할 때, 꺾쇠 괄호 안에 있는 단어를 새 단어로 교체하면 됩니다. 하지만 애플리케이션의 모든 페이지, 마이크로플로우, 기타 문서들을 일일이 번역하는 것은 매우 힘든 작업입니다. 그래서 Mendix Studio Pro는 일괄 번역 옵션을 제공합니다. 이 기능은 소스 및 대상 언어의 번역 가능한 모든 텍스트 목록을 보여주며, 이를 통해 애플리케이션(또는 애플리케이션의 일부)을 훨씬 효율적으로 번역할 수 있습니다. 특정 모듈을 필터링하고, 특정 라벨을 검색하는 기능도 제공합니다.

## 텍스트 발생 위치
일부 라벨과 텍스트는 목록에 여러 번 나올 수 있기 때문에, 해당 텍스트가 앱의 어디에서 사용되고 있는지를 아는 것이 중요합니다. 이를 위해 일괄 번역 창 하단에 있는 발생 위치(Occurrence) 창을 사용할 수 있습니다.

예를 들어, 영어 라벨에 ‘Address’라는 단어가 두 번 있을 수 있습니다. 이를 네덜란드어로 번역할 때, 이 단어가 “사람의 연락처”를 의미하는지 또는 “사람에게 특정 방식으로 말하는 것”을 의미하는지를 아는 것이 중요합니다. 네덜란드어에서 첫 번째 의미는 ‘Adres’로, 두 번째 의미는 ‘Aanspreken’으로 번역되기 때문입니다.

## 번역 내보내기/가져오기
Mendix Studio Pro 외부에서 언어를 번역하고 싶다면, 번역 가능한 텍스트를 Excel(.xlsx) 형식으로 내보낼 수 있습니다. 그러면 각 언어에 대한 열이 있는 Excel 파일이 생성됩니다. 번역이 완료되면, Excel 파일을 프로젝트에 다시 가져오면 됩니다.

# 언어 추가
애플리케이션을 다른 언어로 번역하는 첫 번째 단계는 해당 언어를 앱에 추가하는 것입니다. 이 작업은 프로젝트 설정 창에서 할 수 있습니다.

## 1. 언어 추가 방법
1. **App Explorer**에서 `Settings`를 더블 클릭하세요. 그러면 `App Settings` 창이 열립니다.
2. **Languages** 탭으로 이동합니다.
3. `Add` 버튼을 클릭하여 새로운 언어를 추가합니다.
4. `Dutch, Netherlands` 언어를 검색한 후 `OK`를 클릭하세요.
5. 다시 `OK`를 클릭하여 `Settings` 창을 닫습니다.

## 2. 앱 번역
### 2.1 방법
1. **현재 언어**를 네덜란드어로 설정하세요. (해당 7.1 Introduction 파트에서 제공하는 모듈을 다운 받았다면 네덜란드어가 이미 포함되어 있을 것이다.)
![image](https://github.com/user-attachments/assets/d3e2c52f-e13b-4fe3-9107-7752bd2814d0)

2. `Request_Wizard_Step1` 페이지를 열어보면, 다른 단어들에 각괄호 (<>)가 있는 것을 볼 수 있습니다. 이는 일부 단어가 자동으로 네덜란드어 시스템 값으로 설정되기 때문입니다(예: ‘Knop’, 네덜란드어로 버튼을 의미). 다른 단어들은 자동으로 번역되지 않아 각괄호가 표시됩니다.

3. **영어**로 다시 전환하여 번역할 텍스트 발생 위치를 파악하세요.

4. 툴바의 **Language** 메뉴에서 `Batch Translate...`를 클릭하세요.
   - **Source language**: English, United States (기본값).
   - **Destination language**: Dutch, Netherlands.
   - `OK`를 클릭하세요.

5. **Batch translate** 창에서 `Cancel`을 검색하세요. 여러 번 발생한 이 라인을 한 번에 번역할 수 있습니다!

6. 이를 `Annuleren`으로 번역하고 `Translate` 버튼을 클릭하세요.
![image](https://github.com/user-attachments/assets/0da9f85a-cf16-4d01-a553-1e86c5f413cc)

7. 창을 닫고 다시 언어를 네덜란드어로 설정하세요. 버튼이 번역된 것을 보셨나요?

8. 이제 `HeaderExpenses` 스니펫을 열고 `<Submitted>`를 `<Aangevraagd>`로, `<Approved>`를 `<Goedgekeurd>`로 번역하세요.

9. 언어를 다시 영어로 변경해보세요. 여전히 `Submitted`와 `Approved`로 표시되어 있나요?

# 퀴즈
## Question 1:
How many source and destination languages can you specify?
- One source, many destinations
- One source, one destination
- Many sources, one destination
- Many sources, many destinations

### 번역:
**몇 개의 소스 및 목적지 언어를 지정할 수 있습니까?**
- 하나의 소스, 여러 목적지
- 하나의 소스, 하나의 목적지
- 여러 소스, 하나의 목적지
- 여러 소스, 여러 목적지

### Explanation:
You can specify one source language and multiple destination languages for translations in Mendix. This allows you to translate your app from one language to several other languages efficiently.

**해설:**
Mendix에서는 하나의 소스 언어에서 여러 목적지 언어로 번역할 수 있습니다. 이를 통해 한 언어에서 다른 여러 언어로 앱을 효율적으로 번역할 수 있습니다.

정답: **하나의 소스, 여러 목적지**

---

## Question 2:
What does default project language define?
- The language selected for the given user at the moment of account creation.
- The language which users will see when using your app.
- The language in which project content is visualized in Studio Pro.
- The language which will be selected by the user at the first log-in.

### 번역:
**기본 프로젝트 언어는 무엇을 정의합니까?**
- 계정 생성 시 사용자에게 선택된 언어
- 사용자가 앱을 사용할 때 볼 언어
- Studio Pro에서 프로젝트 콘텐츠가 시각화되는 언어
- 사용자가 처음 로그인할 때 선택하는 언어

### Explanation:
The default project language defines the language that users will see when using your app. This is the language displayed to users if no other language settings are applied.

**해설:**
기본 프로젝트 언어는 사용자가 앱을 사용할 때 기본적으로 표시되는 언어를 정의합니다. 다른 언어 설정이 적용되지 않으면 이 언어가 사용자에게 표시됩니다.

정답: **사용자가 앱을 사용할 때 볼 언어**

---

## Question 3:
When and how a default language of an app needs to be selected?
- Manually at the moment of app creation.
- Automatically at the moment of app creation.
- Manually when opening an app in Studio Pro.
- Automatically when opening an app in Studio Pro.

### 번역:
**앱의 기본 언어는 언제, 어떻게 선택되어야 합니까?**
- 앱 생성 시 수동으로
- 앱 생성 시 자동으로
- Studio Pro에서 앱을 열 때 수동으로
- Studio Pro에서 앱을 열 때 자동으로

### Explanation:
The default language of an app is automatically set at the moment of app creation. This setting can be adjusted manually later if needed.

**해설:**
앱의 기본 언어는 앱 생성 시 자동으로 설정됩니다. 필요에 따라 나중에 수동으로 조정할 수 있습니다.

정답: **앱 생성 시 자동으로**

---

## Question 4:
Where can you choose the development language?
- In the language library
- In the system texts
- In the project folder
- In the toolbar of Studio Pro

### 번역:
**개발 언어는 어디에서 선택할 수 있습니까?**

- 언어 라이브러리
- 시스템 텍스트
- 프로젝트 폴더
- Studio Pro의 툴바

### Explanation:
The development language can be chosen in the toolbar of Studio Pro. This language setting is used for displaying project content during development.

**해설:**
개발 언어는 Studio Pro의 툴바에서 선택할 수 있습니다. 이 언어 설정은 개발 중에 프로젝트 콘텐츠를 표시하는 데 사용됩니다.

정답: **Studio Pro의 툴바**

---

## Question 5:
Which of the following functionalities do you need to use to show a complete list of all translatable texts of a source and destination language?
- Import translation
- Batch translation
- Occurrence window
- Export translation

### 번역:
**소스와 목적지 언어의 모든 번역 가능한 텍스트 목록을 표시하려면 어떤 기능을 사용해야 합니까?**
- 번역 가져오기
- 일괄 번역
- 발생 창
- 번역 내보내기

### Explanation:
To show a complete list of all translatable texts for a source and destination language, you use the Batch translation functionality. This tool helps manage translations more efficiently by listing all translatable texts and their occurrences.

**해설:**
소스와 목적지 언어의 모든 번역 가능한 텍스트 목록을 표시하려면 일괄 번역 기능을 사용합니다. 이 도구는 번역 가능한 모든 텍스트와 그 발생 위치를 목록화하여 번역 관리를 효율적으로 도와줍니다.

정답: **일괄 번역**





