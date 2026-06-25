# FTPサーバ構築マニュアル（vsftpd）

## 1. vsftpdインストール

```bash
sudo apt update
sudo apt install vsftpd -y
```

## 2. vsftpdの状態確認

vsftpd が現在起動しているかどうかを確認する。
```bash
sudo systemctl status vsftpd
```

## 3. vsftpd起動

vsftpd が停止している場合は起動する。
```bash
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
```
### 起動後の確認

```bash
sudo systemctl status vsftpd
```

## 4. ポート確認
```bash
sudo ss -tlnp | grep :21
```
`*:21`を`vsftpd`が待ち受けていれば成功。

## 5. クライアントから接続確認

### FTPクライアントが未インストールの場合
```bash
sudo apt install ftp -y
```

接続：
```bash
ftp localhost
```
ログイン時には、Ubuntu側に存在するユーザ名とパスワードを入力する。
Vagrant環境の場合、ユーザー名：vagrant、パスワード：vagrant　となっている。




