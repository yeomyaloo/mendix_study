# Using Version Management
## 목표
- 버전 관리 저장소에 앱을 업로드하기
- 앱의 기록에 접근하고 지금까지 적용된 모든 변경 사항 확인하기
- 앱 기록에서 찾을 수 있는 다양한 이벤트 유형 설명하기
- 로컬 데이터를 팀원들과 공유하기
- 앱 충돌 해결하기
- 이전 앱 수정본 열기
- 충돌 상황 방지하기
- 브랜치 작업하기
- 자체 버전 관리 서버 사용하기

## 버전 관리 저장소에 앱 업로드하기 
![image](https://github.com/user-attachments/assets/25063d69-68df-41af-9764-a7d954a8a1b9) </br>
Mendix에서 새로운 앱을 시작할 때, 시스템은 자동으로 앱을 위한 저장소를 생성할 것을 제안합니다. 아직 버전 관리되지 않은 앱은 언제든지 버전 관리된 저장소에 연결할 수 있습니다. 다른 앱을 재사용하거나 기존 앱의 복사본을 만들 때 이러한 상황이 발생할 수 있습니다. 이 경우 Mendix는 "버전 관리 서버에 업로드" 옵션을 제공하며, 이는 버전 관리 메뉴에서 찾을 수 있습니다.

## 히스토리
앱의 히스토리를 통해 지금까지 앱에 적용된 변경 사항을 확인할 수 있습니다. 이러한 변경 사항을 바탕으로, 새로 추가된 기능을 되돌려야 할 경우 되돌릴 시점을 선택할 수 있습니다.

`Mendix Portal` 또는 `Studio Pro` 내에서 히스토리를 확인할 수 있습니다.

### 1. Mendix Portal에서 History 확인하기
Mendix Portal에서는 앱 페이지에서 일반 > 팀 서버로 이동하면 다음과 같은 네 가지 유형의 이벤트를 볼 수 있습니다:

- 커밋(Commits)
- 생성된 태그(Created tags)
- 생성된 브랜치 라인(Created branch lines)
- 삭제된 브랜치 라인(Deleted branch lines)
참고: 태그가 지정된 버전은 Mendix 배포 패키지를 빌드하는 데 사용된 수정본입니다.

#### 각 항목별로 다음 정보를 확인할 수 있습니다:
- 설명 메시지
- 이벤트가 발생한 날짜 및 시간
- 이벤트를 트리거한 담당자 이름
- 사용된 Studio Pro 버전 (태그 이벤트의 경우 Mendix Studio Pro 버전을 표시하지 않음)
- 관련된 사용자 스토리
Mendix Studio Pro 내에서는 **버전 관리 > 히스토리...**로 이동하면 다음 두 가지 유형의 이벤트를 확인할 수 있습니다:

커밋(Commits)
생성된 브랜치 라인(Created branch lines)

#### 각 항목별로 다음 정보를 확인할 수 있습니다:
- 리비전 번호
- 변경 유형을 나타내는 기호
- 이벤트 작성자
- 이벤트 발생 날짜
- 이벤트 발생 시간
- 이벤트 메시지
- 관련된 사용자 스토리
- 모델의 변경 사항
- 디스크(저장소)의 변경 사항
이 두 가지 히스토리 보기에는 약간의 차이가 있습니다. 이는 같은 이벤트를 다른 관점에서 보기 때문입니다.

## 스냅샷 포함
- 스냅샷을 이용하면 팀원들과 데이터 베이스 공유를 할수 있습니다. 
Mendix는 로컬 배포를 위해 사용할 수 있는 **자체 기본 데이터베이스를 제공**합니다. 이를 통해 외부 데이터베이스에 의존하지 않고, 이 내장된 데이터베이스를 사용하여 로컬에서 테스트하고 실행할 수 있습니다. 많은 사람들이 모르는 사실은, 이 **데이터베이스를 팀과 공유할 수 있다는 점**입니다. 이를 통해 팀원들도 동일한 데이터셋을 사용하여 앱을 테스트할 수 있으며, 이는 시간을 절약하고 발생한 문제를 재현하는 데 도움이 됩니다.

`Mendix Studio Pro`에서 데이터를 스냅샷으로 저장하려면 버전 관리 메뉴로 이동합니다: 버전 관리 > 데이터 스냅샷 추가.

이 작업은 데이터의 스냅샷을 생성하고 data-snapshot.zip 파일을 앱의 배포 디렉토리에 추가합니다. 다음 번에 커밋할 때, 팀원들은 이 파일을 지정된 배포 폴더에 압축 해제하여 해당 데이터베이스를 사용할 수 있습니다. </br>
![image](https://github.com/user-attachments/assets/489e73d5-64fe-491b-b5dd-35a7ad5d3049)

## 충돌 해결법과 이를 다루는 방법 (Conflicts and How to Resolve Them)
팀과 함께 앱을 개발하다 보면 여러 가지 충돌이 발생할 수 있으며, 이러한 충돌은 새로 커밋하기 전에 반드시 해결해야 합니다. 충돌은 앱 모델의 문서(예: 페이지, 마이크로플로우)와 관련되거나 저장소의 다른 문서와 관련될 수 있습니다. 이 섹션에서는 충돌의 종류와 해결 방법을 알아보겠습니다.

### 1. 충돌의 종류
Mendix에서 주로 발생하는 충돌은 크게 두 가지입니다:

#### 1.1 수정-수정 충돌 (Modify-Modify Conflict)
정의: 같은 문서를 팀원이 **동시에 수정할 때 발생**합니다.
예시:
- 페이지의 입력 필드 레이블을 두 사람이 모두 변경하려 할 때
- 마이크로플로우의 특정 활동을 서로 다르게 수정할 때
- 도메인 모델에서 동일한 모듈 역할의 엔터티 액세스 규칙을 변경할 때
#### 1.2 수정-삭제 충돌 (Modify-Delete Conflict)
정의: 한 사람이 문서를 **수정하는 동안 다른 사람이 그 문서를 삭제했을 때 발생**합니다.
예시:
- 팀원이 DataGrid의 열을 삭제한 상태에서 내가 해당 열을 수정하려 할 때
- 누군가 마이크로플로우를 삭제했는데 내가 이를 수정하려 할 때
- 삭제된 연관 관계를 내가 이름 변경하려고 할 때
#### 1.3 기타 충돌
- 동일한 이름의 문서를 추가: 예를 들어, 동일한 이름의 페이지나 마이크로플로우를 여러 명이 동시에 추가할 때 발생
- 동일한 Marketplace 모듈을 가져오는 경우: 이미 가져온 모듈을 다시 가져오면 충돌이 발생할 수 있습니다.

### 2. 충돌 해결 방법
Mendix에서는 충돌을 해결하기 위해 다음 단계를 따를 수 있습니다.

#### 2.1 차이점 확인
로컬 작업 복사본과 온라인 버전 간의 차이점을 먼저 확인해야 합니다. 이를 위해 변경 사항 창에서 내가 수정한 부분을 확인할 수 있으며, 업데이트 후에는 팀원이 수정한 부분도 다운로드됩니다.
#### 2.2 팀원과 소통
충돌이 발생한 문서를 수정한 팀원과 협력하여 어떤 버전을 사용할지 결정하는 것이 중요합니다. 소통을 통해 충돌을 빠르게 해결할 수 있습니다.
#### 2.3 충돌 해결
Mendix Studio Pro에서 충돌을 해결하려면 다음 방법을 사용할 수 있습니다:
- '그들의 버전으로 해결': 상대방의 버전을 선택하면 해당 문서가 내 문서를 대체합니다.
- 내 문서의 복사본을 만들고 두 버전을 비교한 후 최종 결정을 내리는 것도 가능합니다. 예를 들어, 마이크로플로우의 경우 내 문서를 복사한 뒤 상대방의 버전을 선택해 둘 다 비교할 수 있습니다.

### 3. 충돌 예방 방법
충돌을 예방하려면 다음과 같은 전략을 사용할 수 있습니다:
- 정기적인 업데이트와 커밋: 자주 업데이트하고 커밋하는 습관을 통해 팀 간의 작업 충돌을 최소화할 수 있습니다.
- 작업 분리: 팀원 간의 작업 영역을 명확히 구분하여 동일한 문서를 동시에 수정하는 상황을 방지할 수 있습니다.
- 도메인 모델 합의: 도메인 모델의 기초는 스프린트마다 팀원들과 합의하여 변경사항이 한쪽에서 일방적으로 이루어지지 않도록 합니다.
이러한 절차를 통해 충돌을 관리하고 원활하게 협업할 수 있습니다.

## 이전 수정본 열기 (Opening Older Revisions)
전 버전을 열 수 있습니다. 이전 버전을 열어 모델의 두 수정본 간의 차이를 식별하거나, 라이브 환경에서 배포된 수정본을 디버깅할 수 있습니다.

이전 수정본을 열려면 해당 수정본에서 브랜치를 생성한 후, 새 Studio Pro 세션에서 그 브랜치를 열면 됩니다. 단, 이 브랜치는 **조회 및 분석 목적으로만 사용**해야 하며, 이 브랜치에서 **변경 작업을 하지 않는 것이 중요**합니다. 이미 해당 수정본 이후로 여러 커밋이 이루어졌기 때문입니다.(Make sure to only use this branch for viewing and analyzing purposes, don’t make changes to this branch since you already have a number of commits done after that revision.)

## 브랜치 사용법(Using Branches)
앱이 프로덕션 환경에 배포된 후, 브랜치를 생성하는 방법을 알면 유용합니다. 이는 실행 중인 프로덕션 앱에 영향을 주지 않고 새로운 기능 개발을 계속할 수 있게 해줍니다. 또한, 새로운 기능 개발과 긴급 수정(핫픽스)을 분리하는 것이 모범 사례입니다. 완료되지 않은 기능과 함께 핫픽스를 배포하는 것은 바람직하지 않기 때문입니다.

브랜치를 사용하는 방법에 대해 알아보겠습니다.

### 1. 브랜치 생성
브랜치 생성은 Studio Pro에서 버전 관리 > 브랜치 라인 관리로 이동하여 할 수 있습니다.

#### 1.1 브랜치를 생성하는 세 가지 방법이 있습니다:
- 메인 라인의 리비전(개정)
- 다른 브랜치 라인의 리비전(개정)
- 태그된 버전

### 2. 변경 사항 병합(Merge Changes)
``` plain text
포토 픽스(port fix)란?
멘딕스에서 브랜치 라인에서 작업한 특정 변경 사항을 메인 라인으로 옮길 때 사용하는 기능입니다. 이 기능은 브랜치 전체를 병합하지 않고 선택한 일부 변경 사항만 메인 라인으로 옮기고자 할 때 유용합니다. 주로 단일 기능이나 수정 사항을 프로덕션 환경에 반영하고 싶을 때 사용합니다.

포트 픽스 사용 시 주의 사항
포트 픽스는 메인 라인에서만 사용 가능합니다.
Mendix의 모범 사례에서는 전체 브랜치를 병합하는 것이 더 권장됩니다. 포트 픽스를 자주 사용하면 추후 관리가 복잡해질 수 있기 때문입니다.
```
**포트 픽스(Port Fix) (메인 라인에서만 사용 가능):** 
**특정 부분을 브랜치 라인에서 메인 라인으로 이동하는 옵션**입니다. 이 기능은 브랜치에서 단일 기능을 프로덕션으로 이동할 때 유용할 수 있습니다. 필요한 기능을 선택할 때 하나 또는 여러 개의 리비전을 선택할 수 있습니다. 하지만 Mendix의 모범 사례에 따라 전체 브랜치만 이동하는 것이 권장되므로 자주 사용되지는 않습니다.

### 3. 기능 브랜치 병합 (메인 라인에서만 사용 가능): Merge feature branch (only available on main line)
이 기능은 전체 브랜치를 메인 라인에 병합할 때 사용되며, 메인 라인에서만 가능합니다. 일반적으로 브랜치 라인에서 개발이 완료되면 메인 라인에 병합합니다.

- Studio Pro에서 메인 라인을 열고 Version control > Merge Changes Here.을 선택하여 병합을 시작합니다.
  - ![image](https://github.com/user-attachments/assets/124cbe12-1deb-498b-926b-01dc14c885ee)
 
**참고:** 병합하기 전에 주 브랜치에서 모든 변경 사항을 커밋하세요.
- 병합할 기능 브랜치를 선택한 후, 브랜치 라인에 적용된 변경 사항이 변경 사항 창에 나열됩니다.
- 변경 사항을 메인 라인에 커밋하면 브랜치가 메인 라인에 성공적으로 병합됩니다.

### 4. 고급 병합 (메인 라인 및 브랜치 라인에서 사용 가능): Advanced merge (available on main line and branch lines)
- 고급 병합 옵션은 메인 라인 또는 브랜치 라인의 다양한 리비전을 선택한 라인에 병합할 수 있도록 합니다.

### 5. 변경 사항 되돌리기
때로는 앱의 이전 버전으로 되돌리고, 변경 사항을 취소해야 할 때가 있습니다. 이 경우 시작 버전과 끝 버전을 지정하여 변경 사항을 되돌릴 수 있습니다. 여러 커밋을 한 번에 되돌리거나, 시작 및 끝 리비전을 동일하게 지정하여 단일 커밋만 되돌릴 수도 있습니다.

### 6. 브랜치 삭제
브랜치를 다른 브랜치 또는 메인 라인에 병합한 후에는 원래 브랜치 라인을 삭제하는 것이 좋습니다. 사용하지 않는 브랜치를 정리하면 브랜치 관리를 더 쉽게 할 수 있습니다. 브랜치 라인 관리에서 브랜치를 선택한 후 삭제를 선택하여 브랜치를 삭제할 수 있습니다.

## 자신의 Git 서버 이용하기 (Using Your Own Git Server)
기본적으로 Mendix는 Team Server를 활성화할 때 버전 제어 환경을 자동으로 설정합니다. 이는 일일 백업과 운영 관리로 인한 번거로움 없이 제어를 유지하면서 최대 가동 시간을 보장하는 데 도움이 됩니다.

### 2. 자신의 git 서버로 앱 배포 디렉토리 지정하는 방법
#### 2.1 설명
- 기존에는 멘딕스 자체적으로 팀서버 활성화 시 버전 제어 환경을 자동으로 설정해줍니다.
- 그러나 앱 배포 디렉토리를 개인적으로 지정해서 저장할 수도 있습니다.
- 이를 위해서는 먼저 자신의 Git 서버를 설정해야 합니다.
- 다음으로, Studio Pro에서 편집 > 환경설정 > 버전 제어 > Git으로 개인 버전 제어 활성화로 이동하여 개인 버전 제어를 활성화해야 합니다.
  - `Edit > Preferences > Version Control > Enable private version control with Git.`
- 마지막으로, 버전 제어 메뉴 > 버전 제어 서버로 업로드 항목에서 추가 옵션을 사용할 수 있으며, 이제 개인 서버 옵션을 사용하여 저장소 주소를 입력하고 구성을 완료할 수 있습니다.
  - `Version Control menu > item Upload to Version Control Server` 
#### 2.2 방법
- ![image](https://github.com/user-attachments/assets/6a49784a-51b8-4cd2-8c4f-a6ccf113cfea)
- ![image](https://github.com/user-attachments/assets/451a52bc-8e3e-4f2a-8301-3ed007b6fab0)
- ![image](https://github.com/user-attachments/assets/dffd8922-c42b-4faf-8832-cf7c13799f18)

## 퀴즈
### Question 1
When working in an app with version control, which concept would you use to share your database with your team?

Your answer: By creating a data snapshot and adding it to the deployment directory of your app.

Explanation: When using version control in an app, sharing the database with your team can be achieved by creating a data snapshot. This snapshot is a backup of your current database state, which you can add to the deployment directory of your app. This allows team members to access a consistent version of the database that matches the application’s current state.

해설: 버전 제어를 사용하는 앱에서 데이터베이스를 팀과 공유하려면 데이터 스냅샷을 생성하는 방법을 사용할 수 있습니다. 데이터 스냅샷은 현재 데이터베이스 상태의 백업으로, 앱의 배포 디렉토리에 추가할 수 있습니다. 이를 통해 팀원들이 애플리케이션의 현재 상태와 일치하는 데이터베이스의 일관된 버전에 접근할 수 있습니다.

### Question 2
What type of conflict occurs when you and your colleague both modified the microflow implementing the delete behavior?
-> 삭제 동작을 구현하는 마이크로 플로우를 나와 동료가 같이 수정했을 때 어떤유형의 충돌이 발생하나요? 
Your answer: Modify-Modify

Explanation: A Modify-Modify conflict occurs when two or more team members have made changes to the same part of a file or feature, such as a microflow, in a version control system. In this case, both you and your colleague modified the microflow implementing the delete behavior, leading to a conflict that needs to be resolved by merging the changes.

해설: Modify-Modify 충돌은 두 명 이상의 팀원이 파일이나 기능의 동일한 부분(예: 마이크로플로우)을 변경했을 때 발생합니다. 이 경우, 당신과 동료가 모두 삭제 동작을 구현하는 마이크로플로우를 수정하였기 때문에 충돌이 발생하며, 이 충돌은 변경 사항을 병합하여 해결해야 합니다.

### Question 3
What is a tagged version?

Your answer: A revision that has been used to build a Mx deployment package.

Explanation: A tagged version refers to a specific revision in the version control system that has been marked for a particular purpose, such as building a Mendix (Mx) deployment package. Tagging a version helps in identifying and referencing that particular state of the codebase, which can be useful for deployment and version tracking.

해설: 태그된 버전은 버전 제어 시스템에서 특정 용도로 표시된 **특정 리비전을 의미**합니다. 예를 들어 Mendix (Mx) 배포 패키지를 빌드할 때 사용된 버전이 태그된 것입니다. 버전을 태그하는 것은 코드베이스의 특정 상태를 식별하고 참조하는 데 도움이 되며, 배포 및 버전 추적에 유용합니다.

++ 추가 (브랜치를 생성하는 3가지 방법 중 태그 빼고 2개..) 
1. 메인 라인의 리비전(개정)
Your answer: A revision from the main line used as the base for creating new branches or for merging.

Explanation: A main line revision refers to a specific state of the main branch, which is the primary line of development. This revision represents the current stable state of the project. Creating new branches from the main line allows you to develop features or fixes based on the latest stable code, ensuring that changes are integrated into the main codebase effectively.

해설: 메인 라인의 리비전은 **주요 개발 브랜치에서의 특정 상태를 의미**합니다. 이 리비전은 프로젝트의 현재 안정적인 상태를 나타냅니다. 메인 라인에서 새로운 브랜치를 생성하면 최신 안정 코드 기반에서 기능 개발이나 수정 작업을 시작할 수 있으며, 변경 사항이 효과적으로 메인 코드베이스에 통합되도록 합니다.

2. 다른 브랜치 라인의 리비전(개정)
Your answer: A revision from a different branch line used as the base for creating new branches or for merging changes.

Explanation: A revision from a different branch line refers to a specific state of a branch other than the main branch. This type of revision is typically used for working on specific features or fixes separate from the main line. Creating branches from a different branch line allows for isolated development of features or experimental changes before merging them back into the main branch or other relevant branches.

해설: 다른 브랜치 라인의 리비전은 메인 브랜치가 아닌 다른 **브랜치의 특정 상태를 의미**합니다. 이 리비전은 일반적으로 메인 라인과 별도로 특정 기능이나 수정을 작업할 때 사용됩니다. 다른 브랜치 라인에서 브랜치를 생성하면 기능 개발이나 실험적인 변경 작업을 독립적으로 진행할 수 있으며, 완료된 후 메인 브랜치나 다른 관련 브랜치에 병합할 수 있습니다.
### Question 4
Which function is used to merge a complete branch into the mainline and is only available on the main line?

Your answer: Merge feature branch

Explanation: The "Merge feature branch" function is used to integrate changes from a feature branch into the mainline branch (also known as the main or master branch). This operation consolidates all the changes from the feature branch into the mainline, ensuring that the new features or fixes are included in the primary codebase. This function is typically available only on the mainline.

해설: "기능 브랜치 병합" 기능은 기능 브랜치에서 메인라인 브랜치(또는 메인 브랜치, 마스터 브랜치)로 변경 사항을 통합하는 데 사용됩니다. 이 작업은 기능 브랜치의 모든 변경 사항을 메인라인에 통합하여 새로운 기능이나 수정 사항이 기본 코드베이스에 포함되도록 보장합니다. 이 기능은 일반적으로 메인라인에서만 사용 가능합니다.

### Question 5
Which of the below mentioned options can be used to merge revisions into and from all lines, main line or branch line?

Your answer: Advanced merge

Explanation: The "Advanced merge" function is used to merge revisions between various branches, including both the main line and branch lines. This option allows for more complex merge scenarios where changes need to be integrated across different branches, ensuring that all revisions are appropriately reconciled.

해설: "고급 병합" 기능은 메인라인과 브랜치 라인 모두를 포함하여 다양한 브랜치 간에 리비전을 병합하는 데 사용됩니다. 이 옵션은 여러 브랜치에 걸쳐 변경 사항을 통합해야 하는 복잡한 병합 시나리오를 지원하며, 모든 리비전이 적절하게 조정되도록 보장합니다.

