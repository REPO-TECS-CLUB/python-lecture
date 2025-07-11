# Docker + Ubuntu 24.04 + nginx WordPress 개발 실습 가이드

## 1. Docker 컨테이너 생성 및 기본 설정

### 1.1. Docker 컨테이너 실행

```bash
docker run -it --name wordpress-dev -p 22:22 -p 80:80 ubuntu:24.04 /bin/bash
```

### 1.2. 시스템 업데이트 및 기본 패키지 설치

```bash
apt update && apt upgrade -y
apt install -y openssh-server sudo nano wget curl unzip
```

### 1.3. 개발용 계정 생성

```bash
# dev 사용자 생성 및 패스워드 설정
useradd -m -s /bin/bash dev
echo 'dev:dev' | chpasswd
usermod -aG sudo dev

# dev 사용자의 홈 디렉토리 권한 설정
chown -R dev:dev /home/dev
chmod 755 /home/dev
```

### 1.4. SSH 서비스 설정

```bash
# SSH 설정 수정
sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config
sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config
sed -i 's/#Port 22/Port 22/' /etc/ssh/sshd_config

# SSH 서비스 시작 (Docker 컨테이너에서는 service 명령어 사용)
service ssh start
```

### 1.5. 웹 디렉토리 생성

```bash
# dev 사용자로 전환하여 웹 디렉토리 생성
su - dev
mkdir -p /home/dev/WEB/wp
exit
```

## 2. PuTTY 및 VS Code Remote-SSH 접속 설정

### 2.1. PuTTY 접속

- Host Name: `localhost`
- Port: `22`
- Connection Type: `SSH`
- Username: `dev`
- Password: `dev`

### 2.2. VS Code Remote-SSH 접속

1. VS Code에서 Remote-SSH 확장 설치
2. `Ctrl+Shift+P` → "Remote-SSH: Connect to Host" 선택
3. `dev@localhost:22` 입력
4. 패스워드: `dev`

## 3. nginx 웹 서버 설치 및 설정

### 3.1. nginx 및 PHP 설치

```bash
apt install -y nginx php8.3-fpm php8.3-mysql php8.3-mbstring php8.3-zip php8.3-gd php8.3-curl php8.3-xml php8.3-cli
```

### 3.2. nginx를 dev 사용자로 실행하도록 설정

```bash
# nginx 설정 파일 수정
sed -i 's/user www-data;/user dev;/' /etc/nginx/nginx.conf

# PHP-FPM을 dev 사용자로 실행하도록 설정
sed -i 's/user = www-data/user = dev/' /etc/php/8.3/fpm/pool.d/www.conf
sed -i 's/group = www-data/group = dev/' /etc/php/8.3/fpm/pool.d/www.conf
sed -i 's/listen.owner = www-data/listen.owner = dev/' /etc/php/8.3/fpm/pool.d/www.conf
sed -i 's/listen.group = www-data/listen.group = dev/' /etc/php/8.3/fpm/pool.d/www.conf
```

### 3.3. nginx 가상 호스트 설정

```bash
# 기본 사이트 설정 제거
rm -f /etc/nginx/sites-enabled/default

# 새로운 사이트 설정 생성
cat > /etc/nginx/sites-available/wp << 'EOF'
server {
    listen 80;
    server_name localhost;
    root /home/dev/WEB/wp;
    index index.php index.html index.htm;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    location /mysql {
        alias /home/dev/WEB/wp/mysql;
        location ~ \.php$ {
            include snippets/fastcgi-php.conf;
            fastcgi_pass unix:/var/run/php/php8.3-fpm.sock;
            fastcgi_param SCRIPT_FILENAME $request_filename;
            include fastcgi_params;
        }
    }
}
EOF

# 사이트 활성화
ln -s /etc/nginx/sites-available/wp /etc/nginx/sites-enabled/

# 웹 디렉토리 권한 설정
chown -R dev:dev /home/dev/WEB/wp
chmod -R 755 /home/dev/WEB

# nginx 및 PHP-FPM 서비스 시작 (Docker 컨테이너에서는 service 명령어 사용)
service nginx start
service php8.3-fpm start
```

## 4. MySQL 서버 설치 및 설정

### 4.1. MySQL 서버 설치

```bash
apt install -y mysql-server
```

### 4.2. MySQL 초기 설정 및 보안 설정

```bash
# MySQL 서비스 시작 (Docker 컨테이너에서는 service 명령어 사용)
service mysql start

# MySQL 보안 설정 실행
mysql_secure_installation
```

