# Bài 3 — HTTP Basic Authentication với Nginx

## Tệp cấu hình

- `ptit-web.conf`: server block HTTP port 80; bảo vệ cả `/admin` và `/admin/` bằng Basic Auth.
- `html/`: website tĩnh và trang quản trị.
- `.htpasswd`: thông tin `admin_user` với mật khẩu APR1 hash, đặt ngoài thư mục web root.

Đặt `.htpasswd` tại `/etc/nginx/.htpasswd` và `ptit-web.conf` tại `/etc/nginx/sites-available/ptit-web.conf`. Chép nội dung `html/` vào `/var/www/ptit-web/html/`, bật site bằng symlink trong `sites-enabled`, bỏ kích hoạt site mặc định, kiểm tra bằng `sudo nginx -t` rồi reload Nginx.

Tài khoản thực hành: `admin_user` — mật khẩu `Ptit-Admin-2026!`.

Kiểm tra xác thực:

```bash
curl -I http://<IP_ADDRESS_DROPLET>/admin
curl -u 'admin_user:Ptit-Admin-2026!' http://<IP_ADDRESS_DROPLET>/admin/
```

Yêu cầu đầu tiên trả `401` kèm `WWW-Authenticate`; yêu cầu có thông tin hợp lệ trả trang quản trị. Khi dùng trên máy chủ thật, hãy thay mật khẩu mẫu bằng mật khẩu riêng và tạo lại hash bằng `htpasswd -cB /etc/nginx/.htpasswd admin_user`.
