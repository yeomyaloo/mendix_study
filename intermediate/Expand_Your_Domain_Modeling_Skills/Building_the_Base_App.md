# 학습목표
- 엔티티 간의 연관성 검토
- 도메인 모델 구축
- 팀 페이지 구축 및 연결

# 앱 만들기
이 학습 경로는 Studio Pro 10.0.0을 사용하며, 동일한 버전을 사용하여 앱을 구축할 것을 권장합니다.
- 좋은 앱 이름을 생각해 봅시다. "Soccer Squad"는 어떨까요?
- 새로운 앱을 생성하세요. Mendix Portal 또는 Mendix Studio Pro에서 직접 생성할 수 있습니다. Mendix Portal에서 생성할 경우 올바른 템플릿을 선택해야 합니다.
- 빈 스타터 앱(Blank starter app)을 선택하세요. 이 앱은 처음부터 끝까지 구축할 것입니다.
- 새로 생성한 앱을 Mendix Studio Pro에서 엽니다.
- 작업한 내용을 Summary 강의의 리소스 섹션에 있는 솔루션 앱과 비교해 볼 수 있습니다.

# 엔티티 간 다중 연관
새로운 이론에 들어가기 전에, Rapid Developer 학습 경로에서 배운 내용을 요약해 보겠습니다.
### Mendix에서의 Association(3가지)
Mendix에는 세 가지 유형의 연관이 있습니다. 이러한 연관은 객체 간의 가능한 연결을 생성할 수 있도록 해줍니다. 이러한 연결은 참조(reference)라고도 불립니다. Mendix 플랫폼의 연관 유형은 다음과 같습니다:
- 일대다 (1 - *)
- 일대일 (1 - 1)
- 다대다 (* - *)

### Rapid에서의 연관관계
- Rapid Developer 학습 경로에서는 엔티티 간에 단일 연관을 사용했습니다.
- 두 엔티티 간에는 항상 하나의 연관만 존재했습니다. 예를 들어: 교사(Teacher)와 교육 이벤트(Training Event) 간의 단일 일대다 연관입니다.

### 다중 연관관계 
- 하지만 두 엔티티 간에 다중 연관을 추가하는 것도 가능합니다.
- 이렇게 하는 가장 중요한 이유는 엔티티 인스턴스 간에 서로 다른 관계를 가질 수 있기 때문입니다.
  - 예를 들어, 회사는 고객에 대해 두 개의 주소: 하나의 배송지 주소와 하나의 청구지 주소를 저장하고 싶어할 수 있습니다.

### 다중 연관관계가 필요한 이유
회사는 앱에서 모든 고객을 표시하는 데이터 그리드를 보고, 해당 데이터 그리드에서 두 주소를 즉시 보여주고 싶어합니다. 이는 고객(Customer)과 주소(Address) 간에 일대다 연관을 사용하여 주소 유형을 열거하는 경우 불가능합니다. 여러 개의 일대일 연관을 사용하면 데이터 그리드에서 두 주소를 직접 출력할 수 있습니다.

일대다 연관과 여러 개의 일대일 연관을 사용하는 것은 최종 사용자가 특정 연결을 설정하는 방식에도 영향을 미칩니다.

### 결론
결국, 어떤 것을 선택할지는 대부분 최종 사용자가 앱의 프론트 엔드에서 데이터를 어떻게 보고 조작하길 원하는지에 달려 있습니다.

# 선수와 주장(Players and Captains)
이제 두 엔티티 간에 다중 연관을 추가할 수 있는 가능성에 대해 알았으니, 이것이 Adrian과 Soccer Squad 앱에 어떻게 도움이 되는지 살펴보겠습니다.

상상해 보세요: 축구 팀은 여러 명의 선수를 가질 수 있습니다(사실, 최소 11명이 필요합니다). 이는 일대다 연관의 완벽한 예입니다. 하지만 각 팀은 단 한 명의 주장만 가질 수 있으며, 이 주장도 선수입니다.

이를 해결하기 위해 Player 엔티티에 Boolean 속성인 Captain을 추가할 수 있습니다. 이렇게 하면 선수를 생성하거나 수정할 때마다 이 선수가 주자인지 아닌지 묻는 입력 위젯이 표시됩니다.
![image](https://github.com/user-attachments/assets/e177c4f9-67c7-491c-b0f2-6e977d7fa52c)

아마도 이 솔루션이 괜찮다고 생각할 수도 있지만, Team과 Player 엔티티 간에 두 개의 연관을 사용하는 더 나은 솔루션을 살펴보겠습니다.
![image](https://github.com/user-attachments/assets/2b33af67-f5ce-4d7d-a2a3-553db8c9dc38)

이 도메인 모델 구조를 사용하면 팀에 많은 선수를 추가하고 그 중 한 선수를 주장으로 선택할 수 있습니다. 두 번째 연관은 일대일 연관이기 때문에 주장을 오직 하나만 가질 수 있도록 즉시 강제합니다. 이로 인해 이를 강제하는 맞춤 로직을 만들 필요가 없어집니다!

Soccer Squad 앱에서 두 엔티티 간의 다중 연관을 적용할 수 있는 또 다른 예는 Match와 Team 간의 연관입니다. 경기는 홈팀과 원정팀, 두 팀이 참여합니다. Mendix에는 일대이(One-to-Two) 연관이 없습니다. 그리고 단순히 다대다(Many-to-Many) 연관을 사용하면 홈팀이 누구인지 저장할 수 없습니다.
![image](https://github.com/user-attachments/assets/5b8b680c-23a3-455a-aade-b7ef19a8fbcf)

이 문제를 해결하기 위해 Rapid Developer 학습 경로에서 논의한 정보 엔티티 패턴을 사용할 수 있습니다. 하지만 이 솔루션은 데이터베이스에 세 개의 테이블을 추가하고, 경기에 두 팀만 추가할 수 있도록 강제하는 맞춤 로직을 만들어야 합니다. 또한 이 엔티티의 이름은 무엇이 될까요? MatchRole? MatchTeamType? 이 솔루션은 시작하기 전에 이미 불명확하므로, 애플리케이션 개발에서는 좋은 일이 아닙니다!

대신, Match와 Team 엔티티 간에 두 개의 연관을 사용할 수 있습니다. 하나는 Match_TeamHome, 다른 하나는 Match_TeamAway입니다. 이렇게 하면 경기에 두 팀만 선택할 수 있도록 자동으로 강제됩니다. 이는 데이터베이스에 두 개의 간단한 테이블만 추가하며, 이름도 매우 명확합니다. 이 솔루션이 승자가 될 것 같습니다(말장난이었습니다)!
![image](https://github.com/user-attachments/assets/82c2863e-de39-46cd-bb02-e5cbe1f55a23)
## 1. 
