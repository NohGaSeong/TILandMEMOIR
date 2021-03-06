# DevOps 기법
## 공부하게 된 이유
- 팀 내에서 DevOps 로써 팀원들에게 무엇을 해줄 수 있을까 하며 찾아보던 와중 DevOps가 하는 업무, 일들을 찾게 되었고 그것들에 대해서 정리 해볼려고한다.

## 01. 사람들에게 우위를 둔 다음, 프로세스와 테크놀로지에 초점을 맞춘다.
- 소프트웨어 개발의 3대 요소는 사람, 프로세스, 도구 입니다. 데브옵스 문화를 받아들일 때는 3개 요소가 현재의 요구 사항에 맞게 적절하게 조저오디어야합니다.
- 조직에서 소프트웨어 개발 수명주기를 최소화할 수 있는 프로세스 그리고 적절한 도구와 테크놀로지를 갖춘 인프라는 데브옵스를 매끄럽게 구현할 수 있도록 도와줍니다.
- 결국 데브옵스는 다른 부서들과 함께 하는 것이기에, 이 주레를 다루는 조직에서는 팀원들로 하여금 회사 안에서 다양한 역할을 수행하면서 고도로 생산적인 환경을 구축하기 위해 서로 간의 실천 기법과 경험을 공유하도록 유도합니다.

## 02. SDLC를 지원하기 위해서 테스트를 자동화한다.
- 테스트를 자동화 -> 지속적인 코드 및 데이터 품질 검사를 갖춘 자동화된 인프라를 의미
- 소프트웨어 개발 수명주기의 흐름을 유지하면서 테스트를 자동화하게 되면, 검증을 거친 코드가 데브옵스의 파이프라인을 따라서 자동적으로 개선되거나 또는 뒤늦게 결함이 발견되는 것을 방지 할 수 있음.

## 중앙 집중식 데브옵스 인프라를 구축한다.
- 데브옵스의 파이프라인 과정에서 일반적으로 사용되는 도구들은 다양하게 존재하는데, 대표적으로는 젠킨스, 스플렁크, 테라폼, 나기오스, 그라파나, 프로메테우스 등이 있습니다.
- 따라서 데브옵스로 전활할 때는 중앙 집중화되고, 영합된 인프라가 균형을 잘 맞출 수 있도록 관리 시스템이 특별히 구현되어야합니다.
- 이를 통해 프로비저닝, 보안, 연결성과 관련하여 사람들이 조직되ㅣ어있는 독립적인 개발자 중심의 데브옵스 모델로 전환활 수 있고, 보다 쉽게 접근할 수 있으며, 중앙 집권화된 소스 저장소를 갖춘 API 기반의 방식으로 스프투에어를 개발할 수 있씁니다.

## 처리량을 향상 시키기 위해서 배포 자동화를 구현한다.
- 배포의 안정성은 지속적인 배포가 제대로 이뤄지고 있는지를 가늠하는 지표이며, 지정된 저장소가 얼마나 성공적인지, 그리고 코드 생성, 버전 관리, 테스트, 배포, 배포 이후의 절차와 같은 배포의 허위 프로세스들이 과연 제대로 제어되고 있는지에 대해서 팀에게 정보를 알려줍니다. 

## 지속적인 통합 및 지속적인 배포의 과정에서 지속적인 모니터링과 지속적인 관찰 가능성을 수립한다.
- 장애가 있을 때 빠르게 확인하기 위해서는 프로세스를 지속적으로 모니터링해야함.
- 효율적인 모니터링 도구는 컨테이너 환경, 클라우드 환경 그리고 온프레미스 환경에서 모두 동일하게 잘 대처할 수 있음.
- 가장 많이 쓰이는 모니터링 도구로는 센수, 프로메테우스, 나기오스 등이 있습니다.
- 또한 슬렉, 페이저듀티, 서비스나우와 같은 데브옵스 알림 도구가 있는데 이들은 팀에서 대응해야하는 이슈가 발생했을 때 그에 대한 중요한 정보를 제공해줍니다.
- 견고한 모니터링 환경을 조성하기 위한 목적으로 데브옵스 도구들을 합리적으로 사용한다면, 팀의 기능이 확장되고, 팀원들이 담당하는 제품이나 서비스의 품질과 가치를 개선할 수 있습니다.

## 지속적인 통합으로 성과를 개선한다.
- 지속적인 통합을 지원하고 실천하면 그룹들 사이의 협업을 돕기 때문에, 전반적인 성과를 향상시킬 수 있음.
- 지속적인 통합을 실천하는 개발 부서는 코드 변경으로 인해서 기존의 기능이나 테스트가 중단되지 않았음을 확인하기 위해서 자동화된 테스트를 구성해야 할것임.

## 서버리스를 통해서 조직이 긍정적으로 변화할 수 있도록 유지한다.
- 서버리스 아키텍처는 데브옵스의 잠재력을 최대한 발휘할 수 있도록 힘을 실어줍니다.
- AWS Lambda, Google Cloud Functions 등 데브옵스 조직의 고유한 요구사항을 충족시킬 수 있도록, 서버리스 인프라 위에서 어플리케이션을 실행하기 위한 환경이 잘 갖추어져 있습니다.
- IT 아키텍처에서의 이러한 변화는 소프트웨어 개발 부서와 운영 부서가 함께 일하는 방식도 변화시킬 겁니다.

## 데브옵스 도입?
- 쉽진 않지만 시도해 볼 만한 가치가 있는 변화인 것은 확실함.
- 생산성과 효울성에 긍정적인 영향을 미치고, 소프트웨어의 품질을 개선하며, 궁긍적으로 최대한 빠르게 가치를 전달하는 것.
