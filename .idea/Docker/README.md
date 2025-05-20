# 🐳Docker와 CI/CD
---

## 🐳도커(Docker)란?

Docker는 **컨테이너(Container) 기술**을 이용해 소프트웨어를 쉽고 빠르게 개발, 배포, 실행할 수 있게 도와주는 플랫폼입니다.

컨테이너는 애플리케이션과 그 실행 환경(라이브러리, 설정 등)을 하나로 묶어서 어디서든 동일하게 실행할 수 있게 해줍니다.

---
## Docker 주요 개념
[이미지(Image)]
- 애플리케이션 실행에 필요한 모든 것(코드, 라이브러리, 환경 등)이 포함된 파일
- 변경 불가능하며, Dockerfile로 만듦

[컨테이너(Container)]
컨테이너는 애플리케이션과 그 실행 환경을 함께 패키징하여 어디서든 동일하게 실행될 수 있도록 해주는 기술입니다.
- 이미지를 실행한 상태 
- 실제로 동작하는 애플리케이션 인스턴스

---

## Docker를 사용하는 이유

1. **일관성**: "내 컴퓨터에서는 잘 되는데..."와 같은 문제가 줄어듭니다.
2. **이식성**: 컨테이너는 어디서든 동일한 환경을 제공하므로, 다양한 플랫폼에서 쉽게 애플리케이션을 실행할 수 있습니다.
3. **확장성**: 마이크로서비스 아키텍처(MSA)와 궁합이 좋음

여러 상황에서 환경이 달라 동작하지 않을 수 있지만, 도커를 사용한다면 해결 가능!

---

### Docker 시작하기

Docker를 사용해보려면, 먼저 Docker를 설치해야 합니다.<br>

도커 설치: [**https://www.docker.com/get-started/**](https://www.docker.com/get-started/)

윈도우의 경우 `Hyper V` 주의!

💡 **도커 명령어 암기** **절대 금지!** 모르는 건 그 때 그 때 검색하기. 😄
1. Dockerfile을 생성해요.

        <aside>
        💡 **도커파일(Dockerfile)이란?**
        Dockerfile은 Docker 이미지를 빌드하기 위한 설정 파일로, Docker 이미지를 생성하는 데 필요한 명령어와 지침을 포함하고 있습니다. Dockerfile은 일반 텍스트 파일 형식으로 작성되며, Docker가 어떤 식으로 애플리케이션을 설정하고 실행할지에 대한 명세를 담고 있습니다.

        </aside>

       그런데 Dockerfile? 도대체 어떻게 만드는 걸까요? 그럴 땐 검색, 혹은 ChatGPT에게 물어보면 금방 알 수 있어요.

        - ChatGPT에게 물어보기

          ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/d1db10b2-5d8f-46fa-b898-6d28b0a6dcb8/Untitled.png)

          ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/0350f1d4-114f-4108-b482-e3358b8162d1/Untitled.png)


        ---
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/2c04ed54-b542-496d-99ea-a2c74a244af1/Untitled.png)
        
        <aside>
        💡 **alpine이란?**
        Alpine Linux는 최소한의 패키지만을 포함하는 경량 리눅스에요. 이것이 무엇인지 정확히 알 필요는 없어요. 단, 우리는 이것만 기억하면 돼요.
        **일반 이미지에 비해 가볍기 때문에 빌드, 배포 속도가 빨라진다!**
        
        </aside>
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/01a00f35-5d0a-4cf4-a429-883f09eeabc3/Untitled.png)
        
        429.53mb → 345.98mb, **alpine 이미지가 20% 가량** 더 가벼운 것을 확인할 수 있어요.
        
    
    1. 도커 이미지를 빌드해요.
        
        ```bash
        docker build -t test-docker-hello .
        ```
        
        (`test-docker-hello`라는 이름으로 도커이미지를 빌드)
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/f41824a9-f983-4736-a932-fcca1b755e43/Untitled.png)
        
    2. 빌드한 도커 이미지를 실행시켜요.
        
        ```bash
        docker run -d -p 8080:8080 test-docker-hello
        ```
        
        ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/569ae755-a047-4aa0-a967-812f3d38fc17/Untitled.png)
        
        `cranky_pike`라는 Container 이름으로 `test-docker-hello` 이미지가 실행된 것을 볼 수 있어요!
        
        - Container 이름을 지정해주려면?
            
            ```bash
            docker run -d -p 8080:8080 **--name custom-container-name** test-docker-hello 
            ```
            
            `—-name 지정하고싶은이름` 을 추가해서 이름을 지정해줄 수 있어요.
            
            `8080:8080` : 도커 내부의 port를 외부에 노출시켜주어야해요. 보통은 복잡도를 낮추기 위해 xxxx:yyyy를 같게 설정합니다(xxxx=yyyy).
            
            ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/50d4c9f0-ec79-41c6-9b28-58d2166dba91/Untitled.png)
            
            <aside>
            💡 이 또한 외우는 것이 아니라, 검색하면 다 찾아볼 수 있어요. **절대 암기 금지!**
            
            </aside>



❓ `docker build -t test-docker-hello .`

- 이 명령어 끝에 있는 ‘.’은 무엇을 뜻할까요?

  현재 디렉토리에 있는 Dockerfile을 빌드하겠단 뜻.

  `docker build -t test-docker-hello -f Dockerfile-dev .`

  (tip: -f는 file입니다.)



---

## Docker Compose란 무엇인가요?

docker-compose는 여러 개의 Docker 컨테이너를 정의하고, 이들을 하나의 애플리케이션으로 관리할 수 있게 해줍니다.

