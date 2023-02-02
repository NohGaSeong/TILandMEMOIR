## Dockerfile 문법
```.yaml
FROM node:12-alpine
RUN apk add --no-cache python3 g++ make
WORKDIR /app
COPY . .
RUN yarn install --production
CMD ["node", "src/index.js"]
```
도커 공식 문서에 가보면 정확히 알 수 있다.

### Format
형식은 Dockerfile .

```.yaml
# Comment
INSTRUCTION arguments
```
- 명령어는 대소문자를 구분하지 않음. 하지만 인수와 더 쉽게 구별하기 위해 대문자로 지정하는 편임.
- Docker 명령을 Dockerfile 순서대로 실행함.
- 도커 파일은 from 명령으로 시작해야함.
- from 명령은 빌드할 상위 이미지를 지정함.
- from 은 도커 파일의 from 행에 사용되는 인수를 선언하는 하나 이상의 arg 명령어 앞에만 올 수 있음.
- 도커는 #로 시작하는 행을 주석으로 처리함.

### 주요 명령
#### FROM
- 베이스 이미지 지정 명령
- Dockerfile에서 반드시 있어야 하는 명령어임.
- 베이스 이미지란 그 충 중에서 가장 기본이 되는 이미지이고 FROM이 이 이미지를 지정해줌.

#### LABEL
- = 형식으로 메타 데이터를 넣을 수 있는 기능
- 보통 저자,버전,설명,작성일자 등을 각각 key = value 형식으로 적는다.
```.yaml
LABEL maintainer="dev.yohan05@gmail.com"
```
#### CMD
- 해당 dockerfile 로 만든 이미지를 기반으로 컨테이너를 만들었을 때, 해당 컨테이너가 실행될때 가장 먼저 실행될 프로그램을 기술
- CMD는 하나의 dockerfile에서 한 가지만 설정되며, 만약 cmd 설정이 여러개일 경우, 맨 마지막에 설정된 CMD 설정만 적용됨.
#### RUN
- 도커 명령어의 run 와는 다른 명령어
- 이 항목의 기능을 알기 위해서는 docker 이미지의 구성 방식을 알아야함.
    - docker는 이미지를 생성 할 때, 하나의 layer만 쓰는 것이 아니라, 여러 단계의 layer를 층층이 쌓아야함.
    - RUN 명령은 이미지 생성시, 일종의 layer을 만들 수 있는 단계, 보통 베이스 이미지에 패키지를 추가로 설치하여 새로운이미지를 만들 때 사용함.
    
```.yaml

...

RUN apt-get update
RUN apt-get install -y apache2

# 이런 식으로 말이다.
```
#### ENTRYPOINT
만약 dockerfile 로 이미지를 만든 다음, 컨테이너를 docker run 으로 생성/실행하면서 명령문을 같이 적으며 실행한다면, 기존 이미지에 있던 CMD 명령이 터미널 명령을 씌워진다.

하지만, 이미지에 entrypoint 항목이 있다면, docker run 으로 명령을 싱행하더라도 entrypoint의 명령에 영향을 끼치지 못하고 entrypoint의 명령 뒤에 쭉 인자로 나열을 하게 된다.
#### EXPOSE
- docker 컨테이너의 특정 포트를 외부에 오픈하는 설정
- docker run -p 옵션과 유사하다. 차이점은 -p 옵션은 컨테이너의 특정 포트를 외부에 오픈하고, 해당 포트를 호스트 pc 의 특정 포트와 매핑 시키는 것까지 알아서 해주지만, expose 는 그냥 단순히 포트를 열어주기만 한다는 것.
- 결국 도커 파일에 expose 로 포트를 열어줘도 docker run 을 할때 p 옵션을 쓰게 된다.

#### WORKDIR
- 이미지 내에서 특정 폴더로 이동하기 위해서 쓰는 명령 cd 같은 느낌이라고 보면 된다.
`WORKDIR /usr/app`

### 도커 환경변수
#### 환경 변수
```yaml
ENV PORT 80
EXPOSE $PORT # EXPORT PORT 80
```
- 이때의 환경변수는 컨테이너의 환경변수.

#### 빌드 인수
인수의 경우 Dockerfile을 통해 `docker build` 를 실행할 때 `--build-arg` 옵션으로 인수를 전달하는 방식. 이 방식은 이미지를 build 할 때 다른 값을 추가할 수 있음.

run time 환경변수와 다른 것 : 이전 환경 변수는 빌드된 이미지를 인스턴스화 시켜 컨테이너를 생성할 때 환경변수를 설정한 것이지만 arg 방식은 이미지를 빌드 할 때 전달하는 방식.

```.yaml
FROM node:14
ARG DEFAULT_PORT=80 #ARG 옵션 추가
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
ENV PORT $DEFAULT_PORT
EXPOSE $PORT

CMD ["npm", "start"]
```
- 80번 포트를 기본적으로 사용하게되지만 build를 할 때 아래와 같이 동적으로 변경해줄 수 있음.
`docker build -t node-server:prd --build-arg DEFAULT_PORT 8080 .`
- 도커파일의 수정이 필요없이 유연한 방식으로 다른 이미지를 빌드할 수 있다는 것임.
