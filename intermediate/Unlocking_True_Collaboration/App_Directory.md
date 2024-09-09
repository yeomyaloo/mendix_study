## 1. directory Location
### 1-1. 폴더 열기
![image](https://github.com/user-attachments/assets/cbde6949-bbdf-4e58-a338-eeaf4956c000)
### 1-2. 폴더 확인하기
![image](https://github.com/user-attachments/assets/18b43498-19ca-4a68-a84f-a80d07ce39bb)


## 2. Locating the App Directory
### Javascriptsource
javascriptsource 폴더 내에는 앱 모듈 구조와 유사한 구조가 있지만, 실제로 nanoflow를 위한 JavaScript 액션이 정의된 모듈만 포함되어 있습니다. 이는 해당 모듈에 속하는 모든 JavaScript 소스를 쉽게 찾을 수 있게 해주며, 이 모듈을 다른 앱에서 재사용할 때 편리합니다.

### Javasource
javasource 폴더 내에는 앱 모듈 구조와 유사한 구조가 있습니다. 이 폴더는 microflows와 관련된 모든 Java 소스를 포함합니다. 새 앱에서는 9개의 모듈이 있으며, 앱이 최소한 한 번 실행된 후에 이 구조가 디렉터리에 반영됩니다. 모든 모듈이 보이지 않는 경우, 로컬에서 앱을 실행하여 디렉터리에 나타나게 할 수 있습니다.

참고: 때때로, 동일한 디렉터리 레벨에 서드파티 Java 파일을 구현하는 서브폴더가 있는 다른 폴더를 찾을 수 있습니다. 예를 들어 Apache 라이브러리 같은 것들이 있습니다.

이제 모듈 폴더 중 하나, 예를 들어 system 폴더를 확대해 보면 다음과 같은 구조를 확인할 수 있습니다.

### Actions
actions 폴더는 특정 모듈에서 생성된 모든 Java 액션의 대상 폴더입니다. 이는 Studio Pro에서 생성한 것입니다. 현재 이 폴더에는 VerifyPassword.java라는 파일만 있어야 하며, 이는 System 모듈에 현재 있는 단일 Java 액션입니다. 아래 이미지를 참고하거나 자신의 앱에서 확인할 수 있습니다.

### Datasets
이제 myfirstmodule의 javasource 폴더로 전환하면 다음을 볼 수 있습니다:

datasets 폴더는 특정 모듈에서 생성된 모든 데이터 세트의 대상 폴더입니다. 이 폴더도 Studio Pro에서 생성된 것입니다. 현재는 폴더가 비어 있어야 하지만, 데이터 세트 파일을 생성하고 Java 액션을 소스로 선택하면 디렉터리에서 생성된 것을 확인할 수 있습니다. OQL 쿼리를 소스로 선택하면 이 디렉터리에서 파일을 볼 수 없으며, OQL 코드는 모델에서 유지됩니다.

참고: 여기서는 데이터 세트가 무엇인지 설명하는 것이 아니라, 앱 디렉터리의 구조를 설명하는 것이 목표입니다. 데이터 세트에 대한 설명은 다른 학습 경로에서 다룰 것입니다. 그러나 System 모듈은 읽기 전용이므로, 다른 모듈을 사용하여 데이터 세트를 생성하는 방법을 시연할 것입니다.

## Clean Directory
### 1. Create Dataset
![image](https://github.com/user-attachments/assets/9cde7838-6f41-4644-95f9-cbb95f103c5a)
![image](https://github.com/user-attachments/assets/5699fb0d-a414-4dc8-ac4f-2d49c393e678)
- Now you should be able to see the file in your app directory: …\javasource\myfirstmodule\datasets

## The Clean Directory Example - Continue
현재 javasource\system 폴더 구조를 좀 더 자세히 살펴보겠습니다:
### Proxies
system 모듈의 proxies 폴더로 돌아가면, microflows라는 폴더와 constants라는 폴더, 그리고 여러 개의 파일이 있습니다.

proxies 폴더는 모든 엔티티(지속적 및 비지속적)와 모든 열거형(enumerations)을 나타냅니다. 내부 microflow 폴더에는 Microflows.java라는 파일 하나만 있으며, 이 파일은 모듈의 모든 마이크로플로우 이름을 저장합니다. 이는 Java 개발을 위한 것입니다.

### Resources
주 앱 디렉터리로 돌아가면, resources 폴더를 살펴보겠습니다. 이 폴더에는 애플리케이션 작동 방식에 직접적인 영향을 미치는 파일들(예: HTML 파일 또는 구성 파일)만 있어야 합니다. 이 파일들은 앱 모델과 함께 패키징됩니다. 이 폴더의 파일들은 Java 리소스로 접근할 수 있습니다. 이 폴더를 사용하는 Mendix 모듈의 예로는 SAML 모듈과 Deeplink 모듈이 있습니다.

### Theme
theme 폴더에는 애플리케이션의 스타일링을 구성하는 파일과 폴더가 포함되어 있습니다. 이 폴더의 변경은 HTML/CSS/SASS 지식이 필요합니다. 이 지식을 통해 기존 디자인 속성을 확장하거나 변경하거나 새로운 디자인 속성을 생성할 수 있습니다.

### Userlib
userlib 폴더에는 사용자 정의 Java 기능을 지원할 수 있는 Java 라이브러리가 포함되어 있습니다. 이 폴더의 내용은 Community Commons Function Library 또는 Email 모듈과 같은 모듈을 다운로드하면 변경됩니다. 다운로드한 기능을 더 이상 사용하지 않을 경우 이 파일을 변경하지 마세요. 모듈을 제거하면 Java 라이브러리가 자동으로 이 디렉터리에서 제거되지 않으므로 수동으로 제거하는 것을 잊지 마세요.

### Widgets
widgets 폴더에는 .mpk 확장자를 가진 파일만 포함됩니다. 이 파일들은 Studio Pro에서 사용할 수 있는 위젯을 반영합니다. Add-on widgets 그룹에 나열된 위젯의 수와 앱 디렉터리의 파일 수가 다를 수 있습니다. 이는 하나의 .mpk 파일이 여러 개의 위젯을 포함할 수 있기 때문입니다. 예를 들어 Charts.mpk 파일은 Area chart, Bar chart, Bubble chart 등 여러 차트를 포함하고 있습니다.

다시 말하지만, 이 파일을 수정하려면 위젯을 만드는 방법에 대한 지식이 필요합니다. 이는 Mendix API와 JavaScript에 대한 지식이 요구됩니다.

Files in this folder
최상위 수준(루트 폴더) 외에도 앱 디렉터리에는 다음과 같은 파일들이 있습니다:

### .mpr
.mpr 파일은 Studio Pro가 앱을 열 때 필요한 파일입니다.

### mpr.bak
.mpr.bak 파일은 .mpr 파일의 백업 파일입니다. 이 백업 파일은 Mendix 버전 업그레이드나 Team Server 앱 업데이트 시 문제가 발생할 경우 앱을 복원하는 데 사용할 수 있습니다.

### .mpr.lock
<AppName>.mpr.lock 파일은 이 앱이 현재 Studio Pro에서 열려 있음을 나타냅니다. 이 파일은 Windows 설정에 따라 숨겨질 수 있습니다

## Optional Files and Folders

### Deployment folder
배포 폴더는 앱을 로컬에서 실행하는 데 필요한 배포 파일을 포함합니다. 이 폴더에는 로컬 데이터베이스를 지원하는 데 필요한 여러 폴더와 파일, 애플리케이션 사용 중 저장된 파일, Mendix가 애플리케이션을 실행하기 위해 해석하는 소스가 포함되어 있습니다.

### Releases folder
Studio Pro로 배포 패키지를 생성할 때, Mendix는 기본적으로 이 패키지를 releases 폴더에 저장합니다.

### Packages folder
앱 패키지를 생성할 때, Mendix는 자동으로 이 패키지를 저장할 위치를 제공합니다. packages 폴더는 생성된 패키지를 저장합니다.

### data-snapshot.zip file
data-snapshot.zip 파일은 Studio Pro에서 데이터 스냅샷을 생성할 때 생성됩니다. 이 파일에는 팀원들이 재사용할 수 있는 로컬 데이터베이스가 포함되어 있습니다.

### .classpath file
이 파일은 Eclipse에서 앱을 가져오는 데 필요한 파일입니다. 자세한 정보는 여기에서 확인할 수 있습니다.

### .project file
이 파일은 Eclipse에서 앱을 가져오는 데 필요한 파일입니다. 자세한 정보는 여기에서 확인할 수 있습니다.

### < root folder >.launch file
이 파일은 Eclipse에서 앱을 가져오는 데 필요한 파일입니다.

## Best Practices
앱 디렉터리를 깨끗하고 최신 상태로 유지하는 것이 매우 중요합니다! 이 디렉터리의 내용은 작업 결과에 따라 변경되므로, 추가한 모듈과 위젯을 인식하고 더 이상 사용하지 않는 경우 적시에 제거하는 것이 필요합니다.
1. 모듈을 제거할 때는 userlib 폴더에서 Java 라이브러리를 수동으로 제거하는 것을 잊지 마세요.
2. resources 폴더의 내용은 배포 폴더 내의 model/resources 폴더로 복사됩니다. 배포 폴더에 추가할 수 없는 파일은 이 resources 폴더에 추가할 수 있습니다.
3. 버전 관리를 사용하는 경우(다음 모듈에서 설명할 예정), 커밋하기 전에 앱을 업데이트하여 새로운 기능을 확인하고 충돌을 해결하는 것이 중요합니다.

## 퀴즈
### Question 1
Which folders contain source information tied to a specific module enabling reuse of this module in another app?

Your answer:
Javascriptsource and Javasource folders

해석:
특정 모듈과 연결된 소스 정보를 포함하여 이 모듈을 다른 앱에서 재사용할 수 있게 하는 폴더는 무엇인가요?
답변:
Javascriptsource와 Javasource 폴더

### Question 2
The VerifyPassword.java file in the System module is stored in which of the JavaSource sub-folders?

Your answer:
Actions

해석:
System 모듈의 VerifyPassword.java 파일은 JavaSource 하위 폴더 중 어떤 곳에 저장되나요?
답변:
Actions

### Question 3
The Microflows.java file is stored in which sub-folder of the JavaSource directory?

Your answer:
Proxies

해석:
Microflows.java 파일은 JavaSource 디렉토리의 어떤 하위 폴더에 저장되나요?
답변:
Proxies

### Question 4
Which of the following sources are typically stored in the Resources folder of the App Directory?

Your answer:
Configuration files, HTML and Java files

해석:
다음 중 어떤 소스들이 일반적으로 앱 디렉터리의 Resources 폴더에 저장되나요?
답변:
구성 파일, HTML 및 Java 파일

### Question 5
Files and folders that form the styling of your application are typically stored in which of the following folders?

Your answer:
Theme

해석:
애플리케이션의 스타일링을 형성하는 파일과 폴더는 일반적으로 다음 중 어떤 폴더에 저장되나요?
답변:
Theme









