### MYSQL 접속
```shell
mysql -h localhost -u root -p

cd /usr/local/mysql/bin
./mysql -uroot -p
```

### 데이터베이스 생성하기
```sql
CREATE DATABASE IF NOT EXISTS mysql;
CREATE SCHEMA 'mysql' DEFAULT CHARACTER SET utf8; // 한글 사용 가능
```

### 테이블 생성하기
```sql
use mysql;

CREATE TABLE IF NOT EXISTS users (
  id INT(30) NOT NULL AUTO_INCREMENT,
  title VARCHAR(255) NOT NULL,
  img_path VARCHAR(255) NOT NULL,
  explanation VARCHAR(255) NOT NULL,
  PRIMARY KEY(id)
);

CREATE TABLE IF NOT users (
  id INT(30) NOT NULL AUTO_INCREMENT,
  name VARCHAR(20) NOT NULL,
  title VARCHAR(255) NOT NULL,
  age INT UNSIGNED NOT NULL,
  married TINYINT NOT NULL,
  comment TEXT NULL,
  img_path VARCHAR(255) NOT NULL,
  explanation VARCHAR(255) NOT NULL,
  created_at DATETIME NOT NULL DEFAULT now(),
  PRIMARY KEY(id),
  UNIQUE INDEX name_UNIQUE (name ASC)) // 여기서 끝나
  COMMENT = '사용자 정보'
  DEFAULT CHARACTER SET utf8;
  ENGINE = InnoDB;
);
```

### 테이블 확인
```sql
DESC users;

SHOW TABLES;
SHOW DATABASES;
```

### 테이블 제거
```sql
DROP TABLE users;
```

### 데이터 삽입, 업데이트, 변경, 삭제, 조회
```sql
-- 삽입
INSERT INTO users (title, img_path, explanation) VALUES ('', '', '');

-- 업데이트
UPDATE users SET explanation="Choose you favorite Taylor Swift's song" WHERE id = 4;

-- 삭제
DELETE FROM users WHERE id = 5;

-- 조회
SELECT * FROM users;
SELECT id, title FROM users WHERE married = 1 AND(OR) age > 30;
SELECT id, title FROM users ORDER BY age DESC LIMIT 1 OFFSET 1;
```

### 테이블 변경
```sql
-- 칼럼 추가
ALTER TABLE users ADD names TEXT NOT NULL AFTER explanation;

-- 칼럼 이름
ALTER TABLE users CHANGE id user_id INT(30) NOT NULL AUTO_INCREMENT;

-- 칼럼 조건 변경
ALTER TABLE users MODIFY sub TEXT;
```
