# 학습 목표
이 모듈을 완료하면, 다음을 할 수 있습니다:
- 앱에 알림 모듈을 추가하고 보안 및 접근 권한을 설정합니다.
- 앱에서 알림을 생성, 승인, 거부하는 기능을 구축합니다.
- 앱에서 알림을 표시하는 기능을 구축합니다.

# 소개
## 1. 기본 기능 구축
- 이전에 했던 것처럼, 먼저 이 새로운 기능의 기본 사항인 도메인 모델과 기본 접근 권한을 구축하는 것에 집중하겠습니다.

### 1.1 알림 기능
알림은 일반 직원과 재무 직원에게만 필요하며, 관리자는 필요하지 않습니다. 관리자가 알림 기능을 사용할 수 없도록 쉽게 만들기 위해, 별도의 모듈로 추가할 것입니다.

### 1.2 도메인 모델
1. App Explorer에서 앱 이름을 마우스 오른쪽 버튼으로 클릭하고 **Add module…**을 선택하세요.![image](https://github.com/user-attachments/assets/4f408448-4a7a-4241-8cd4-ea0937caa221)
2. 모듈 이름을 **Notifications**로 설정합니다.
3. 도메인 모델이 자동으로 열립니다. **Notification** 엔터티를 추가하고 다음 속성을 추가하세요:
   - **Title** (String)
   - **Message** (String, 최대 길이 1000)
   - **Read** (Boolean)
   - **AssociatedObject** (Long)
4. **Store 'owner'** 체크박스를 선택합니다.![image](https://github.com/user-attachments/assets/c743ad4e-3a82-4d0a-bd59-ebebdc3ec8f9)
5. **Notification** 엔터티를 마우스 오른쪽 버튼으로 클릭하고, **Add > Association**을 선택하여 **Administration.Account** 엔터티와 * - * 연관 관계를 추가합니다.
6. **Expenses** 모듈의 도메인 모델을 엽니다.
7. **Request** 엔터티에 **RequestID**라는 새 속성을 추가합니다. 유형은 **AutoNumber**입니다.
   - **AssociatedObject** 속성은 **Request**와의 연결을 담당하며, 연관 관계를 생성하지 않고도 연결을 할 수 있게 해줍니다. 이를 통해 모듈을 독립적인 기능으로 다른 앱으로 내보내기 쉽게 만듭니다. 이 속성은 **RequestID**를 저장하고 연결을 조회하는 데 사용됩니다.

### 1.3 보안 및 접근 권한
1. **Notifications** 모듈의 보안 설정 창을 엽니다.
2. **User**와 **Approver**라는 두 개의 새 모듈 역할을 추가합니다.
3. **Notification** 엔터티와 **User** 모듈 역할에 대한 엔터티 접근 규칙을 추가합니다. 접근 규칙을 다음 이미지와 같이 구성하세요:
   - XPath 제약 조건 탭에서 **Path to user…** 버튼을 사용하여 사용자가 자신의 알림만 볼 수 있도록 XPath 제약 조건을 생성합니다. 버튼은 다음과 같은 XPath를 생성해야 합니다: `[Notifications.Notification_Account='[%CurrentUser%]']`![image](https://github.com/user-attachments/assets/dd6a17a3-a7dd-443c-9746-e1b738e2f850)
4. **Notification** 엔터티와 **Approver** 모듈 역할에 대한 엔터티 접근 규칙을 추가합니다. 접근 규칙을 다음 이미지와 같이 구성하세요:![image](https://github.com/user-attachments/assets/0be55407-f2e8-4377-bad8-850063fcb9bf)
5. **Expenses** 모듈의 보안 설정 창을 엽니다.
   - **Requestor**에게 **Request** 엔터티의 **RequestID** 속성에 대한 읽기 권한을 부여하세요.![image](https://github.com/user-attachments/assets/cca06672-cfe1-47a6-a5ee-43a1cfa2f359)
6. 앱 보안 설정 창을 엽니다.
   - **Requestor** 사용자 역할을 **Notifications** 모듈의 새로 생성된 **User** 모듈 역할에 연결합니다.
      - ![image](https://github.com/user-attachments/assets/ef9d5d52-b16b-41e0-8880-b63d148b9c96)
   - **Approver** 사용자 역할을 **Notifications** 모듈의 **Approver** 모듈 역할에 연결합니다.
      - 

# 사용자 정의 네비게이션 메뉴
- 주 네비게이션 트리가 아닌 네비게이션 메뉴를 표시하고 싶을 때는 **Menu document**를 사용하여 사용자 정의 네비게이션 메뉴를 만들 수 있습니다.
- **Menu document**는 메뉴 위젯에서 사용할 수 있는 네비게이션 메뉴를 정의합니다.
- 일반적으로 애플리케이션의 주요 메뉴는 기기 유형에 정의되며, **Menu document**는 사이드바와 같은 보조 메뉴에 사용됩니다.
- 메뉴는 메뉴 항목의 목록으로 구성되며, 선택적으로 하위 항목을 포함할 수 있습니다.
- 위젯에 따라 허용되는 레벨의 수가 다를 수 있습니다.
- 이 **Menu document**는 페이지나 네비게이션 레이아웃에서 원하는 곳에 표시할 수 있습니다.
- 네비게이션 항목을 만드는 방식은 기본 네비게이션 메뉴에서와 동일합니다.

# 알림 생성
## 1. 알림 생성 시나리오
알림이 생성되어야 하는 세 가지 시나리오가 있습니다:
1. 요청자가 요청을 생성할 때, 모든 승인자는 알림을 받아야 합니다.
2. 요청이 승인자에 의해 승인될 때, 요청을 생성한 요청자가 알림을 받아야 합니다.
3. 요청이 승인자에 의해 거절될 때, 요청을 생성한 요청자가 알림을 받아야 합니다. 이 경우, 승인자는 요청이 거절된 이유에 대한 메시지를 추가할 수 있어야 합니다.

## 2. 생성 알림
### 2.1 알림이 생성될 때(Creation Notification)
요청자가 요청을 완료하면 모든 승인자에게 알림이 발송되어야 합니다. 이를 통해 승인자들은 승인해야 할 새 요청이 있다는 사실을 알게 됩니다.
한 명의 승인자가 알림을 확인하면 다른 승인자들의 알림은 제거되어야 합니다.

### 2.2 생성 알림 만드는 방법
1. **Request_Wizard_Step3** 페이지를 엽니다.
2. **Finalize request** 버튼의 클릭 시 동작을 **Call a microflow**로 변경합니다.
3. 새 마이크로플로우를 생성합니다: **ACT_Request_Save**.
4. 요청자에게 마이크로플로우 접근 권한을 부여합니다.
5. 먼저, 저장 버튼의 기본 동작을 모방하여 객체를 커밋하고 페이지를 닫습니다.![image](https://github.com/user-attachments/assets/2c8d426a-61b9-45f0-98ae-201ff932062f)
6. 데이터베이스에서 모든 승인자를 검색합니다.(`[System.UserRoles/System.UserRole/Name = 'Approver']`)![image](https://github.com/user-attachments/assets/ff10af44-4d7c-49a7-b848-7c728477fe85) 
7. 데이터베이스에서 요청자를 검색하여, 메시지에서 그의 **FullName**을 사용할 수 있도록 합니다.(`[id=$Request/System.owner]
`)![image](https://github.com/user-attachments/assets/e917fe77-29a6-4786-8181-5d5c74976424)
8. 새 **Notification** 객체를 생성합니다. 객체는 다음 이미지처럼 구성합니다.
   - Title: 'Request created on' + formatDateTime($Request/createdDate,'MM/dd/yyyy')
   - AssociatedObject: $Request/RequestId
   - Notifications.Notification_Account: `$ApproverList`
   - Message: `$Requestor/FullName + 'created a new request;' + $Request/Title + '. Please check this request and approve or reject it.'`
   - ![image](https://github.com/user-attachments/assets/38006a3c-d203-4531-bc42-d02f8ab3d85b)

### 2.3 생성 알림 마이크로플로우
이제 마이크로플로우는 다음과 같은 모습일 것입니다:
![image](https://github.com/user-attachments/assets/38bc9193-6ba2-445e-9ada-dab43dfba23d)

## 3. 승인 알림
### 3.1 알림이 승인될 때
요청이 승인자에 의해 승인될 때, 요청을 생성한 요청자가 알림을 받아야 합니다.

### 3.2 승인 알림 만드는 방법
1. **ACT_Request_StatusApproved** 마이크로플로우를 엽니다.
2. 기존 활동들 전에 요청자를 검색합니다.
   - **TeamMember** 엔터티에 대한 **Retrieve** 활동을 추가합니다.
   - 범위를 **First**로 설정합니다.
   - 다음 XPath를 사용합니다: `[id = $Request/System.owner]`.
   - 출력 객체 이름을 **Requestor**로 설정합니다.
   - ![image](https://github.com/user-attachments/assets/217e92db-615d-424f-90c1-f80c77bdbb95)
3. 승인자를 검색합니다.
   - **TeamMember** 엔터티에 대한 **Retrieve** 활동을 추가합니다.
   - 범위를 **First**로 설정합니다.
   - 다음 XPath를 사용합니다: `[id = $currentUser]`.
   - 출력 객체 이름을 **Approver**로 설정합니다.
4. 새 **Notification** 객체를 생성합니다. 객체는 다음 이미지처럼 구성합니다.
![image](https://github.com/user-attachments/assets/ead3a24e-96f6-4a3a-9728-539a0bf73418)
- Title: `'you request has been approved.'`
- Message: `Dear'+$Requestor/FullName+', Your request: ' + $Request/Title + 
'has been rejected on ' + formatDateTime([%CurrentDateTime%],'MM/dd/yyyy')+
'by'+$Approver/FullName + ', for the following reason: '`
- AssociatedObject`$Request/RequestId`
- Notifications.Notification_Account: `$Requestor`

### 3.3 승인 알림 마이크로플로우
이제 마이크로플로우는 다음과 같은 모습일 것입니다:
![image](https://github.com/user-attachments/assets/395985f8-bcab-44ee-9f30-175f64443387)
![image](https://github.com/user-attachments/assets/d67793c6-0bd9-4d4d-8fcf-d5e33218fe54)
- 이때 주의해야 하는 것은 ObjectName을 잘 설정해서 써야 한다는 것이다. 안 그러면 변수로 인식이 안 된다. 

## 4. 거절 알림
### 4.1 알림이 거절될 때
요청이 승인자에 의해 거절될 때, 요청을 생성한 요청자가 알림을 받아야 합니다. 이 경우, 승인자는 요청이 거절된 이유를 설명하는 메시지를 추가할 수 있어야 합니다.
### 4.2 거절 알림 만드는 방법
1. **Act_Request_StatusRejected** 마이크로플로우를 엽니다.
2. 기존 활동 전에 요청자를 검색합니다.
   - **TeamMember** 엔터티에 대한 **Retrieve** 활동을 추가합니다.
   - 범위를 **First**로 설정합니다.
   - XPath를 다음과 같이 설정합니다: `[id = $Request/System.owner]`.
   - 출력 객체 이름을 **Requestor**로 설정합니다.
3. 승인자를 검색합니다.
   - **TeamMember** 엔터티에 대한 **Retrieve** 활동을 추가합니다.
   - 범위를 **First**로 설정합니다.
   - XPath를 다음과 같이 설정합니다: `[id = $currentUser]`.
   - 출력 객체 이름을 **Approver**로 설정합니다.
4. 새 **Notification** 객체를 생성합니다. 객체는 다음 이미지처럼 구성합니다.![image](https://github.com/user-attachments/assets/c30b3da4-9d9b-4b2d-a563-a943d864999d)
- Title: ''Your request has been rejected.''
- Message: `'Dear '+ $Requestor/FullName + ', Your request: ' 
+ $Request/Title + ' has been rejected on ' 
+ formatDateTime([%CurrentDateTime%],'MM/dd/yyyy') 
+ 'by' + $Approver/FullName + ', for the following reason: '`
- AssociatedObject: `$Request/RequestId`
- Notifications.Notification_Account: `$Requestor`
5. 마이크로플로우 끝에 **Show page** 활동을 추가합니다. 이 페이지에서 승인자는 알림에 사용자 정의 메시지를 추가할 수 있습니다.
6. 새 페이지를 생성합니다: **Notification_CustomizeRejectionMessage**.
   - 템플릿: **Form Vertical**
   - 레이아웃: **PopupLayout**
   - **NewNotification** 객체를 페이지에 전달합니다.

### 4.3 거절 알림 마이크로 플로우
이제 마이크로플로우는 다음과 같은 모습일 것입니다:


**Notification_CustomizeRejectionMessage** 페이지를 엽니다. 페이지를 구성하는 방법은 다음 이미지처럼 합니다:

# 알림 표시(Display Notifications)
이제 알림 시스템을 생성했으니, North Sea Shipbuilders Expenses 앱의 사용자들에게 알림을 실제로 표시하는 데 집중하겠습니다.

## 1. 알림 표시를 위한 필요 수행 작업
이를 위해 다음 작업을 수행해야 합니다:
1. **알림 개요 페이지**를 생성하여 상단 네비게이션 메뉴를 통해 접근할 수 있도록 합니다.
2. **사용자 정의 네비게이션 메뉴**를 생성하여 사용자가 읽지 않은 알림과 읽은 알림 간에 전환할 수 있도록 합니다.
3. 사용자가 알림을 읽은 것으로 표시하고, 알림을 삭제하며, 알림이 속한 요청으로 이동할 수 있는 버튼을 생성합니다.

## 2. 알림 페이지 만들기(Build the Notification Pages)
1. **Notifications** 모듈에 두 개의 폴더를 추가합니다: **Notifications**와 **Resources**.
2. **Notifications** 폴더에 두 개의 페이지를 추가합니다: **Notification_Overview_Unread**와 **Notification_Overview_Read**.
   - 네비게이션 레이아웃: **Atlas_Custom**
   - 템플릿: **Blank**
3. **Resources** 폴더를 마우스 오른쪽 버튼으로 클릭하고, **Menu (Add other > Menu)**를 추가하여 **Notifications**라고 이름을 지정합니다. 앞서 제시된 디자인을 참고하여 새로 생성된 메뉴에 두 개의 네비게이션 항목을 생성합니다.
4. **Notification_Overview_Unread** 페이지를 엽니다.
   - 페이지에 이미 있는 레이아웃 그리드 위젯에 추가 열을 추가합니다. 왼쪽 열의 너비는 3, 오른쪽 열의 너비는 9로 설정합니다.
   - 왼쪽 열에 **텍스트 위젯**을 추가하고, 캡션을 **Notifications**으로 설정합니다. 텍스트 스타일을 **Heading 3**으로 설정합니다.
   - 그 아래에 **Navigation tree** 위젯을 배치합니다.
     - 위젯을 두 번 클릭하여 속성을 엽니다.
     - **Menu source**를 **Menu document**로 설정합니다.
     - 앞서 생성한 **Notifications** 메뉴를 선택합니다.
   - 오른쪽 열에 **List view** 위젯을 배치합니다.
     - **Notification** 엔터티에 연결합니다.
     - 데이터 소스로 **XPath**를 선택하고, 다음 XPath를 설정합니다: `[Notifications.Notification_Account = ‘[%CurrentUser%]’] [not(Read)]`
     - 모델러가 리스트 뷰를 자동으로 채우지 않도록 설정합니다.
     - 리스트 뷰의 내용을 구성할 때, 다음 이미지를 참조합니다.
     - **Mark as read** 버튼은 새 마이크로플로우, **ACT_Notification_SetToRead**를 트리거합니다.
     - **Show request** 버튼은 새 마이크로플로우, **ACT_Notification_OpenAssociatedRequest**를 트리거합니다.
     - **Show request** 버튼에는 **Spacing right**을 **Outer small**로, **Spacing left**를 **Outer small**로 설정합니다.
     - **Delete** 버튼은 표준 삭제 동작을 수행합니다.
     - 모든 버튼을 포함하는 컨테이너의 **Align content**를 **Right align**으로 설정합니다.
     - **{Title}**의 스타일은 **Heading 4**입니다.
     - 검색 필드를 활성화하려면 구조 모드로 전환하고, 리스트 뷰에서 **Search on**을 두 번 클릭합니다. **Attribute paths**에 **Title**, **Message**, **AssociatedObject**를 추가합니다.
5. 이제 **Notification_Overview_Read** 페이지를 엽니다.
   - 5번에서 9번까지의 단계를 반복하여 이 페이지를 구축합니다. 단, 버튼은 제외합니다. 두 번째 XPath 제약 조건은 **not(Read)** 대신 **Read**로 설정합니다.
  
## 3. 네비게이션 메뉴 확장(Extend the Navigation Menu)
이제 사용자들이 자신의 알림에 접근할 수 있도록 해봅시다.
### 3.1 네비게이션 메뉴 확장 방법
1. **Navigation menu**를 엽니다.
2. 새 네비게이션 항목을 추가합니다: **Notifications**.
   - 아이콘으로 **bell**을 사용합니다.
   - 이 네비게이션 항목이 **Notification_Overview_Unread** 페이지를 열도록 설정합니다.

## 4. 마이크로플로우 구축(Build the Microflows)
### 4.1 마이크로플로우 생성
1. **ACT_Notification_SetToRead** 마이크로플로우를 엽니다.
   - **Read** 속성의 값을 **true**로 변경합니다.
   - 객체를 커밋하고 클라이언트를 새로 고칩니다.
2. **ACT_Notification_OpenAssociatedRequest** 마이크로플로우를 엽니다.
   - 다음 XPath를 사용하여 데이터베이스에서 연결된 요청을 검색합니다: `[RequestID = $Notification/AssociatedObject]`.
   - **Show page** 활동을 추가하여 **Request_Details_Approver** 페이지를 열고 요청 객체를 전달합니다.

## 5. 보안 업데이트
보안을 업데이트하고 모든 새로운 기능을 테스트해봅시다.
### 5.1 보안 기능 설정하기
1. **User**에게 모든 새로운 페이지와 마이크로플로우에 대한 접근 권한을 부여합니다.

# 퀴즈
# 문제 및 정답 해설

## Question 1:
### Which of the following options provides an easy way to limit access rights for a given role to a specific functionality within an app?
- **By adding a separate module.**
- By creating a package.
- By creating a snippet.
- By creating a separate domain model.

**해석:** 
앱 내에서 특정 기능에 대한 역할의 접근 권한을 제한하는 가장 쉬운 방법은 무엇인가?

**정답 해설:**
- 정답은 **"By adding a separate module"**입니다. 별도의 모듈을 추가하면 특정 기능에 대한 접근 권한을 간단하게 관리할 수 있습니다. 모듈별로 보안 설정을 적용할 수 있기 때문에, 특정 역할에 대해 필요한 기능만 노출하도록 쉽게 제한할 수 있습니다.

## Question 2:
### Where on the page can the Menu document be displayed in an app?
- Only on a page
- Only inside of a menu widget
- Only in a navigation layout
- **Anywhere**

**해석:**
앱에서 메뉴 문서를 페이지의 어디에 표시할 수 있는가?

**정답 해설:**
- 정답은 **"Anywhere"**입니다. 메뉴 문서는 페이지나 네비게이션 레이아웃, 메뉴 위젯 등 앱 내 어디에나 배치하여 사용할 수 있습니다.

## Question 3:
### What alternative to drawing an association between two entities can you use to connect two entities, each located in a separate domain model?
- By setting the 'Specialization' setting of one entity to the other.
- **By right-clicking in an entity and selecting Add>Association.**
- By copying entities from one domain model to another.
- By writing Java code.

**해석:**
두 개의 도메인 모델에 위치한 두 엔티티를 연결하기 위한 연관 관계 설정의 대안은 무엇인가?

**정답 해설:**
- 서로 다른 도메인 모델에 위치한 엔티티를 가장 직접적이고 효율적으로 연결하는 방법은 우클릭 후 Add>Association을 선택하는 것입니다.


## Question 4:
### Which of the following XPath constraints should be used to allow users to only see their own notifications?
- [Notifications.Notification_Account=System.User']
- Notifications.Notification_Account='[%CurrentSession%]'
- **[Notifications.Notification_Account='[%CurrentUser%]']**
- Notifications.Notification_Account=ID'

**해석:**
사용자가 자신의 알림만 볼 수 있도록 하기 위해 사용해야 하는 XPath 제약 조건은 무엇인가?

**정답 해설:**
- 정답은 **"[Notifications.Notification_Account='[%CurrentUser%]']"**입니다. 이 제약 조건은 현재 로그인한 사용자의 알림만 표시하도록 제한합니다. `%CurrentUser%`는 현재 사용자의 식별자입니다.

## Question 5:
### What can you use whenever you wish to display a navigation menu, but not the main navigation tree?
- External icons
- Javascript
- **Menu**
- Modules from the App Store

**해석:**
메인 네비게이션 트리가 아닌 네비게이션 메뉴를 표시하고 싶을 때 사용할 수 있는 것은 무엇인가?

**정답 해설:**
- 정답은 **"Menu"**입니다. 메뉴 문서를 사용하여 메인 네비게이션 트리가 아닌 사용자 정의 네비게이션 메뉴를 표시할 수 있습니다.

### Navigation Tree와 Menu의 차이
Navigation Tree와 Menu는 둘 다 사용자가 애플리케이션 내에서 페이지 간 이동을 할 수 있게 돕는 기능이지만, 사용 목적과 활용 방식에서 차이가 있습니다.

1. Navigation Tree
용도: 애플리케이션의 전체적인 네비게이션을 구성합니다. 일반적으로 메인 네비게이션으로 사용되며, 앱의 전반적인 페이지 구조를 나타냅니다.
위치: 대개 애플리케이션의 사이드바 또는 헤더에 배치되며, 사용자가 주요 페이지들을 쉽게 탐색할 수 있게 해줍니다.
구조: 트리 구조로 되어 있어, 상위 메뉴 아래에 여러 하위 메뉴를 배치할 수 있습니다. 여러 단계로 나뉘어 있어 계층적인 페이지 구조를 만들기 용이합니다.
사용 예: 사이드바에 있는 여러 메뉴 항목들(대시보드, 요청 관리, 사용자 프로필 등)을 트리 형식으로 표현해, 사용자가 클릭하면 해당 페이지로 이동하게 합니다.

2. Menu Document
용도: 특정 컨텍스트에서만 사용되는 보조 메뉴를 만들기 위한 기능입니다. Navigation Tree처럼 전체 앱을 네비게이트하는 것이 아니라, 특정 페이지나 레이아웃에서 특정 기능만을 위한 간단한 메뉴를 제공합니다.
위치: 페이지 어디에서든 사용자가 원하는 곳에 배치할 수 있습니다. 예를 들어, 페이지 내 특정 섹션에서 보조적인 메뉴를 제공할 때 활용할 수 있습니다.
구조: 하위 메뉴를 가질 수 있지만, Navigation Tree보다는 단순한 구조를 가집니다. 주로 클릭 이벤트에 반응하는 몇 가지 버튼들로 구성될 수 있습니다.
사용 예: 사용자가 특정 알림을 확인할 수 있는 메뉴를 제공하거나, 특정 기능(예: 읽음 처리, 삭제)만을 위한 작은 네비게이션 메뉴를 페이지의 한쪽에 배치할 때 사용합니다.

#### 차이점 요약
Navigation Tree는 앱의 전반적인 네비게이션을 담당하며, 계층적이고 복잡한 구조로 애플리케이션 전체를 탐색할 수 있게 해주는 반면, Menu Document는 특정 기능을 수행하거나 보조적인 역할을 하는 간단한 메뉴입니다.
Navigation Tree는 주로 메인 네비게이션으로 사용되고, Menu Document는 특정 페이지나 영역에서 보조적인 역할을 담당합니다.

#### 문제 5번에 대한 설명
정답: Menu
이유: Menu는 사용자가 애플리케이션의 주 네비게이션 트리를 제외한 특정 컨텍스트에서 사용할 수 있는 네비게이션 항목을 정의할 수 있는 문서입니다. Menu는 특정 위젯에 연결되어 페이지 내 어디에서든 나타날 수 있지만, Navigation Tree는 일반적으로 앱 전체의 탐색을 돕기 위한 구조적 메뉴입니다.
