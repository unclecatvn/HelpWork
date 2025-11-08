# Hướng Dẫn Cài Đặt Odoo 18

## Giới Thiệu

Odoo 18 là phiên bản mới nhất của hệ thống ERP/CRM mã nguồn mở. Hướng dẫn này cung cấp các bước cài đặt Odoo 18 trên các hệ điều hành khác nhau.

## Cài Đặt Trên Ubuntu/Debian

### 1. Cập Nhật Hệ Thống

```bash
sudo apt update && sudo apt upgrade -y
```

### 2. Cài Đặt Các Gói Phụ Thuộc

```bash
sudo apt install -y \
  git \
  python3 \
  python3-pip \
  python3-dev \
  python3-venv \
  postgresql \
  postgresql-contrib \
  libxml2-dev \
  libxslt1-dev \
  libjpeg-dev \
  zlib1g-dev \
  libpq-dev \
  libssl-dev \
  libffi-dev \
  libblas-dev \
  liblapack-dev \
  libatlas-base-dev \
  npm \
  wkhtmltopdf
```

### 3. Khởi Tạo PostgreSQL

```bash
# Bắt đầu PostgreSQL
sudo service postgresql start

# Đăng nhập vào PostgreSQL
sudo -u postgres psql

# Tạo user cho Odoo
CREATE USER odoo WITH PASSWORD 'password123';
ALTER USER odoo CREATEDB;
\q
```

### 4. Tạo Thư Mục Odoo

```bash
# Tạo thư mục
sudo mkdir -p /opt/odoo
sudo chown -R $USER:$USER /opt/odoo
cd /opt/odoo
```

### 5. Tải Odoo 18

```bash
# Clone từ GitHub (Community Edition)
git clone https://github.com/odoo/odoo.git -b 18.0 --depth 1

# Hoặc tải phiên bản Enterprise
# Yêu cầu quyền truy cập từ Odoo
cd odoo
```

### 6. Tạo Virtual Environment

```bash
python3 -m venv venv
source venv/bin/activate
```

### 7. Cài Đặt Python Dependencies

```bash
pip install --upgrade pip
pip install -r requirements.txt
pip install wkhtmltopdf  # Hoặc python-pptx
```

### 8. Cài Đặt Node Dependencies

```bash
npm install -g rtlcss
```

### 9. Tạo File Cấu Hình

```bash
# Tạo thư mục config
mkdir -p ~/.config/odoo
touch ~/.config/odoo/odoo.conf
```

**Nội dung `odoo.conf`:**

```ini
[options]
; Cơ sở dữ liệu
db_host = localhost
db_port = 5432
db_user = odoo
db_password = password123
db_name = odoo_18

; Thư mục add-ons
addons_path = /opt/odoo/odoo/addons,/opt/odoo/custom_addons

; Server
http_port = 8069
xmlrpc_port = 8071
workers = 4
max_cron_threads = 2

; Logging
logfile = /tmp/odoo.log
log_level = info

; Security
admin_passwd = admin_password_123
```

### 10. Khởi Động Odoo

```bash
# Chạy trực tiếp
python -m odoo.bin --config ~/.config/odoo/odoo.conf

# Hoặc chạy dạng nền
nohup python -m odoo.bin --config ~/.config/odoo/odoo.conf > /tmp/odoo.log 2>&1 &
```

## Kiểm Tra và Khởi Động

### 1. Kiểm Tra Kết Nối Database

```bash
# Kích hoạt virtual environment
source /opt/odoo/venv/bin/activate

# Test connection
python -c "import psycopg2; conn = psycopg2.connect('dbname=odoo_18 user=odoo password=password123'); print('✓ Connection OK')"
```

### 2. Kiểm Tra Dependencies

```bash
python -m pip check
```

### 3. Khởi Tạo Database

```bash
python -m odoo.bin -d odoo_18 --init=base --without-demo
```

### 4. Truy Cập Web Interface

```
URL: http://localhost:8069
Admin Email: admin
Password: admin
```

---

## Vấn Đề Thường Gặp & Giải Pháp

### 1. Lỗi: Port 8069 đã được sử dụng

```bash
# Tìm process sử dụng port
lsof -i :8069

# Kill process
kill -9 <PID>

# Hoặc dùng port khác
python -m odoo.bin --http-port 8070
```

## Tối Ưu Performance

### 1. Cấu Hình Workers

```ini
workers = 4  ; số lõi CPU x 2
max_cron_threads = 2
```

### 2. Cấu Hình Database

```sql
-- Kết nối max
ALTER SYSTEM SET max_connections = 200;
-- Connection pool
ALTER SYSTEM SET shared_buffers = '256MB';
ALTER SYSTEM SET effective_cache_size = '1GB';

-- Apply
sudo service postgresql restart
```

### 3. Sử Dụng Reverse Proxy (Nginx)

```nginx
upstream odoo_backend {
    server localhost:8069;
}

server {
    listen 80;
    server_name odoo.example.com;

    proxy_pass http://odoo_backend;
    proxy_set_header Host $host;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Forwarded-Proto $scheme;
}
```

---

## Backup & Restore

### 1. Backup Database

```bash
pg_dump -U odoo odoo_18 > backup_odoo_18_$(date +%Y%m%d).sql
```

### 2. Backup Đầy Đủ (Với Filestore)

```bash
tar -czf odoo_backup_$(date +%Y%m%d).tar.gz \
  /opt/odoo/odoo/.local/share/Odoo/filestore/odoo_18 \
  backup_odoo_18_$(date +%Y%m%d).sql
```

### 3. Restore Database

```bash
psql -U odoo odoo_18 < backup_odoo_18_20240101.sql
```

---

## Tham Khảo & Liên Kết Hữu Ích

- [Odoo 18 Official Docs](https://www.odoo.com/documentation/18.0/)
- [GitHub Odoo](https://github.com/odoo/odoo)
