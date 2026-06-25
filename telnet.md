# Telnetサーバ構築マニュアル（telnetd）

## 1. telnetdインストール

```bash
sudo apt update
sudo apt install telnetd -y
```

## 2. inetdの状態確認

telnetdはサービスをうけるのにinetd(スーパーデーモン)を利用する。
TCP23の待ち受けはinetdが実施し、実際にパケットが来たタイミングでinetdがtelnetdを起動する仕組みになっているため、inetd が現在起動しているかどうかを確認する。
```bash
sudo systemctl status inetd
```

## 3. telnetサービス設定確認
設定ファイル /etc/inetd.conf を確認する。
```bash
sudo vi /etc/inetd.conf
```

以下の行が有効になっているかを確認する。
```conf
telnet stream tcp nowait telnetd /usr/sbin/tcpd /usr/sbin/telnetd
```
先頭に、`#<off>#`がついてた場合は削除する。

## 4. inetd再起動
設定を反映するため、`inetd` を再起動する。
```bash
sudo systemctl restart inetd
```

確認：
```bash
sudo systemctl status inetd
```

## 5. ポート確認

telnetは23番ポートを使用するため、待ち受け状態を確認する。
```bash
sudo ss -tlnp | grep :23
```
`*:23`を`inetd`が待ち受けていれば成功。

## 6. telnet接続確認

### 同じマシンから接続する場合
```bash
telnet localhost
```

### 別のマシンから接続する場合
```bash
telnet <IPアドレス>
```

ログイン時には、Ubuntu側に存在するユーザ名とパスワードを入力する。
Vagrant環境の場合、ユーザー名：vagrant、パスワード：vagrant　となっている。



