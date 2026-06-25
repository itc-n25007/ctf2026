# Apache Webサーバ構築

## Apacheのインストール

sudo apt update
sudo apt install apache2 -y

## 起動確認
sudo systemctl start apache2
sudo systemctl enable apache2

## Basic認証設定

sudo apt install apache2-utils

パスワードファイル作成

sudo htpasswd -c /etc/apache2/.htpasswd student

設定ファイル編集

sudo vi /etc/apache2/sites-available/000-default.conf

<Directory /var/www/html>
    AuthType Basic
    AuthName "Restricted Area"
    AuthUserFile /etc/apache2/.htpasswd
    Require valid-user
</Directory>

モジュール有効化

sudo a2enmod auth_basic

再起動

sudo systemctl restart apache2

