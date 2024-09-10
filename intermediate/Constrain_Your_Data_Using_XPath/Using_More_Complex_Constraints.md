# 더 복잡한 제한 사항 사용하기
## 1. 학습 목표
By the end of this module, you will be able to:
1. Constrain data using the UserRole system variable
- 사용자 역할 시스템 변수를 사용하여 데이터 제한하기
2. Write XPaths using Operators and Functions
- 연산자와 함수를 사용하여 XPath 작성하기
3. Use DateTime tokens in XPaths
- XPath에서 DateTime 토큰 사용하기
4. Perform an empty check on data using XPaths
- XPath를 사용하여 데이터의 비어있는지 확인하기

# 사용자 역할 시스템 변수란? (What is the UserRole System Variable?)
## 1. 의의
- 이전 모듈에서는 '[%CurrentObject%]'와 '[%CurrentUser%]'와 같은 Mendix XPath 변수를 배웠습니다. 또한, 플랫폼이 열거형을 사용하여 XPath를 구성하는 데 어떻게 도움을 줄 수 있는지 배웠습니다. 이번 모듈에서는 **사용자 역할 시스템 변수를 사용**하여 계정을 역할에 따라 제한하는 방법을 배울 것입니다.
- 보안 문서에서 사용자 역할을 생성하면, Mendix는 자동으로 해당 역할에 대한 시스템 변수를 생성합니다. 예를 들어 '[%UserRole_Manager%]'와 같은 변수가 생성됩니다. 이 변수는 XPath가 시스템 모듈의 UserRole 엔터티와의 연관으로 끝날 때만 자동 완성 메뉴에 나타납니다.
    - 사용자 역할 생성 -> 멘딕스가 자동으로 해당 역할에 대한 시스템 변수를 생성한다.
- 이 연관성은 계정 선택을 특정 사용자 유형으로 제한하는 데 유용합니다. 다음 강의에서는 이 기능을 사용하여 사용자가 자신의 휴가 요청을 승인할 승인자를 선택할 수 있도록 하는 방법을 배울 것입니다.
## 2. 사용법
### 2.1 UserRole 변수를 사용하여 데이터 제약하기
현재 애플리케이션에서는 사용자가 새로운 휴가 요청을 생성할 수 있지만, 승인자를 선택할 수 있는 메커니즘이 없습니다. 첫 번째 반복에서는 비즈니스 결정으로 관리자가 자신의 승인자를 선택할 수 있어야 하며, 다른 사용자의 승인자로는 오직 관리자만 선택할 수 있어야 합니다.

이를 구현하기 위해 애플리케이션에서 Reference Selector에서 선택할 수 있는 객체를 XPath를 사용하여 제한합니다. 그 후, VacationRequest_NewEdit 페이지에서 저장 버튼을 수정하여 마이크로플로우를 호출하고 휴가 요청의 상태를 'Submitted'로 설정하도록 합니다.

### 2.2 올바른 Reference Selector 찾기
1. VacationRequest_NewEdit 페이지를 엽니다.
2. 이 페이지에서 VacationRequest_Submitter 연관 관계를 설정하는 Reference Selector 위젯을 찾습니다. 두 개의 Account 위젯의 속성을 열어야 할 수 있습니다. 이 위젯들은 페이지가 생성될 때 자동으로 생성된 것입니다.
3. Submitter 위젯의 Edit Reference Selector 팝업을 엽니다.
    - 기본적으로 이 필드는 "Account"라는 레이블이 붙어 있습니다. 레이블 캡션 속성을 "Submitter"로 변경합니다.
    - OK를 클릭합니다.
4. VacationRequest_Approver 연관 관계에 대해서도 같은 절차를 수행합니다.
    - 레이블 캡션을 "Approver"로 변경합니다.

