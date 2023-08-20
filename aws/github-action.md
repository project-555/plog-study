# GitHub Actions

GitHub Actions는 GitHub에서 제공하는 CI(Continuous Integration, 지속 통합)와 CD(Continuous Deployment, 지속 배포)를 위한 서비스  

Repository에서 어떤 이벤트가 발생했을 때 특정 작업이 일어나게 하거나, 주기적으로 어떤 작업들을 반복해서 실행시킬 수 있음  

(현재 프로젝트에서 PR이 되면 coverage를 체크하고, merge되면 서버에 자동 배포되도록 하고 있음)  



## WorkFlows

자동화된 작업들로 `.github/workflows` 폴더 아래에 위치한 `YAML 파일`로 설정할 수 있음  

`YAML파일`에는`name`속성에 해당 workflow의 이름을 명시하고,  `on`속성을 통해 워크플로우가 실행되는 시점을 정의하고, `jobs` 속성을 통해 어떤 일을 하는지 명시함   

### On

workflows의 event를 명시하여 실행시점을 정의  

### Jobs

job이란 독립된 가상머신 또는 컨테이너에서 돌아가는 하나의 처리 단위  

모든 작업은 기본적으로 동시에 실행되며 필요 시 작업 간 의존관계를 설정해 실행 순서 제어 가능  

jobs에 해당하는 속성은 아래와 같은 것들이 있음  

- `runs-on`: 작업이 실행될 컴퓨팅 자원(runner) 지정(required)

- `env`: job에서 사용할 환경변수를 key=value 형태로 명시

- `strategy`: 여러 환경(ex. 다양한 node버전)에서의 테스트/배포를 위해 build matrix를 구성

- `needs`: needs에 job을 명시하여 의존관계 설정 가능

- `steps`: job이 가지는 순차적인 동작의 나열, 컴퓨팅 자원에서 독립적인 프로세스로 동작하며 runner의 파일 시스템에 접근할 수 있음

#### Steps

steps에 해당하는 속성은 아래와 같은 것들이 있음

- `name`: step의 이름을 명시, github actions 페이지에서 workflow 구동로그를 확인할 때 보여짐
- `uses`: step에서 사용할 action을 선택(github marketplace에서 action들을 확인할 수 있음), `{owner}/{repo}@{ref|version}`의 형태를 지님
- `run`: job에 할당된 컴퓨팅 자원의 shell을 이용하여 command line program을 구동

커맨드나 스크립트를 실행할 때 `run`속성을 사용, 액션을 사용할 때 `uses`속성을 사용  



## Actions

workflow의 가장 작은 블럭으로, 재사용 가능한 컴포넌트



## Reference

- https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions
- https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions
- https://www.daleseo.com/github-actions-basics/
- https://zzsza.github.io/development/2020/06/06/github-action/
- https://hwasurr.io/git-github/github-actions/