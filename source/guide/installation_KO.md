---
제목 : 설치
설명 : jbone 설치 개발 환경
키워드 : jbone 설치 개발 환경
유형 : 가이드
p : 가이드 / 설치
날짜 : 2019-11-29 18:39:06
---

jbone은 공공 프로젝트 및 비즈니스 라인 프로젝트를 포함하는 프로젝트 그룹입니다.

공용 프로젝트는 공용 jar 패키지 또는 시스템에서 사용하는 프로젝트이며 시스템 관리, 싱글 사인온 등과 같이 설치해야합니다.

LOB (Line-of-Business) 프로젝트는 특정 비즈니스 요구 사항을 충족하고 CMS, 전자 쇼핑몰 등과 같은 개인 요구 사항에 따라 선택 및 설치되는 프로젝트입니다.

> jbone의 첫 번째 설치는 구덩이를 피하기 위해 다음과 같은 방법으로 수행되어야합니다. 자유롭게 알아 내십시오.

## Redis 설치
### 다운로드
```쉘 스크립트
wget http://download.redis.io/releases/redis-5.0.3.tar.gz
```
### 압축 해제
```쉘 스크립트
tar xzf redis-5.0.3.tar.gz
```
### 설치
```쉘 스크립트
cd redis-5.0.3
하다
```
### 구성
`redis.conf`에 다음 구성을 추가합니다.

```쉘 스크립트
requirepass jbone
예를 데몬 화
```
### 시작
```쉘 스크립트
cd redis-5.0.3 / src /
./redis-server ../redis.conf
```
## RabbitMq 설치
### 설치
```쉘 스크립트
brew install rabbitmq
```
### 시작
```쉘 스크립트
/usr/local/Cellar/rabbitmq/3.7.10/sbin
./rabbitmq-server -detached
```
## Nginx 설치
### 설치
```쉘 스크립트
양조 nginx 설치
```
### 구성
nginx.conf에 다음 구성을 추가합니다.

```쉘 스크립트
업스트림 레지스터 {       
      서버 127.0.0.1:10001;
}
upstream smadmin {
      서버 127.0.0.1:10002;
}
업스트림 게이트웨이 {
      서버 127.0.0.1:10005;
}
업스트림 sso {
      서버 127.0.0.1:30001;
}
업스트림 ssomanagement {
      서버 127.0.0.1:30002;
}
업스트림 sysadmin {
      서버 127.0.0.1:20002;
}
upstream cmsadmin {
      서버 127.0.0.1:50002;
}
upstream cmsportal {
      서버 127.0.0.1:50003;
}
    서버 {
        들어 봐 80;
        server_name localhost;
        위치 / {
            루트 html;
            index index.html index.htm;
        }
        error_page 500502503504 /50x.html;
        위치 = /50x.html {
            루트 html;
        }
    }
서버 {
        들어 봐 80;
        server_name sso.local.jbone.cn;
        위치 / {
             proxy_set_header 호스트 $ host;
             proxy_set_header X-Real-Ip $ remote_addr;
             proxy_set_header X-Forwarded-For $ remote_addr;
             proxy_pass http : // sso /;
             proxy_redirect 끄기;
             루트 index.html;
        }
        error_page 500502503504 /50x.html;
        위치 = /50x.html {
            루트 html;
        }
    }
서버 {
        들어 봐 80;
        server_name ssomanagement.local.jbone.cn;
        위치 / {
             proxy_set_header 호스트 $ host;
             proxy_set_header X-Real-Ip $ remote_addr;
             proxy_set_header X-Forwarded-For $ remote_addr;
             proxy_pass http : // ssomanagement /;
             proxy_redirect 끄기;
             루트 index.html;
        }
        error_page 500502503504 /50x.html;
        위치 = /50x.html {
            루트 html;
        }
    }
서버 {
        들어 봐 80;
        server_name gateway.local.jbone.cn;
        위치 / {
             proxy_set_header 호스트 $ host;
             proxy_set_header X-Real-Ip $ remote_addr;
             proxy_set_header X-Forwarded-For $ remote_addr;
             proxy_pass http : // gateway /;
             proxy_redirect 끄기;
             루트 index.html;
        }
        error_page 500502503504 /50x.html;
        위치 = /50x.html {
            루트 html;
        }
    }
서버 {
        들어 봐 80;
        server_name smadmin.local.jbone.cn;
        위치 / {
             proxy_set_header 호스트 $ host;
             proxy_set_header X-Real-Ip $ remote_addr;
             proxy_set_header X-Forwarded-For $ remote_addr;
             proxy_pass http : // smadmin /;
             proxy_redirect 끄기;
             루트 index.html;
        }
        error_page 500502503504 /50x.html;
        위치 = /50x.html {
            루트 html;
        }
    }
서버 {
        들어 봐 80;
        server_name sysadmin.local.jbone.cn;
        위치 / {
             proxy_set_header 호스트 $ host;
             proxy_set_header X-Real-Ip $ remote_addr;
             proxy_set_header X-Forwarded-For $ remote_addr;
             proxy_pass http : // sysadmin /;
             proxy_redirect 끄기;
             루트 index.html;
        }
        error_page 500502503504 /50x.html;
        위치 = /50x.html {
            루트 html;
        }
    }
서버 {
        들어 봐 80;
        server_name cmsadmin.local.jbone.cn;
        위치 / {
             proxy_set_header 호스트 $ host;
             proxy_set_header X-Real-Ip $ remote_addr;      
             proxy_set_header X-Forwarded-For $ remote_addr;
             proxy_pass http : // cmsadmin /;
             proxy_redirect 끄기;
             루트 index.html;
        }

        error_page 500502503504 /50x.html;
        위치 = /50x.html {
            루트 html;
        }
    }
서버 {
        들어 봐 80;
        server_name cmsportal.local.jbone.cn;
        위치 / {
             proxy_set_header 호스트 $ host;
             proxy_set_header X-Real-Ip $ remote_addr;
             proxy_set_header X-Forwarded-For $ remote_addr;
             proxy_pass http : // cmsportal /;
             proxy_redirect 끄기;
             루트 index.html;
        }
        error_page 500502503504 /50x.html;
        위치 = /50x.html {
            루트 html;
        }
    }
서버 {
        들어 봐 80;
        server_name register.local.jbone.cn;
        

        위치 / {
             proxy_pass http : // register;
             proxy_redirect 끄기;
             루트 index.html;
        }

        위치 = /50x.html {
            루트 html;
        }

    }
```

