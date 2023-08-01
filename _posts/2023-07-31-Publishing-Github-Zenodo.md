---
layout: post
title: Zenodo로 Github repository doi 발급하고 참조 및 인용하기
subtitle: Github와 Zenodo 연동을 통해 doi 발급하고 release 하기.
categories: misc
tags: [Github, Zenodo, doi]
---

### 왜 이걸 하게 되었는가?

논문 작업을 하다보면 Github repository를 인용해야 할 때가 있다. 그러면 Github repository의 주소를 그대로 올릴 수 있다. 그런데 변하지 않는 doi를 발급해서 doi 주소를 인용하도록 되어 있는 경우가 있다. 다른 사람이 만든 라이브러리면 그들이 원하는 인용 방식을 취하면 되겠지만 내가 연구하면서 짠 코드를 공유하고 싶다면 doi를 내가 직접 발급받아야 한다. 이런 아카이브들로는 mendeley나 Zenodo가 있는데 이 포스트에서는 Zenodo로 하는 법을 기술한다. 

## Github repository의 Zenodo doi 발급 법

결론부터 말하면 다음 링크를 따라하면 된다.
[Github archiving link](https://docs.github.com/ko/repositories/archiving-a-github-repository/referencing-and-citing-content)

우선, 내 Github repository가 public인지를 확인하자. Setting 탭으로 가서 스크롤 내리면 visibility를 확인할 수 있다.
![Check-visibility.png](/assets/images/posts/2023-07-31/Check-visibility.png)
여기서 private repository를 public으로 전환한 뒤에 모든 작업을 수행하자.

모든 예시는 pyGOSH 코드를 대상으로 예시를 보여준다. 우선 Zenodo 로그인페이지로 간다.
![Zenodo-login.png](/assets/images/posts/2023-07-31/Zenodo-login.png)
그럼 다음 링크로 인도되며 아래 그림처럼 보인다. 이걸 따라하면 된다.
[Zenodo github setting link](https://zenodo.org/account/settings/github/)
![Zenodo-procedures.png](/assets/images/posts/2023-07-31/Zenodo-procedures.png)
가능한 repository 목록에서 Zenodo에 등록하고자 하는 부분 옆의 버턴을 누르면 된다고 한다. 그런데 목록에 내가 원하는 repository가 안 보인다. 
![Zenodo-repositories-1.png](/assets/images/posts/2023-07-31/Zenodo-repositories-1.png)
그러면 위에 sync 버튼을 누르자.
![Zenodo-procedures-sync1.png](/assets/images/posts/2023-07-31/Zenodo-procedures-sync1.png)
그럼 뿅하고 아래 리포지토리가 나온다 그러면 off 스위치를 눌러서 on으로 만들어주자.(그래도 안 나오면 release를 먼저 추가하고 시도해보자.)
![Zenodo-procedures-sync2.png](/assets/images/posts/2023-07-31/Zenodo-procedures-sync2.png)
여기까지 오면 다 된 것이다. 이렇게 Zenodo 싱크가 되면 release가 업데이트될때마다 Zenodo가 알아서 이를 갱신해준다.
On으로 버튼을 바꾸고 새로고침 한 다음에 해당 리포지토리 버튼을 누르면 이렇게 Get started! 라고 나오면서 release를 만들라고 한다. 
![Zenodo-get-started.png](/assets/images/posts/2023-07-31/Zenodo-get-started.png)
가면 release를 만들 수 있는 창이 나온다. 
![Publish-release.png](/assets/images/posts/2023-07-31/Publish-release.png)
또는 repository 페이지에서 'Release' 탭의 'Create a new release'를 누르면 된다.
![Releases-1.png](/assets/images/posts/2023-07-31/Releases-1.png)
해당되는 release 제목과 내용을 넣는다. 무엇보다 위에 tag에서 v1.0.0같이 release 태그를 적어주어야 한다. Release를 publish하면 아래와 같이 된다.
![Publish-release2.png](/assets/images/posts/2023-07-31/Publish-release2.png)
Release를 만들고 Zenodo를 가면 바로 doi가 자동으로 생성된다.
![Zenodo-generated-doi.png](/assets/images/posts/2023-07-31/Zenodo-generated-doi.png)
이를 활용해 Github에도 doi를 업데이트할 수 있고 참조 및 인용할 수 있다.

