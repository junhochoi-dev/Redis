# Redis 설치

> MacOS

- https://redis.io/docs/getting-started/installation/install-redis-on-mac-os/

1. HomeBrew 설치
   - `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`
2. Redis 설치
   - `brew install redis`
3. Redis 실행
   - `brew services start redis`
4. Redis 종료
   - `brew services stop redis`

> Windows

- https://redis.io/docs/getting-started/installation/install-redis-on-windows/

1. Redis 설치
   - `curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg`
   - `echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list`
   - `sudo apt-get update`
   - `sudo apt-get install redis`
2. Redis 실행
   - `sudo service redis-server start`

> 명령어

- REDIS-CLI 실행
  - `redis-cli`
- PING
  - PONG 리턴시 REDIS 정상 실행
- 데이터 저장
  - `SET lecture inflearn-redis`
  - OK
- 데이터 불러오기
  - `GET lecture`
  - inflearn-redis
- REDIS 명령어는 대소문자 둘다 가능
- 데이터 삭제하기
  - `DEL lecture`
- 데이터가 없을 때 불러오기
  - `GET lecture`
  - nil (=null)
- REDIS-CLI 종료
  - `exit`