# docker
1. Docker 실습 샘플 설치하는 문제 
# Docker 설치 및 확인
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo systemctl start docker
sudo systemctl enable docker
docker --version

# Docker 실습 샘플 설치
git clone https://github.com/docker/labs.git
cd labs
git checkout master

# 실습 샘플 목록 확인
ls

2. docker 통해서 Redmine 설치 및 Github연동
# Docker 이미지 다운로드
docker pull redmine (thêm)
docker stop redmine (dừng)
docker rm redmine (remade)

# Docker 컨테이너 실행
docker pull postgres
docker run -d --name=postgresql -e POSTGRES_PASSWORD=mysecretpassword postgres

docker run -d --name=redmine --link=postgresql:postgresql -p 8081:80 redmine

# Github 연동 설정
- 설정 및 적용 과정은 사용자 및 환경에 따라 다르므로, 이 과정은 생략한다.

3. Jenkins와 Github연동??
brew install jenkins
docker exec jenkins2 cat /var/jenkins_home/secrets/initialAdminPassword
# Docker 이미지 다운로드
docker pull jenkins/jenkins
# Docker 컨테이너 실행
docker start jenkins2
docker run -d -p 8081:8080 -p 50000:50000 --name=jenkins jenkins

# Github 연동 설정
- 설정 및 적용 과정은 사용자 및 환경에 따라 다르므로, 이 과정은 생략한다.

4. docker image start & 수정 or 삭제
# Docker 컨테이너 시작
docker start <container_name>

# Docker 컨테이너 수정
- 수정 가능한 내용: 네트워크, 스토리지, 실행 중인 프로세스 등
- 컨테이너 내부로 접속하여 설정 파일을 수정하는 방법 등이 있다.

# Docker 컨테이너 삭제
docker rm <container_name>

5. docker image 직접수정
# Docker 이미지 다운로드 및 수정
docker pull <image_name>
docker commit <container_id> <new_image_name>

# 수정된 Docker 이미지 확인
docker images
6. docker compose 실행
# docker-compose.yml 파일 작성
version: '3'
services:
 web:
    image: <web_image_name>
    ports:
      - "8080:80"
 db:
    image: <db_image_name>
    volumes:
      - db-data:/var/lib/postgresql/data
volumes:
 db-data:

# Docker Compose 실행
docker-compose up -d

# Docker Compose 종료
docker-compose down


7. open API 실습
pip install requests
url = "https://jsonplaceholder.typicode.com/todos/1"
import requests
response = requests.get(url)
print(response.json())
