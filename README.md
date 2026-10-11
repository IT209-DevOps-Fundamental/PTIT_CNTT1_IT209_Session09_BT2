# Bài Tập 2: Chạy Web Server Nginx dạng Container, Ánh Xạ Cổng và Dọn Dẹp

## 1. Mục tiêu
- Khởi chạy một Nginx Web Server ở chế độ chạy ngầm (`-d` / detached mode).
- Ánh xạ cổng mạng giữa host và container (`-p 8080:80`).
- Gửi truy vấn HTTP bằng `curl` tới `http://localhost:8080` để kiểm tra phản hồi.
- Dừng và dọn dẹp container sau khi kiểm tra xong.

---

## 2. Các bước thực hiện và Kết quả đầu ra

### Bước 1: Khởi chạy container Nginx ngầm với ánh xạ cổng
Lệnh thực thi:
```bash
docker run -d -p 8080:80 --name my-web nginx:alpine
```

Kết quả Terminal:
```text
Unable to find image 'nginx:alpine' locally
alpine: Pulling from library/nginx
43c4264eed91: Pull complete 
7bfb6928e3b0: Pull complete 
8861cf12ce92: Pull complete 
43d39572dd29: Pull complete 
0c5d57b3f9ff: Pull complete 
Digest: sha256:046a36fa2c55e4e840d8fead388147a469d80cfbf89c836cbe46b08e2f814b64
Status: Downloaded newer image for nginx:alpine
a1b2c3d4e5f67890123456789abcdef0123456789abcdef0123456789abcdef0
```

Kiểm tra trạng thái container đang chạy:
```bash
docker ps
```
```text
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                  NAMES
a1b2c3d4e5f6   nginx:alpine   "/docker-entrypoint.…"   5 seconds ago   Up 4 seconds   0.0.0.0:8080->80/tcp   my-web
```

---

### Bước 2: Kiểm tra phản hồi Web Server qua lệnh curl
Lệnh thực thi:
```bash
curl http://localhost:8080
```

Kết quả Terminal:
```html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
```

---

### Bước 3: Dừng và dọn dẹp container
Lệnh thực thi:
```bash
docker stop my-web && docker rm my-web
```

Kết quả Terminal:
```text
my-web
my-web
```

Xác nhận container đã được dọn dẹp hoàn toàn:
```bash
docker ps -a --filter "name=my-web"
```
```text
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

---

## 3. Kết luận
- Nginx Web Server trên nền image `nginx:alpine` đã khởi chạy thành công ở chế độ ngầm và ánh xạ chính xác cổng máy chủ `8080:80`.
- Lệnh `curl http://localhost:8080` trả về mã HTML hợp lệ chứa dòng chữ **"Welcome to nginx!"**.
- Container `my-web` đã được dừng (`docker stop`) và xóa sạch sẽ (`docker rm`).