### 시작
```쉘 스크립트
./nginx
```

## 로컬 호스트 구성
```속성
127.0.0.1 sso.local.jbone.cn
127.0.0.1 ssomanagement.local.jbone.cn
127.0.0.1 sysadmin.local.jbone.cn
127.0.0.1 cmsadmin.local.jbone.cn
127.0.0.1 cmsportal.local.jbone.cn
127.0.0.1 smadmin.local.jbone.cn
127.0.0.1 gateway.local.jbone.cn
127.0.0.1 register.local.jbone.cn
127.0.0.1 zipkinserver.local.jbone.cn
127.0.0.1 smmonitor.local.jbone.cn
```


## 공개 프로젝트 설치

### 소스 코드 다운로드

```쉘 스크립트
git clone https://github.com/417511458/jbone.git
git clone https://github.com/417511458/jbone-system.git
git clone https://github.com/417511458/jbone-system-admin.git
git clone https://github.com/417511458/jbone-sso.git
git clone https://github.com/417511458/jbone-service-management.git
```

### IDE 가져 오기
다운로드 한 소스 코드를 IDE로 가져 오기

### 설치
다음 순서로 한 번 설치하십시오.

* jbone
* jbone 시스템
* jbone-sso

```쉘 스크립트
mvn 설치
```

> 참고 : 공용 jar 프로젝트는 maven 중앙웨어 하우스에 게시되었습니다. 공용 jar 패키지를 수정하지 않으면 로컬에 설치할 필요가 없습니다.

## 로컬 시작
다음 순서로 프로젝트를 시작하십시오.
1. 먼저 Mysql, Redis, RabbitMq, Nginx 등을 시작합니다.
2. 서비스 거버넌스 파트를 시작하십시오.
3. 다른 프로젝트를 시작합니다.

### 서비스 등록 센터 시작
`jbone-sm-register`의 시작 클래스를 로컬에서 실행하거나`tomcat`에서 실행합니다.
### 시스템 관리 서비스 시작
`jbone-system-server`의 시작 클래스를 로컬에서 실행하거나`tomcat`에서 실행합니다.
### SSO 시작
`tomcat`에서 실행하십시오.

`sso-server`의 포트 번호는`30001`이고`sso-management`의 포트 번호는`30002`입니다.

### 시스템 관리 배경 시작
`jbone-system-admin`의 시작 클래스를 로컬에서 실행하거나`tomcat`에서 실행합니다.
### 액세스 테스트
브라우저에서 'http://sysadmin.local.jbone.cn'을 방문하여 로그인 페이지로 리디렉션합니다.

기본 사용자 이름과 비밀번호`jbone / jbone`을 입력하면 로그인이 성공하면 시스템 페이지로 리디렉션됩니다. 이는 성공을 의미합니다.
