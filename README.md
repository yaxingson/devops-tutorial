# Devops Tutorial

## Development

### Plan

### Code

### Build

### Test

## Operations

### Integrate

> CI(Continuous integration)

__Jenkins__

[Install Docker](https://docs.docker.com/engine/install/)

```sh
docker pull gitlab/gitlab-ce:latest
docker pull jenkins/jenkins:2.319.1-lts

touch docker-compose.yml

docker-compose down
docker-compose up -d
docker-compose restart

docker logs -f jenkins

docker exec -it gitlab bash

```

```yml
# docker-compose.yml
version: "3.1"
services:
  jenkins:
    image: jenkins/jenkins:2.319.1-lts
    container_name: jenkins
    ports:
      - 8080:8080
    

```

```txt
# Dockerfile


```

__Gitlab CI/CD__

```sh
# install gitlab with docker
docker pull gitlab/gitlab-ce:latest

docker run -d -p 443:443 -p 80:80 -p 22:22 --name gitlab -- restart always gitlab/gitlab-ce

docker start gitlab

```

> Gitlab Runners: `Shared Runner`、`Group Runner` & `Specific Runner`

```sh
# install github-runner with package manager
sudo yum install github-runner-10.0.0-1

# or with docker
docker pull gitlab/gitlab-runner:v12.9.0

docker run -v gitlab/gitlab-runner:v12.9.0

docker exec -it gitlab/gitlab-runner bash

gitlab-runner register

gitlab-runner verify

```

Gitlab runner executor：

- Shell
- Docker
- Kubernetes


```yml
# .gitlab-ci.yml
stages:
  - build
  - deploy

variables:
  DOMAIN: example.com

before_script:
  - echo "pipeline start"

install:
  stage: .pre
  script:
    - echo ""

format:
  script:
    - echo "foramt code"
  

build:
  stage: build
  tags:
    - build
  only:
    - main
  script:
    - echo "start build"

deploy:
  stage: build
  retry:
    max: 1
    when:
      - script_failure
  only:
    - main
  script:
    - echo "start deploy"

clean:
  stage: .post
  when: delayed
  start_in: "10"
  script:
    - echo "clear cache"

after_script:
  - echo "pipeline end"

```



__Github Actions__



### Deploy

> CD(Continuous Deploy)


### Operate

### Monitor
