# GitHub Actions

GitHub Actions는 GitHub에서 제공하는 CI(Continuous Integration, 지속 통합)와 CD(Continuous Deployment, 지속 배포)를 위한 서비스  

Repository에서 어떤 이벤트가 발생했을 때 특정 작업이 일어나게 하거나, 주기적으로 어떤 작업들을 반복해서 실행시킬 수 있음  

(현재 프로젝트에서 PR이 되면 coverage를 체크하고, merge되면 서버에 자동 배포되도록 하고 있음)  



## WorkFlows

자동화된 작업들로 `.github/workflows` 폴더 아래에 위치한 `YAML 파일`로 설정할 수 있음  

`YAML파일`에는 `on`속성을 통해 워크플로우가 실행되는 시점을 정의하고, `jobs` 속성을 통해 어떤 일을 하는지 명시함   

### On

workflows의 event를 명시하여 실행시점을 정의  





### Jobs

job이란 독립된 가상머신 또는 컨테이너에서 돌아가는 하나의 처리 단위  

모든 작업은 기본적으로 동시에 실행되며 필요 시 작업 간 의존관계를 설정해 실행 순서 제어 가능  

jobs에 해당하는 속성은 아래와 같은 것들이 있음  

- `runs-on`: 작업이 실행되는 실행환경 지정

- `steps`: 작업 순서를 정의

- `env`: job에서 사용할 환경변수를 key/value 형태로 설정  

- `strategy`: 여러 환경(ex 다양한 node버전)에서의 테스트/배포를 위해 build matrix를 구성

  

#### Steps

steps에 해당하는 속성은 아래와 같은 것들이 있음

- `name`: 

커맨드나 스크립트를 실행할 때 `run`속성을 사용, 액션을 사용할 때 `uses`속성을 사용  



## Actions





## Reference

- https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions
- https://www.daleseo.com/github-actions-basics/
- https://tech.kakaoenterprise.com/180