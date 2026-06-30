# Apache Webサーバ構築

## Apacheのインストール

```bash
sudo apt update
sudo apt install apache2 -y
```

## 起動確認

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
sudo systemctl status apache2
```

ブラウザで以下のURLにアクセスし、「Apache2 Ubuntu Default Page」が表示させる

```bash
http://<サーバーIP>
```

## Basic認証設定

```bash
sudo apt install apache2-utils -y
```

パスワードファイル作成
例:ユーザー名をstudentにする場合

```bash
sudo htpasswd -c /etc/apache2/.htpasswd student
```

内容確認
暗号化されたパスワードが表示させる

```bash
cat /etc/apache2/.htpasswd
```

設定ファイル編集

```bash
sudo vi /etc/apache2/sites-available/000-default.conf
```

<VirtualHost *:80>の中に以下を追加

```bash
<Directory /var/www/html>
    AuthType Basic
    AuthName "Restricted Area"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>
```

Apache設定の確認

```bash
sudo apachectl configtest
```

結果

Syntax OK

再起動

```bash
sudo systemctl restart apache2
```

動作確認
ブラウザで以下のURLを入力

http://192.168.xx.xx

アクセスすると、

Username:
Password:

の認証画面が表示

作成した

ユーザー名: student
パスワード:設定したもの

でログインできれば成功

index.htmlを作成（任意）

```bash
echo "<h1>hello</h1>" | sudo tee /var/www/html/index.html
```

アクセスすると

hello

が表示される

認証画面が表示されない場合
Apacheで<Directory>の設定を反映するには、ディレクトリ設定が有効になっていることを確認

```bash
sudo apache2ctl -s
```

または、設定ファイルに誤りがないか確認

```bash
sudo apachectl configtest
```

さらにログを確認すると原因がわかることがある

```bash
sudo journalctl -u apache2
```

または

```bash
sudo tail -f /var/log/apache2/error.log
```