### 2.3 XPath를 사용하여 선택 가능한 계정 제한하기
1. VacationRequest_Approver Reference Selector 위젯의 속성 창에서 Selectable objects 탭을 클릭합니다.
2. 이 탭에서 Source를 XPath로 설정합니다.
3. XPath 자동 완성 도구를 사용하여 모든 시스템 사용자 역할에 해당하는 시스템 변수를 확인할 수 있습니다. "Manager" 역할에 대한 변수를 선택합니다. 즉, 완성된 XPath는 다음과 같아야 합니다:
```xpath
[System.UserRoles='[%UserRole_Manager%]']
```
4. OK를 클릭합니다.
이제 관리자로 로그인한 사용자가 이 페이지를 열어 요청에 대한 'Approver'를 선택할 때, 드롭다운 목록에는 'Manager' 사용자 역할이 할당된 사용자만 표시됩니다!

### 2.4 기능 테스트하기
이 기능을 테스트하려면 'Employee' 사용자 역할을 가진 사용자로 로그인할 수 있어야 합니다. 계정을 만들려면 Administration.AccountOverview 페이지를 애플리케이션 탐색에 추가합니다. 탐색에도 로그아웃 액션을 추가하는 것을 잊지 마세요!
- ![image](https://github.com/user-attachments/assets/7330b237-ac21-42c7-9977-e010ec103a4e)
- ![image](https://github.com/user-attachments/assets/23839218-9d5a-4a4a-b1e7-901564f6ea69)
- ![image](https://github.com/user-attachments/assets/532b421b-d6df-4921-928d-2df04d93e0e8)
    - 해당 페이지에 해당 권한을 넣어주면 navigation에 해당 User Roles가 들어갑니다.

이제 MxAdmin 사용자로 로그인하고 해당 페이지에서 계정을 생성할 수 있습니다. 두 개의 'Employee' 역할을 가진 계정과 두 개의 'Manager' 역할을 가진 계정을 생성하여 수행한 작업을 테스트해 보세요.

- 'Employee' 역할을 가진 사용자로 로그인하고 요청을 제출합니다.
- 로그아웃한 후 MxAdmin으로 다시 로그인합니다.
- 관리자는 제출된 요청 목록을 보고 요청을 열어 'Approver' 레이블이 붙은 드롭다운을 사용하여 승인자를 지정할 수 있습니다. 필드에 나타나는 이름은 'Manager' 사용자 역할이 할당된 계정만 포함됩니다.

# XPath 표현식
- [XPath 표현식 공식 문서](https://docs.mendix.com/refguide/xpath-expressions/)
## 1. Exist Expression (존재 표현법)
### 1.1 의의
- 해당 표현법은 XPath를 사용해서 특정 연관관계(association)이나 속성(attribute)이 존재하는지, 즉 값이 설정되어 있는지를 확인하는 방법입니다.
### 1.2 예시를 통한 설명
- 연관관계가 존재하는지 확인하는 표현식은 한 엔티티가 다른 엔티티와 연관관게를 맺고 있는지를 확인하는 것입니다.
- Mendix에서는 특정 엔티티가 다른 엔티티와 관계를 맺고 있는지를 확인할 수 있습니다.
#### 1.2.1 엔티티 구조도
```plaintext
VacationRequest
+-------------------+
| VacationRequest    |
|-------------------|
| Status             |
| StartDate          |
+-------------------+
         |
         | VacationRequest_Approver
         v
+-------------------+
| Account (Approver)|
|-------------------|
| UserName          |
| Role              |
+-------------------+
```
- VacationRequest: 휴가 요청을 나타내는 엔티티로, 상태(Status)와 시작 날짜(StartDate) 등의 속성을 가집니다.
- Account: 휴가 요청의 승인자(Approver) 역할을 하는 계정을 나타내는 엔티티입니다
#### 1.2.2 예시
```xpath
[VacationManagement.VacationRequest_Approver/Administration.Account]
```
- 이 표현법은 VacationRequest 엔티티에 Approver(승인자)로 설정된 Account가 있는지 확인하는 표현식입니다.
- `VacationManagement.VacationRequest_Approver/Administration.Account`는 VacationRequest 엔티티에서 Approver 연관관계를 통해서 Account 엔티티로 연결된 것을 나타냅니다. 
    - VacationRequest: 휴가 요청 데이터
    - Approver: 휴가 요청을 승인하는 관리자
    - Account: 관리자의 계정 정보
- 해당 표현식은 Approver(승인자)와 계정이 연결될 VacationRequest들을 반환합니다. 

#### 1.2.3 예시2(연관관계가 존재하지 않음을 표현)
```xpath
[not(VacationManagement.VacationRequest_Approver/Administration.Account)]
```
- 이 XPath는 VacationRequest 엔티티가 Approver와 연관관계가 없는 데이터를 반환합니다. 즉, 승인자가 지정되지 않은 휴가 요청들을 가져옵니다.
- `not()` 함수는 조건을 부정합니다. 따라서 승인자(Approver)가 설정되지 않은 VacationRequest를 찾을 때 유용합니다.
### 1.3 추가로 자바로 알아보는 멘딕스 Domain Model
- 자바와 ORM 개념을 통해서 알아보는 멘딕스 도메인 모델의 의미를 알아보자.
#### 1.3.1 Entity
![image](https://github.com/user-attachments/assets/5dd4eb37-7075-403d-b3f4-fd479d858d8a)
- 해당 붉은 선 안에 개념이 Entity이다.
- 이때 당연하게 Account 역시 Entity이다.
#### 정의
- 엔티티는 애플리케이션에서 관리할 데이터의 단위를 나타냅니다. 각 엔티티는 특정 데이터 구조를 정의하며, 하나의 엔티티는 데이터베이스의 테이블과 유사한 개념입니다.
#### 의의
- 데이터 구조화: 엔티티는 데이터의 속성과 유형을 정의하며, 이는 데이터베이스에서 테이블의 역할을 합니다.
- 비즈니스 로직: 엔티티는 비즈니스 로직을 구현하는 데 필요한 핵심 데이터 단위를 제공합니다. 예를 들어, VacationRequest 엔티티는 휴가 요청과 관련된 정보를 저장합니다.
- 객체 간의 관계 정의: 엔티티는 다른 엔티티와의 관계를 정의하여 데이터의 연관성을 명확히 합니다.  
#### 1.3.2 Association(연관관계)
![image](https://github.com/user-attachments/assets/112564f0-c5ea-46e6-8041-419fe2f11138)
#### 정의
- 연관관계는 엔티티 간의 관계를 정의합니다. 이는 객체 간의 관계를 설정하여 데이터의 연관성을 모델링합니다.
#### 의의
- 데이터 통합: 연관관계는 서로 다른 엔티티 간의 데이터를 연결하여 통합된 정보를 제공합니다. 예를 들어, VacationRequest 엔티티는 Employee 엔티티와 연관될 수 있으며, 이를 통해 요청한 직원의 정보를 쉽게 가져올 수 있습니다.
- 비즈니스 규칙 적용: 연관관계를 통해 비즈니스 규칙을 정의하고 데이터를 관리합니다. 예를 들어, VacationRequest 엔티티의 Approver 필드는 요청을 승인할 관리자와의 연관관계를 설정합니다.
- 데이터 접근: 연관관계를 통해 다른 엔티티의 데이터를 쉽게 조회하고 처리할 수 있습니다. 예를 들어, VacationRequest 엔티티에서 VacationRequest_Approver 연관관계를 통해 해당 요청의 승인자를 참조할 수 있습니다.
#### 1.3.3 자바 코드로 알아보자
```
// Define the VacationRequest entity
public class VacationRequest {
    private Account approver; // Represents the association to the Account entity
    private Account submitter;
    // Getter and Setter for approver
    public Account getApprover() {
        return approver;
    }

    public void setApprover(Account approver) {
        this.approver = approver;
    }
}

// Define the Account entity
public class Account {
    // Account fields and methods
}

```
- ORM(그러니까 JPA기술 사용한 경우라고 생각하고 위의 클래스가 엔티티 클래스라면) 관점으로 살펴본다면 해당 작업은 저렇게 필드에 해당 Account를 넣고 ManyToOne 관계로 매핑을 해줬을 것이다.
    - 하나의 계정(회원)은 여러개의 휴가 요청을 보낼수 있기 때문이다. 

# XPath 함수
- [XPath 함수 공식 문](https://docs.mendix.com/refguide9/xpath-constraint-functions/)

# 함수와 연산자를 사용하여 제약하기 (Constrain Usong Functions and Operators)
## 1. 설명
이전 강의에서 함수와 연산자에 대해 배웠습니다. 이를 이번 사용 사례에 어떻게 적용할 수 있을지 살펴보겠습니다:
### 1.1 시나리오
- 회사는 연간 단위로 휴가를 관리하며, 지난 해 동안 승인된 휴가 요청에 대한 통찰을 얻고 싶어합니다.
- 이를 위해 홈 페이지에 새 탭을 추가하여 해당 연도 초부터 승인된 휴가 요청을 표시합니다.
- 일반 사용자에게는 자신이 요청한 휴가만 보이도록 하고, 관리자와 관리자 권한을 가진 사용자에게는 회사 전체의 요청이 보이도록 합니다.
- 하지만 이를 수행하기 전에 관리자들이 휴가 요청을 승인할 수 있는 절차를 제공해야 합니다!
### 1.2 시나리오 수행 단계
- 이 작업을 수행하기 위한 단계는 다음과 같습니다:
    - 관리자들을 위한 '승인' 프로세스 추가
    - 홈 페이지에 휴가 요청 데이터를 표시하는 탭 추가
    - 그리드에 있는 객체를 ‘승인’ 상태이고, 시작일이 해당 연도 초보다 이후인 요청으로 제한
    - 이후 강의에서 위의 각 단계를 어떻게 수행하는지에 대한 지침을 제공합니다.
## 2. 사용법 (모두다 표시 x) 
![image](https://github.com/user-attachments/assets/12cdcbf3-ae39-4561-a9e3-d25c249084ee) </br>
- 해당 마이크로플로우 작업이 끝나면 보안 설정을 해줘야하는데 이때 마이크로플로우 창 아무곳이나 오른쪽 클릭을 한 뒤에 properties를 눌러서 설정에 들어가 보안을 설정하면 된다.

## 3. 시나리오2
### 3.1 시나리오(홈 페이지에 새 탭 추가하기)
다음으로 승인된 휴가 요청이 표시될 탭을 추가해야 합니다. 이를 위해 다음 단계를 따르세요:
1. App Explorer를 사용하여 Home_Web을 엽니다.
2. 기존 ‘Submitted’ 탭을 마우스 오른쪽 버튼으로 클릭하고 Add tab page right를 선택합니다.
3. 이 탭을 더블 클릭하여 Approved this year와 같은 의미 있는 이름으로 변경합니다.
4. 이 탭에 VacationRequest 객체의 Data Grid를 추가합니다. Data View의 내용 자동 채우기 옵션을 선택하세요.

# 빈 값 확인하기 (Checking for Empty Values)
## 1. 설명
- 지금까지 특정 필드의 값을 확인하여 XPath 제약조건을 작성했습니다.
- 그러나 값이 할당되지 않은 엔티티를 찾으려면 상황이 더 복잡해집니다. 예를 들어, 현재 사용자와 연결되지 않은 모든 VacationRequest를 검색하려면 어떻게 해야 할까요? Mendix 플랫폼은 이러한 쿼리를 쉽게 할 수 있도록 도와주는 함수들을 제공합니다.

## 2. empty
- 어떤 속성이나 연관관계에 값이 없을 때, 플랫폼은 empty 값을 사용하여 이를 확인할 수 있습니다.

### 2.1 예시:
```
arduino
//VacationManagement.VacationRequest[Status = empty]
```
- 이 XPath는 Status에 값이 할당되지 않은 VacationRequest 목록을 반환합니다.

`not()`</br>
`empty` 확인 외에도, Mendix 플랫폼에는 조건이 충족되지 않았는지 확인할 수 있는 `not()` 함수가 있습니다. 이 함수는 연산자와 속성을 사용하여 만든 표현식을 평가하는 데 사용할 수 있습니다.

```css
코드 복사
//VacationManagement.VacationRequest[not(StartDate > '[%BeginOfCurrentDay%]')]
```
- 이 XPath는 StartDate가 오늘 이후가 아닌 VacationRequest 목록을 반환합니다. 즉, 오늘 이전에 발생한 휴가 요청들이 반환됩니다.
- 이 함수는 연관관계가 설정되지 않았는지 평가하는 데에도 사용할 수 있습니다.

```arduino
코드 복사
//VacationManagement.VacationRequest[not(VacationRequest_Submitter)]
```
- 이 XPath는 submitter 계정과 연결되지 않은 모든 VacationRequest를 반환합니다.

```css
코드 복사
//Administration.Account[not(VacationRequest/VacationRequest.StartDate = '[%BeginOfCurrentDay%]')]
```
- 이 XPath는 오늘 시작되는 VacationRequest가 없는 모든 계정, 또는 VacationRequest가 전혀 없는 계정 목록을 반환합니다. 이 쿼리는 오늘 출근한 모든 직원을 확인하는 데 사용될 수 있습니다.


# 퀴즈
## 영어
### Question 1
Let’s assume you add a new decimal attribute to the VacationRequest entity called ‘DaysUsed’. The value represents the total amount of days used for the requested vacation. If you write a microflow with a Retrieve action, what will be the return if we use the following XPath?
[DaysUsed < 4.5 and not(VacationManagement.VacationRequest_Submitter/Administration.Account)]

### Your Answer
A list of all VacationRequests that are shorter than 4.5 days and do not have a Submitter assigned.

### Explanation
This XPath filters VacationRequest objects based on two conditions:

DaysUsed < 4.5: It finds vacation requests that are shorter than 4.5 days.
not(VacationManagement.VacationRequest_Submitter/Administration.Account): It finds requests that do not have a submitter assigned.
Thus, the XPath returns only those vacation requests that satisfy both conditions.

## 한국어 번역
### 질문 1
VacationRequest 엔티티에 ‘DaysUsed’라는 새로운 소수(decimal) 속성을 추가한다고 가정해 보겠습니다. 이 값은 요청된 휴가의 총 일수를 나타냅니다. Retrieve 액션이 있는 마이크로플로우를 작성할 때, 다음 XPath를 사용하면 반환되는 결과는 무엇인가요?
[DaysUsed < 4.5 and not(VacationManagement.VacationRequest_Submitter/Administration.Account)]

### 답변
4.5일보다 짧고 제출자가 지정되지 않은 모든 VacationRequest 목록이 반환됩니다.

### 설명
이 XPath는 두 가지 조건을 기반으로 VacationRequest 객체를 필터링합니다:

DaysUsed < 4.5: 4.5일보다 짧은 휴가 요청을 찾습니다.
not(VacationManagement.VacationRequest_Submitter/Administration.Account): 제출자가 지정되지 않은 요청을 찾습니다.
따라서 이 XPath는 두 조건 모두를 만족하는 휴가 요청만 반환됩니다.

## 영어2
### Question 2
If we populate a DataGrid of VacationRequest entities with the following XPath constraint, what will happen?
[StartDate = empty]

### Your Answer
The grid will show all VacationRequests where the StartDate is not populated.

### Explanation
This XPath finds objects where the StartDate attribute is empty, meaning it has no value set. Therefore, the DataGrid will display only those vacation requests where the StartDate field is empty.

## 한국어 번역
### 질문 2
다음 XPath 제약조건을 사용하여 VacationRequest 엔티티의 DataGrid를 채우면 어떤 결과가 나타날까요?
[StartDate = empty]

### 답변
StartDate가 채워지지 않은 모든 VacationRequest가 표시됩니다.

### 설명
이 XPath는 StartDate 속성이 비어 있는 객체를 찾습니다. 즉, 값이 설정되지 않은 경우입니다. 따라서 DataGrid는 StartDate 필드가 비어 있는 휴가 요청만 표시됩니다.
