# XPath 기초(XPath Basics)
## XPath를 사용하는 이유
### 1. 정의
- XPath는 Mendix가 데이터와 상호 작용할 때 **도메인 모델을 탐색하는 데 사용하는 언어**입니다.
- XPaths는 개발자에게 보고자 하는 특정 **데이터를 얻는 방법을 제공**합니다.
- 모든 데이터를 한 번에 화면에 표시하는 대신, XPaths는 엔터티, 속성, 연관 관계 및 변수를 사용하여 **데이터를 제약할 수 있는 방법을 제공**합니다.
### 2 예시
예를 들어, 사용자가 웹사이트에서 제품을 주문한 경우, XPath를 사용하여 Mendix 데이터베이스에 접근하고 사용자의 주문 및 주문한 제품에 대한 정보를 검색할 수 있습니다. 이렇게 하면 Mendix 페이지에서 이러한 특정 제품 목록을 표시할 수 있습니다.

### 3. XPath 사용 이유
- XPath는 데이터 속성 간의 관계를 명시하는 작성된 구문입니다.
- Mendix는 SQL 또는 OQL과 같은 유사한 구문 대신 XPath를 사용하는데, 이는 데이터베이스의 보편성과 사용의 용이성 때문입니다.
- XPath는 도메인 모델의 연관 및 속성 구조와 원활하게 맞물리며, 쿼리를 한눈에 이해할 수 있게 합니다.
- 지능형 애플리케이션은 신중한 데이터 표현을 필요로 합니다. **결과적으로 XPaths는 거의 모든 Mendix 애플리케이션에서 사용됩니다.**

## XPath는 어디에 사용할까요?
XPath는 Mendix 플랫폼 전반에서 데이터베이스의 데이터 흐름을 제어하는 데 사용됩니다. 데이터베이스에서 데이터를 검색하는 거의 모든 위치에서 XPath 쿼리를 활용할 수 있습니다. 대부분의 경우, XPath는 "XPath Constraint"라는 레이블이 붙은 창에 작성됩니다.

### 1. 페이지에서의 XPath(XPaths on Pages)
- 데이터 그리드 및 목록 보기의 제약 조건: `데이터 그리드(Data Grids)`와 `목록 보기(List Views)`와 같은 목록 위젯에서 **어떤 항목이 표시될지를 정의**할 수 있습니다.

#### 1.1 참고: 
- Studio Pro에서 기본적으로는 Structure Mode가 설정되어 있을 수 있습니다. 이 과정 및 모든 스크린샷은 Design mode에서 보여집니다.
![image](https://github.com/user-attachments/assets/e7e6db75-0282-4716-a73c-042131a8f79f)

#### 1.2 참조 선택기에서의 제약 조건: 
- 참조 선택기(Reference Selector)에서 사용자가 볼 수 있는 선택 가능한 객체를 정의할 수 있습니다.
  - 예를 들어, 'Order'에서 'Product'를 선택할 때 참조 선택기를 사용하여 특정 제품만 목록에 나타나도록 XPath 제약 조건을 설정할 수 있습니다.

### 2. 마이크로플로우에서의 XPath (XPaths in Microflows)
- 'Retrieve' 액션: 마이크로플로우(Microflows)에서 'Retrieve' 액션을 사용하여 데이터베이스에서 반환되는 데이터를 정의하는 데 사용됩니다.

### 3. 보안에서의 XPath (XPaths in Security)
- 엔티티 접근 규칙: 도메인 모델 보안 설정에서 엔티티 접근 규칙(Entity access rules)에 XPath 제약 조건을 추가할 수 있습니다.

## XPath 구조화 방법
### 1. XPath 사용 가능 위치
- 이전 강의에서 Mendix에서 XPath를 사용할 수 있는 위치에 대해 배웠습니다. 이번 강의에서는 XPath를 구성하는 요소들에 대해 배우게 됩니다.
- XPath 사용 가능 위치
  - 페이지
  - 마이크로 플로우
  - 보안(security)

### 2. XPath 구문(XPath Syntax)
- XPath 문은 Mendix 런타임에 의해 올바르게 해석되기 위해 따라야 하는 특정 구문(syntax)을 따릅니다.
- XPath는 도메인 모델을 직접 참조하며, 엔티티(Entities), 속성(Attributes), 연관 관계(Associations)를 직접 참조할 수 있습니다.
![image](https://github.com/user-attachments/assets/1000dd2b-62fc-40c5-849d-3d4443df1591)

### 3. XPath의 제약 조건(XPath constraints)
- XPath 제약 조건(XPath constraints)은 다음과 같은 구조적 요소, 즉 토큰(tokens)을 특징으로 합니다:
![image](https://github.com/user-attachments/assets/0015a1a1-d4ab-4981-9bf2-c8d01da659c7)

## 멘딕스가 어떻게 도움이 될수 있을까? (How Can Mendix Help You?)
Mendix 플랫폼은 XPath 제약 조건을 구성할 때 자동 완성(auto-completion) 옵션을 통해 도움을 줄 수 있습니다. 열린 괄호 [ 또는 슬래시 /를 입력하면 자동 완성 기능이 자동으로 열립니다. 또한, 자동 완성을 잃어버리거나 다른 곳을 클릭하여 자동 완성이 사라졌을 때는 CTRL+Space를 눌러 자동 완성 기능에 접근할 수 있습니다.

XPath 제약 조건을 만들 때 기억해야 할 사항은 다음과 같습니다:
1. 도메인 모델에서 검색할 엔티티를 식별합니다.
2. 해당 엔티티에서 데이터 제약에 사용할 속성(attributes) 및/또는 연관 관계(associations)까지의 경로를 식별합니다.
3. 위의 빌딩 블록을 사용하여 XPath 표현식을 구성합니다.

생활을 좀 더 쉽게 하기 위한 팁:
1. 도메인 모델을 숙지하세요. 도메인 모델 구조에 익숙하지 않으면 올바른 경로를 선택하기 어려울 수 있습니다.
2. 도메인 모델을 잘 정리하세요. 엔티티, 연관 관계, 속성을 이해하는 것이 쉽고 읽기 좋은 XPath 구성을 위한 핵심입니다.
    - 엔티티와 속성 이름은 그들이 나타내는 것을 설명해야 하며 기술적인 이름을 사용하지 않아야 합니다.
    - 엔티티는 단수형으로 이름을 지으세요. 예를 들어, Customer 대신 Customers를 사용하세요.
    - 여러 연관 관계가 같은 엔티티 간에 있을 때는 연관 관계 이름을 고유하게 만드세요. 예를 들어, VacationRequest_Account와 VacationRequest_Account_2는 연관 관계의 차이를 설명하지 않습니다. VacationRequest_Submitter와 VacationRequest_Approver는 XPath를 읽을 때 한눈에 차이를 알 수 있습니다.
3. 도메인 모델과 XPath 편집기를 화면 양쪽에 나란히 두면 올바른 경로를 찾는 데 도움이 됩니다.






