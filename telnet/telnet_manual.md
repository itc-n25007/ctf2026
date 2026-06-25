# Telnetサーバ構築

sudo apt update
sudo apt install xinetd telnetd -y

サービス起動

sudo systemctl restart xinetd

接続確認

telnet サーバIPアドレス
