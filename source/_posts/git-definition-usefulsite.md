---
title: Git 개념 및 유용한 사이트
categories:
  - DevEnv
  - Git
tags:
  - GitHub
  - Git
  - DevOps
date: 2016-06-24 21:10:09
thumbnail: http://cfile10.uf.tistory.com/image/2212E8385758B1FC2DAD37
---

## 서론

안녕하세요. 새로입니다. 오늘은 오픈소스 저장소로 유명한 Git에 대해서 알아보는 시간이 되겠습니다. 이번 토픽을 Git으로 선정하게 된 이유는, 몇일전 회사에서 신규서비스 오픈 중 개고생을 했기때문인데요. 머지와 리베이스 그 지옥에서 벗어나기 위해 발버둥 첬던 밤샘작업. 그 뼈아픈 경험때문에 이번 기회에 git의 필요한 부분을 정리하기로 마음먹었습니다. 포스팅 주제와 관련된 필자의 수준은 다음과 같습니다.(2016-06-06) <br/>
**능력 평가는 지극히 주관적임을 먼저 밝힙니다.**
* SVN(형상관리툴) 사용경험 없음.  
* 참여한 모든 프로젝트에서 Git을 사용했었음 동료에게 피해주지 않을 만큼 정도의 Git사용 실력(가장 중요한 부분!!!)

Ps. 누군가 싼 똥은 다른 사람에게 전파된다.....

## Git 개념

먼저 시작하기전에 Git의 기본 개념에 대해 알고 넘어가야겠G요. Git이란 버전관리 시스템으로 쉽게 이해하면 소스코드의 백업공간입니다. 보고서나 어떤 문서를 작성할때 원본파일을 복사하여 복사본을 만들고 수정하셨던 경험이 있을 것입니다. 하지만 파일을 편집할 때 마다 복사본을 만드는 것은 우리모두의 치명적 약점. 언제나 실수 할 수 있다는 점을 생각했을 때 좋지 못한 방법입니다. 그리고 더욱 치명적인 것은 그 작업을 여러명이 진행할 때 실수 확률은 훨씬 더 클것입니다. 언제나 그랬듯이 우리는 우리의 약점을 보완하기 위한 도구를 만들게 됩니다. 그것이 바로 Git과 같은 버전관리 시스템입니다.

## Git에 대한 수다

Git의 사용법은 이 포스팅에서는 따로 하지 않겠습니다. 이유는 체계적으로 정리된 튜토리얼 사이트가 많이 존재하기 때문입니다. 그래서 저는 Git을 사용하면서 느꼈던 점과 중요 포인트를 정리할 예정이며, Git을 공부하실때 제가 언급한 포인트를 생각하면서 공부하시면 좋을것 같습니다.
(이번 Git 포스팅은 회사 서비스 오픈과 겹쳐 성의가 많이 떨어짐을 양해 부탁합니다(꾸벅)........... 우쒸 보기 싫음 보지마 퉤......)

팀원 모두가 잘쓰면 정말 좋은 Git, 아니라면 I'm sure that your team will be in HELL soon. Git을 처음 사용하면 생각보다 복잡한 개념과 사용법에 고전하게 됩니다. 그렇다고 하던 개발을 멈추고, Git을 공부하기란 쉽지않습니다. 결국 개발은 개발대로 진행하고, remote repository에 Push나 Merge를 할때 동료직원중 Git 고수를 소환하여 문제를 해결합니다. 여기까지는 별 문제가 없습니다. 하지만 언제나 함께였던 Git고수 동료가 없을때 문제가 발생합니다.

평소 하던대로 커밋을 하고 풀을 받고, 푸쉬를 하려합니다. 하지만 오랜만에 머지를 해서 그런지 충돌이 난 것같습니다. 충돌때문에 푸쉬가 되지않습니다. 여기서 부터 당황하기 시작합니다. 침착하게 소스코드를 확인합니다. 하지만 방금전까지 멀쩡하던 코드에 뒤죽박죽 빨간줄이 생기고, 에러 천국이 되어버렸습니다. Git을 욕하기 시작합니다. "이 썅개뭐같은것 이딴거 왜쓰는거야?!!". 욕하는 것도 잠시. 개발한 소스를 갱신하지 않으면 다른 동료 작업에 지장이 있기에 최대한 빨리 푸쉬를 해줘야합니다. 에라 모르겠다. 기존에 백업해둔 로컬 파일을 덮어쓰고 푸쉬합니다. 분명 자기자신만 사용하던 하위 브랜치기에 문제가 없으리라 생각합니다. 참고로 로컬에서는 정상적으로 잘 동작하던 소스였습니다.