**mysql_secure_installation 실행 시 응답 가이드:**
- VALIDATE PASSWORD COMPONENT 설치 여부: `n` (실습용이므로 간단한 비밀번호 허용)
- root 비밀번호 설정: `root123` 입력
- 비밀번호 확인: `root123` 다시 입력
- 익명 사용자 제거 여부: `y`
- 원격 루트 로그인 비활성화: `y`
- 테스트 데이터베이스 제거: `y`
- 권한 테이블 리로드: `y`

### 4.3. root 사용자에 비밀번호 인증 방식 설정

```bash
# MySQL에 접속
mysql

# MySQL 프롬프트에서 다음 명령어를 실행합니다:
# ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root123';
# FLUSH PRIVILEGES;
# EXIT;
```

**MySQL 프롬프트에서 실행할 명령어:**
```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'root123';
FLUSH PRIVILEGES;
EXIT;
```

## 5. phpMyAdmin 설치

### 5.1. phpMyAdmin 다운로드 및 설치

```bash
# dev 사용자로 전환
su - dev

# phpMyAdmin 다운로드 및 설치
cd /home/dev/WEB/wp
wget https://files.phpmyadmin.net/phpMyAdmin/5.2.2/phpMyAdmin-5.2.2-all-languages.zip
unzip phpMyAdmin-5.2.2-all-languages.zip
mv phpMyAdmin-5.2.2-all-languages mysql
rm phpMyAdmin-5.2.2-all-languages.zip

# 설정 파일 생성
cd mysql
cp config.sample.inc.php config.inc.php

# 설정 파일 수정 (blowfish_secret 설정)
BLOWFISH_SECRET=$(openssl rand -base64 24)
sed -i "s/\$cfg\['blowfish_secret'\] = '';/\$cfg['blowfish_secret'] = '$BLOWFISH_SECRET';/" config.inc.php

# 임시 디렉토리 생성
mkdir -p tmp
chmod 777 tmp

exit

# 권한 설정
chown -R dev:dev /home/dev/WEB/wp/mysql
```

## 6. WordPress 설치

### 6.1. WordPress 데이터베이스 및 사용자 생성

```bash
# MySQL에 접속하여 데이터베이스 및 사용자 생성
mysql -u root -proot123 << 'EOF'
CREATE DATABASE wordpress CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
CREATE USER 'wpuser'@'localhost' IDENTIFIED BY 'wppass123';
GRANT ALL PRIVILEGES ON wordpress.* TO 'wpuser'@'localhost';
FLUSH PRIVILEGES;
EOF
```

### 6.2. WordPress 다운로드 및 설치

```bash
# dev 사용자로 전환
su - dev

cd /home/dev/WEB/wp

# WordPress 다운로드
wget https://wordpress.org/latest.zip
unzip latest.zip

# WordPress 파일 이동 (mysql 디렉토리 보존)
if [ -d "mysql" ]; then
    mv mysql /tmp/mysql_backup
fi
mv wordpress/* .
rm -rf wordpress latest.zip
if [ -d "/tmp/mysql_backup" ]; then
    mv /tmp/mysql_backup mysql
fi

# WordPress 설정 파일 생성
cp wp-config-sample.php wp-config.php

# 설정 파일 수정
sed -i "s/database_name_here/wordpress/" wp-config.php
sed -i "s/username_here/wpuser/" wp-config.php
sed -i "s/password_here/wppass123/" wp-config.php

# 보안 키 설정
SECURITY_KEYS=$(curl -s https://api.wordpress.org/secret-key/1.1/salt/)
SECURITY_KEYS="${SECURITY_KEYS//\'/\\\'}"
SECURITY_KEYS="${SECURITY_KEYS//\//\\/}"
sed -i "/define( 'AUTH_KEY'/,/define( 'NONCE_SALT'/ d" wp-config.php
sed -i "/put your unique phrase here/a $SECURITY_KEYS" wp-config.php

exit

# 파일 권한 설정
chown -R dev:dev /home/dev/WEB/wp
find /home/dev/WEB/wp -type d -exec chmod 755 {} \;
find /home/dev/WEB/wp -type f -exec chmod 644 {} \;

# .htaccess 파일 생성
touch /home/dev/WEB/wp/.htaccess
chown dev:dev /home/dev/WEB/wp/.htaccess
chmod 644 /home/dev/WEB/wp/.htaccess
```

## 7. 단순 API 구성

### 7.1. api.php 파일 생성

