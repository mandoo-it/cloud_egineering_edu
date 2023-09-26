2# 최신 컨텐츠를 제공하는 웹 애플리케이션 서버

```
[ 요구사항 ] 

두 개의 컨테이너로 구성된 어플리케이션을 개발

1. 첫번째 컨테이너는 주기적으로 깃 허브에서 컨텐츠(HTML)를 다운로드하는 쉘 스크립트가 동작
깃 허브 주소는 컨테이너는 실행할 때 환경 변수로 전달 받아서 사용한다. 

2. 두번째 컨테이너는 첫번째 컨테이너를 사용하여 nginx 서버가 동작하게한다. 
 
```

#### 1. 작업 디렉터리 생성

``` shell
C:\docker> mkdir sidecar
C:\docker> cd sidecar
C:\docker\sidecar>
```


#### 2. cloner 파일을 작성 ⇐ 깃 허브로부터 60초 단위로 컨텐츠를 가져오는 쉘 스크립트 


``` shell
#!/bin/bash

# GITHUB_URL 환경변수가 설정되어 있는지 확인 
# 설정되지 않은 경우 에러 종료
if [ -z $GITHUB_URL ]; then
    exit 1
fi

# 처음에는 git clone을 통해서 컨텐츠를 가져옮
git clone $GITHUB_URL /data

# 이후에는 60초 마다 깃 허브에서 컨텐츠를 가져옮
cd /data
while true
do
    date
    sleep 60
    git pull
done

```
- 주의 할 점 : 리눅스 개행문자로 바꿔줘야 쉘스크립트가 제대로 작동한다. 
![1695715205335](image/실습2_git이랑연동/1695715205335.png)

#### 3. Dockerfile 작성
``` docker
FROM    ubuntu
RUN     apt-get update && apt-get install -y git
RUN     mkdir /myapp
WORKDIR /myapp
COPY    cloner /myapp/
RUN     chmod a+x /myapp/cloner
CMD     [ "/myapp/cloner" ]

```


#### 4. 이미지 빌드

![1695715924065](image/실습2_git이랑연동/1695715924065.png)

#### 5. git에 레포지토리 생성
![1695716007172](image/실습2_git이랑연동/1695716007172.png)

#### 5. git에 레포지토리 생성
- 첫번째 컨테이너 실행 ⇒ git clone 후 1분 단위로 git pull 하는지 확인

``` shell
docker container run -d -e GITHUB_URL=https://github.com/mandoo-it/sidecar.git -v c:\docker\sidecar\html\:/data --name cloner_container cloner_container:1.0
```
