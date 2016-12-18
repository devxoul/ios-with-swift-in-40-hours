## 새 프로젝트 시작하기

우선, [1강에서 했던 것처럼](../Chapter-1/ios-project.html) Xcode에서 새로운 iOS 프로젝트를 생성해봅시다. Product Name에는 'Todobox'를 쓰고, Swift 언어를 선택한 뒤 다음을 눌러 프로젝트가 저장될 디렉토리를 설정합니다.

![new-project](../images/Chapter-4/new-project.png)

### 배포 타겟 설정하기

Xcode에서 프로젝트가 열리면, 가장 먼저 화면 왼쪽에 있는 프로젝트 네비게이터<sup>Project Navigator</sup>에서 'Todobox'라는 프로젝트를 선택해봅시다. 그리고 나오는 화면에서 Project 아래에 있는 Todobox를 선택하여 Deployment Target을 8.0으로 변경합니다. 기본값으로는 Xcode에서 지원하는 가장 최신 버전의 iOS가 선택되어 있는데, 우리는 iOS 9 이상을 지원하도록 합니다.

![deployment-target](../images/Chapter-4/deployment-target.png)

이제 가장 기본적인 프로젝트 환경은 끝났습니다. 이제부터는 사용자가 실제로 사용할 수 있는 UI를 만들어 봅시다.