```bash
# dev 사용자로 전환
su - dev

# API 파일 생성
cat > /home/dev/WEB/wp/api.php << 'EOF'
<?php
header('Content-Type: application/json; charset=utf-8');

function calculateSum($start, $end) {
    $sum = 0;
    for($i = $start; $i <= $end; $i++) {
        $sum += $i;
    }
    return $sum;
}

function calculateMultiply($a, $b) {
    return $a * $b;
}

// 요청 파라미터 받기
$req = $_GET['req'] ?? '';
$start = intval($_GET['start'] ?? 1);
$end = intval($_GET['end'] ?? 100);
$a = intval($_GET['a'] ?? 1);
$b = intval($_GET['b'] ?? 1);

$response = array();

switch($req) {
    case 'sum':
        $result = calculateSum($start, $end);
        $response = array(
            'status' => 'success',
            'operation' => 'sum',
            'start' => $start,
            'end' => $end,
            'result' => $result,
            'message' => "$start 부터 $end 까지의 합은 $result 입니다"
        );
        break;
        
    case 'multiply':
        $result = calculateMultiply($a, $b);
        $response = array(
            'status' => 'success',
            'operation' => 'multiply',
            'a' => $a,
            'b' => $b,
            'result' => $result,
            'message' => "$a 곱하기 $b 의 결과는 $result 입니다"
        );
        break;
        
    default:
        $response = array(
            'status' => 'error',
            'message' => '지원하지 않는 요청입니다. req=sum 또는 req=multiply를 사용하세요.',
            'examples' => array(
                'sum' => 'api.php?req=sum&start=1&end=100',
                'multiply' => 'api.php?req=multiply&a=5&b=10'
            )
        );
        break;
}

echo json_encode($response, JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT);
?>
EOF

exit

# 파일 권한 설정
chown dev:dev /home/dev/WEB/wp/api.php
chmod 644 /home/dev/WEB/wp/api.php
```

## 8. http://localhost 접속 절차

### 8.1. 서비스 상태 확인

```bash
# 모든 서비스 상태 확인 (Docker 컨테이너에서는 service 명령어 사용)
service nginx status
service php8.3-fpm status
service mysql status

# 또는 프로세스 확인
ps aux | grep nginx
ps aux | grep php-fpm
ps aux | grep mysql
```

### 8.2. 접속 테스트

1. **phpMyAdmin 접속**: http://localhost/mysql
   - 사용자명: `root`
   - 비밀번호: `root123`

2. **WordPress 설치**: http://localhost
   - WordPress 웹 설치 마법사 진행

3. **API 테스트**:
   - 합계 계산: http://localhost/api.php?req=sum&start=1&end=100
   - 곱셈 계산: http://localhost/api.php?req=multiply&a=5&b=10
   - API 도움말: http://localhost/api.php

### 8.3. 문제 해결

```bash
# nginx 로그 확인
tail -f /var/log/nginx/error.log

# PHP-FPM 로그 확인
tail -f /var/log/php8.3-fpm.log

# 포트 사용 확인
netstat -tlnp | grep :80
netstat -tlnp | grep :22
```

## 9. ngrok 서비스를 통한 외부 접속

### 9.1. ngrok가 필요한 이유

- **로컬 개발 환경의 외부 노출**: Docker 컨테이너에서 실행되는 웹 서비스를 인터넷을 통해 외부에서 접근할 수 있게 해줍니다.
- **HTTPS 터널링**: ngrok는 자동으로 HTTPS 터널을 생성하여 보안 연결을 제공합니다.
- **임시 도메인 제공**: 고정 IP나 도메인 없이도 임시 공개 URL을 제공받을 수 있습니다.
- **모바일 테스트**: 모바일 기기에서 개발 중인 웹사이트에 접근하여 테스트할 수 있습니다.
- **웹훅 테스트**: 외부 서비스의 웹훅을 로컬 환경에서 테스트할 수 있습니다.

### 9.2. ngrok 설치 및 설정

```bash
# ngrok 다운로드 및 설치
cd /tmp
wget https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz
tar -xzf ngrok-v3-stable-linux-amd64.tgz
mv ngrok /usr/local/bin/
chmod +x /usr/local/bin/ngrok
```

### 9.3. ngrok 토큰 설정

1. **ngrok 계정 생성**: https://ngrok.com 에서 무료 계정 생성
2. **토큰 확인**: Dashboard → Your Authtoken 메뉴에서 토큰 복사
3. **토큰 설정**:

```bash
# 토큰 설정 (YOUR_TOKEN을 실제 토큰으로 변경)
ngrok config add-authtoken YOUR_TOKEN
```

### 9.4. ngrok 서비스 시작

```bash
# HTTP 터널 시작 (백그라운드 실행)
ngrok http 80 --log=stdout > /tmp/ngrok.log 2>&1 &

# ngrok 상태 확인 (잠시 후 실행)
sleep 3
curl -s http://localhost:4040/api/tunnels | grep -o 'https://[^"]*\.ngrok-free\.app'
```