다음날 오전.... 해맑게 웃으며 동료들과 스크럼 미팅을 진행합니다. 어제 개발 반영한 것에 대해 다음 작업을 진행할 동료에게 내용을 전달합니다. 5분뒤 누군가의 비명소리가 들려옵니다. "만어ㅣㅁ나어미나엄니ㅏ엄니ㅏ어마ㅣㄴ어ㅣ 내 소스 어디갔어 꺄오꺄오 ㅅㅍㅅㅍ!!!!!" 본능적으로 느낍니다. '나구나' Git을 사용하면서 Overwrite을 하는것은 절대적으로 피해야합니다. ***충돌은 반드시 소스 내에서 해결하여야 합니다.***

## Git 가지를 치자!!!
Git을 사용하다보면 어마무지한 뻘짓들을 하게 됩니다. 그러면서 얻은 교훈은 가지를 치자 가지치는데 돈 안들고 가지를 잘 칠 수록 행복해지리라~~!! 제가 사용하는 깃방식을 예를 들면 뿌리 (master)를 토대로 기둥(develop)으로 파생되고, 중심가지(서비스 카테고리. 지금 하는 서비스 같은 경우는 항공, 호텔, 보험 등)들이 자라납니다. 여기까지는 아주 훌륭합니다. 그러나 각 파트에서 개발하는 기능들은 가지를 치지 않는 경우가 발생합니다. 여기서 문제가 발생합니다. 가지를 치지 않은상태에서 진행중인 개발사항을 커밋을 하고 푸쉬를 했다고 칩시다. 그런데 다른 팀원의 기능개발이 끝나 develop 브랜치와 머지를 진행한다 합니다. '헐.... 나는 아직 안되는데....... 어쩌지어쩌지 !!! 으악.' 브랜치만 잘 땃어도ㅠㅠ. 물론 해결방법은 있습니다. 하지만 쓸데없이 추가되는 비용을 발생시킬 필요는 없겠죠~ ***Git은 가지치기 위해 존재한다. 고로 가지를 치라!!***

## Git 고수가 되고 싶나?
아래 reference만 진행하셔도 이미 당신은 깃 고수. 지금 바로시작하세요. 사실 이번 포스팅 Git은 작성하는 동안 흥미가 떨어져서 ㅠㅠ 주저리가 많았네요. 양해부탁드립니다.....(쪼쪼)

## Reference

* [Git 브랜치 배우기](http://learnbranch.urigit.com/)
Git으로 협업을 진행할때 가장 중요한 개념인 branch에 대하여 튜토리얼을 통해 학습 할 수 있는 사이트입니다. 제가 PM이라면 신입사원에게 이 사이트의 튜토리얼을 모두 완수하라는 특명을 내리겠습니다!!

* [git - 간편안내서](https://rogerdudler.github.io/git-guide/index.ko.html)
Git의 주요 명령어들이 어떤 상황에서 사용되어야 하는지 쉽게 이해할 수 있는 사이트입니다. 기본적인 git 사용법을 알고 있을때 전체적으로 훓어보기 좋습니다.

* [누구나 쉽게 이해할 수 있는 Git 입문](http://backlogtool.com/git-guide/kr/)
이 사이트의 내용을 모두 이해하셨다면 나는 이미 Git 도사!!! Git의 전반적인 내용을 다루고 있습니다. 버전관리 시스템을 처음 접하시는 분 부터 이미 Git을 사용하시는 분까지 적합한 사이트입니다.

아래 코드는 에러코드입니다. 신경쓰이겠지만 신경쓰지마세요.
```python
class Git(version_control_system):

    local = {
        "master" : source
        "develop" : source0
        "feature" : {
            "new_service" : source1_0,
            "new_feature" : source2,
        }
    }

    remotes.origin = {
        "master" : source
        "develop" : source0
        "feature" : {
            "new_service" : source1
        }
    }

    def __init__(self):
    def commit(self):
    def push(self):
    def pull(self):

    def checkout(self):
    def merge(self):
    def rebase(self):
```

### Related Posts