```yaml
version: '3.8'
services:
  myapp:
    build:
      context: .
      dockerfile: Dockerfile
    depends_on:
      db:
        condition: service_healthy
    ports:
      - "8080:8080"

  db:
    image: mysql:8.0
    container_name: mysql
    environment:
      MYSQL_ROOT_PASSWORD: 1234
      MYSQL_DATABASE: test
    ports:
      - "3306:3306"
    healthcheck:
      test: ["CMD-SHELL", "mysqladmin ping -h localhost -u root -p1234 && sleep 5"]
      interval: 5s
      retries: 10
```

이제 이 docker-compose를 실행해볼까요?

```yaml
docker-compose up -d
```

<aside>
💡 db에 port가 주석 처리된 이유에 대해서 생각해보아요.
만약 port가 있어야한다면 어떤 필요가 있어서 있어야할까요?

> **이 부분이 가장 많이 실수하시고 어려워하시는 부분이니 주의해서 들어주세요!**
>
</aside>

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/d2ea3b6b-5a7a-4d5c-9c74-78673fadb7d6/Untitled.png)

<aside>
💡 docker-compose 전에 build 잊지 마세요!

</aside>

<aside>
💡 멘토링을 하면 docker-compose에서 막히신 분이 굉장히 많았는데, 아마 properties 세팅 때문일 가능성이 큽니다.
왜냐하면 intellij로 실행하신 환경과, docker로 실행하신 환경은 분명 다르기 때문입니다.
분리된 네트워크 환경이란 것을 꼭 기억해주세요!

</aside>

-

  `ENV SPRING_PROFILES_ACTIVE=dev` 와 같은 방식으로 Dockerfile을 세팅하시면 환경변수를 설정해줄 수 있습니다.
  그 외에 여러가지 방법이 있고, 회사마다 다르지만
  Dockerfile image 빌드 시 환경변수를 지정해줄 수도 있고,
  docker-compose 실행 시 환경변수를 지정해줄 수도 있습니다,
  아니면 아예 `Dockerfile-dev` 같은 식으로 Dockerfile을 분리할 수도 있습니다.
  혹은 쉘 스크립트를 짜서 실행할 수도 있을 거예요.
  여러분에게 편한 방법으로 세팅해보세요!

💡 **외우지마세요! 느낌만 가져가시고, 검색하세요. 혹은 AI에게 물어보세요.**

---

### docker-compose를 왜 사용할까요?

아래와 같은 네트워크 환경이 있다고 가정합시다.

(Spring Container 3개, Redis Container 1개, MySQL Container 1개, MongoDB Container 1개)

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/83c75a39-3aba-4ba4-a792-7aefe4b07895/2fee8bce-2bd1-4abe-8e9c-fe132be0b6f1/Untitled.png)

- docker-compose 없이 Container들 간에 통신을 하려면 어떻게 해야할까요? (몰라도 됩니다!)

  ### 1. Docker 네트워크

  Docker 네트워크를 직접 만들어 서로 다른 컨테이너들을 연결시켜줄 수 있습니다.

    ```bash
    docker network create hello-network
    ```

    ```bash
    docker run -d --name container1 --network hello-network spring_image
    docker run -d --name container2 --network hello-network mysql_image
    ```

  ### 2. Docker 링크 옵션 사용 (Deprecated)

  더 이상 사용하지 않지만, 설령 보게 된다면 “아, 이런게 있었지” 정도로만 넘어가시면 됩니다!

    ```bash
    docker run -d --name container1 spring_image
    docker run -d --name container2 --link container1:alias_for_container1 mysql_image
    ```

    <aside>
    💡 만약 관리해야할 이미지, 컨테이너가 많다면 이러한 명령어들만으론 굉장히 어려울 거예요. docker-compose가 얼마나 강력한 도구인지 알 수 있겠죠!

    </aside>


---

### MSA와 Docker Compose를 엮어서 생각해보기

수많은 마이크로 서비스들을 따로 따로 띄운다면 얼마나 힘들까요? 아마 개발을 시작하기도 전에 지쳐버릴 거예요.

💡 하지만 실제 배포 상황과, 로컬 개발 상황에서 docker-compose를 사용하는 것은 다른 일입니다.
이에 대해 이야기해보아요.

---

## CICD란 무엇일까요?

> **마법은 없다.**
>

CI/CD는 **지속적 통합(Continuous Integration) 및 지속적 배포(Continuous Deployment)**를 의미하며, 소프트웨어 개발 라이프사이클을 간소화하고 가속화하는 것을 목표로 합니다.


💡 CI? CD? 
한 번 더 생각해보기

💡 CICD의 방법은 다양합니다.

하지만 **암기의 영역**이 아닙니다.

그렇기 때문에 단순히 인터넷에서 CICD 구현 방법을 검색해서 하는 것보다, CICD의 과정을 한 번 찬찬히 살펴보며 이러한 방법은 어떨까? 저렇게 하면 안될까? 라는 식으로 고민을 해보는 것이 여러분들의 실력 향상에 큰 도움을 줄 것이라고 생각합니다.

CICD를 **3단계**의 큰 단위로 분류하고, 이를 기반으로 생각한다면 절대 어렵지 않아요!


## CICD의 3단계

- CICD를 3단계로 정의해본다면 어떻게 나눌 수 있을까요?
    1. 개발
    2. 빌드
    3. 배포


💡

CICD를 3단계로 분류 완료했다면, 이제 직접 CICD 파이프라인을 구성해봅시다!

