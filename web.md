# Webサーバ構築マニュアル（Apache + Basic認証）

## 1. Apacheインストール

```bash
sudo apt update
sudo apt install apache2 apache2-utils -y
```

## 2. Apache起動

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

確認：
```bash
sudo systemctl status apache2
```

## 3. Webroot確認
```bash
/var/www/html
```

## 4. Basic認証設定
### 4-1. ユーザー作成
```bash
sudo htpasswd -c /etc/apache2/.htpasswd user1
```

### 4-2. Apache設定変更
```bash
sudo vi /etc/apache2/sites-available/000-default.conf
```

追加内容：
<VirtualHost *:80> の中に以下を追加する。
```apache
<Directory /var/www/html>
    AuthType Basic
    AuthName "Restricted Area"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
```

## 5. Apache再起動
```bash
sudo systemctl restart apache2
```

## 6. 動作確認
### 認証なしでアクセス
```bash
curl http://localhost
```
認証がかかっていれば、401 Unauthorizedになる。

### 認証ありでアクセス
```bash
curl -u user1:password http://localhost
```
認証成功でHTMLが表示される。

## 7.ブラウザで確認の場合
```
http://<IPアドレス>
```
アクセス時にユーザー名とパスワードの入力画面が表示されれば成功。









