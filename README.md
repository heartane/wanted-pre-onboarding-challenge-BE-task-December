## 1-1) 사전과제 진행 가이드

- 아래 총 5 문제에 대한 해설을 작성한 뒤 Pull Request를 날려주세요.
- 문제 해설에 대한 정해진 양식은 없으며, 최대한 자세히 해설해주시면 좋습니다.
- 문제 유형은 해당 코스에서 다룰 주제들을 포함하고 있으니 완벽히 이해하시면 코스를 수강하는데 큰 도움이 될 것입니다.

\*_문의 사항은 사전 과제 Repository의 Issue로 등록해 주세요._

## 1-2) 사전 과제

- (1) 동기와 비동기 프로그래밍에 대한 차이점을 설명해주세요.

  동기는 작업 간의 연속성이 중요합니다. 현재 처리하는 작업의 마무리와 다음 작업의 시작이 동시에 일어나야 합니다. 이는 현재 처리되는 작업이 끝나지 않는다면 다음 작업으로 넘어갈 수 없음을 뜻합니다. 순차적으로 처리해 나가기에 매우 직관적이고 명료한 방법이지만, 무거운 작업을 처리한다면 그동안 대기가 발생해 비용이 낭비되면서 결국 사용자에 영향을 미치게됩니다.

  비동기는 이러한 동기의 병목현상을 해결하기 위해 동기가 반드시 지키는 이 동시성, 연속성에서 벗어나 즉각적인 결과를 보기 어려운 작업의 경우 그에 대한 해결을 다른 협력 함수(핸들러)에 위임하고 다음 작업을 진행시키는 방법입니다. 해당 작업의 진행 상태를 계속해서 주시해야 하는 동기와는 달리 비동기는 진행 후 그 결과를 알아서 반환하기 때문에 보다 효율적인 처리가 가능합니다.

- (2) 블로킹과 논블로킹의 차이점을 설명해주세요.

  이는 제어권을 돌려받는 시점의 차이입니다. A 함수가 특정 작업을 위해 B 함수를 호출했을 때, 블로킹 방식은 B 함수가 전달받은 제어권을 작업이 종료됨과 함께 돌려주면서 A 함수는 그때까지 코드 실행 권리가 없어 함수 실행에 멈춤이 발생하게됩니다. 반면 논블로킹 방식은 B 함수가 전달받은 제어권을 받는 즉시 바로 반환하기에 A 함수는 B 함수의 작업 진행 중과 상관없이 다른 작업을 진행할 수 있습니다.

- (3) 본인이 주로 사용하는 언어에서 비동기 프로그래밍을 사용하는 방법을 설명해주세요.

  자바스크립트 엔진의 콜스텍은 싱글 스레드로, 쌓인 실행 컨텍스트를 순차적으로 처리해야 하는 중대한 역할을 가졌기 때문에 비동기 작업은 이벤트 루프에 위임하며 다음 컨텍스트를 논블로킹적으로 처리합니다. 이벤트 루프는 이벤트 큐에 들어온 비동기 작업을 적절하게 백그라운드 스레드 풀에 할당하며, 완료된 결과를 테스크 큐에 대기시키다 콜스텍이 비었을 때 전달합니다.

  여기서 이벤트 루프 내부의 백그라운드 스레드 풀은 블로킹적으로 처리함을 주의해야 합니다. 그렇기에 비동기 작업 내부가 무거운 동기적인 작업으로 지연이 일어날 경우 비동기 처리에 영향을 주기 때문에 제대로 된 비동기를 위해서는 내부 작업의 구성 또한 신경써야 합니다.

- (4) 메세지 큐를 쓰는 이유에 대하여 2가지 예시를 서술해주세요.

  서버 성능 효율을 위해 일괄 처리를 원하는 경우 메세지 큐를 사용할 수 있습니다. 특히 즉시 반영되어 응답으로 필요한 것이 아닌 데이터의 경우, 지정 규모까지 데이터를 모아 한번에 삽입할 수 있습니다.

  또한 트래픽이 급작스럽게 증가했을 때 데이터를 안정적으로 유지하면서 처리할 수 있도록 메세지 큐를 사용합니다.

- (5) 본인이 작성한 서버 코드가 있는 github repo 주소를 제출해주세요. (CRUD 기능을 모두 포함하여야 하며, 서버에 대한 설명을 README에 작성해주시면 더욱 좋습니다.)
  [https://github.com/heartane/Lumiere-backend]

  신입 및 아마추어 작가들의 캔버스 작품을 판매하는 이커머스 서비스를 위한 Node.js 기반의 API 서버입니다.

  보다 간편한 로그인을 위해 OAuth 2.0 프로토콜을 이용해 네이버, 카카오, 구글 소셜 로그인을 구현하였으며, 인증에는 JWT 토큰을 사용해 유저와 관리자 권한을 분리하였습니다. 유저, 상품, 작가, 주문 등의 도메인에 CRUD 기능을 구현하였고 결제의 경우 아임포트를 통해 테스트 결제가 가능하도록 만들었습니다.

  이후 백엔드 개발자에게 중요한 주제는 무엇일까 고민하고 찾아보며 한 차례 리팩토링을 진행하였습니다. 안정적이고 지속 가능한 서버 환경에 초점을 두고 여러 부분에 적용 연습을 해보았습니다.

- (6 - Optional) 해당 수업을 통해 꼭 배우고 싶은 주제 또는 지식이 있다면 자유롭게 서술해주세요.

  단순히 요청을 받아 그에 맞는 데이터를 조합해 응답을 주는 API 서버를 넘어, "안정적이고 지속 가능한 환경"이라는 넓고도 넓은 주제를 공부하면서 CI/CD의 중요성을 느끼게 되었습니다.

  또 기존 서버를 배포했던 AWS 계정의 프리티어 서비스가 종료되는 상황을 통해 쉽게 마이그레이션할 수 있는 컨테이너 환경의 필요성을 깨닫기도 하고 배포 자동화 연습을 하면서 자체 관리보다 인프라 아키텍처 관리를 위임할 수 있는 여러 관리형 서비스를 접하면서 클라우드 서비스에 관심을 갖게 되었습니다.

  그래서 이번 원티드 프리온보딩 벡엔드 챌린지 수업을 통해 실무에서 필요한 AWS 인프라 도구들에 대해, 특히 AWS Lambda에 대해 배워보고 싶습니다. 또한 MSA를 통해 작은 단위 서버를 쪼개 배포함으로 이들의 원할한 협력을 위해 필요한 메세지큐에 대해서도 접하고 싶으며, SDK와 CLI로 AWS와 상호작용하는 방법에 대해서도 배워보고 싶습니다.
