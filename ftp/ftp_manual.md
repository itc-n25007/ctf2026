# vsftpdインストール

```bash
sudo apt update
sudo apt install vsftpd -y
```

起動

```bash
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
```

状態確認

```bash
sudo systemctl status vsftpd
```
または

```bash
sudo ss -tlnp | grep :21
```

接続確認

ftp localhost