### 9.5. ngrok URL 확인 및 접속

```bash
# ngrok 웹 인터페이스 접속 (별도 터미널에서)
curl http://localhost:4040

# 또는 로그에서 URL 확인
tail -f /tmp/ngrok.log | grep "https://"
```

생성된 ngrok URL (예: https://abc123.ngrok-free.app)로 외부에서 접속 가능합니다.

## 10. 컨테이너 이미지화 및 재사용

### 10.1. 컨테이너를 이미지로 저장

```bash
# 호스트 시스템에서 실행 (새 터미널 창)
docker commit wordpress-dev wordpress-nginx-dev:v1.0
```

### 10.2. 저장된 이미지 확인

```bash
docker images | grep wordpress-nginx-dev
```

### 10.3. 새 컨테이너로 재실행

```bash
# 기존 컨테이너 중지 (필요시)
docker stop wordpress-dev

# 새 이미지로 컨테이너 실행
docker run -it --name wordpress-dev-new -p 22:22 -p 80:80 wordpress-nginx-dev:v1.0 /bin/bash

# 컨테이너 내에서 서비스 시작 (Docker 컨테이너에서는 service 명령어 사용)
service ssh start
service mysql start
service php8.3-fpm start
service nginx start
```

### 10.4. 자동 시작 스크립트 생성

```bash
# 컨테이너 내에서 자동 시작 스크립트 생성
cat > /usr/local/bin/start-services.sh << 'EOF'
#!/bin/bash
echo "서비스 시작 중..."

service ssh start
service mysql start
service php8.3-fpm start
service nginx start

echo "모든 서비스가 시작되었습니다."
echo "phpMyAdmin: http://localhost/mysql"
echo "WordPress: http://localhost"
echo "API: http://localhost/api.php"

# 서비스 상태 확인
echo ""
echo "=== 서비스 상태 ==="
service ssh status | grep -E "(Active|running)" || echo "SSH: 중지됨"
service mysql status | grep -E "(Active|running)" || echo "MySQL: 중지됨" 
service php8.3-fpm status | grep -E "(Active|running)" || echo "PHP-FPM: 중지됨"
service nginx status | grep -E "(Active|running)" || echo "nginx: 중지됨"
EOF

chmod +x /usr/local/bin/start-services.sh

# 서비스 시작
/usr/local/bin/start-services.sh
```

## 11. 주요 파일 경로 및 명령어 정리

### 11.1. 중요 경로
- 웹 루트: `/home/dev/WEB/wp`
- nginx 설정: `/etc/nginx/sites-available/wp`
- PHP-FPM 설정: `/etc/php/8.3/fpm/pool.d/www.conf`
- WordPress 설정: `/home/dev/WEB/wp/wp-config.php`
- phpMyAdmin: `/home/dev/WEB/wp/mysql`
- API 파일: `/home/dev/WEB/wp/api.php`

### 11.2. 자주 사용하는 명령어

```bash
# 서비스 재시작 (Docker 컨테이너에서는 service 명령어 사용)
service nginx restart
service php8.3-fpm restart
service mysql restart

# 서비스 시작/중지
service nginx start
service nginx stop
service mysql start
service mysql stop

# 로그 확인
tail -f /var/log/nginx/error.log
tail -f /var/log/mysql/error.log

# 권한 재설정
chown -R dev:dev /home/dev/WEB/wp
find /home/dev/WEB/wp -type d -exec chmod 755 {} \;
find /home/dev/WEB/wp -type f -exec chmod 644 {} \;

# 프로세스 확인
ps aux | grep nginx
ps aux | grep php-fpm
ps aux | grep mysql
```

### 11.3. API 테스트 URL 예시

```
# 기본 API 정보
http://localhost/api.php

# 합계 계산 (1부터 100까지)
http://localhost/api.php?req=sum&start=1&end=100

# 합계 계산 (50부터 150까지)
http://localhost/api.php?req=sum&start=50&end=150

# 곱셈 계산
http://localhost/api.php?req=multiply&a=12&b=15

# 잘못된 요청 (에러 메시지 확인)
http://localhost/api.php?req=invalid
```

이제 Docker 컨테이너 환경에서 nginx + MySQL + phpMyAdmin + WordPress가 설치되어 개발 준비가 완료되었습니다. VS Code Remote-SSH 또는 PuTTY를 통해 접속하여 코드를 편집하고, ngrok를 통해 외부에서도 접근할 수 있습니다.