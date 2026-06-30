# Telnetサーバ構築

パッケージ一覧を更新

```bash
sudo apt update
```

Telnetサーバーをインストール

```bash
sudo apt install telnetd -y
```

viでファイル/etc/inetd.conを開く

```bash
sudo vi /etc/inetd.conf
```

ファイルに次の行を追加

telnet  stream  tcp     nowait  root    /usr/sbin/tcpd  /usr/sbin/telnetd

inetd.conf設定ファイルを保存して、inetdサービスを再起動

```bash
sudo systemctl restart inetd
```

インストールが完了したら、次のコマンドを使用してTelnetサービスの状態を確認できます
特に見てほしいところActive: active(running)になっているか

```bash
sudo systemctl status inetd
```

接続確認

別マシンの場合

```bash
telnet サーバIPアドレス
```

同じマシンの場合
```bash
telnet localhost
```
