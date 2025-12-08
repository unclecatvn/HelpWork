# Sổ tay hướng dẫn cho Developer (Developer Handbook)

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![Laravel](https://img.shields.io/badge/Laravel-FF2D20?style=for-the-badge&logo=laravel&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![Odoo](https://img.shields.io/badge/Odoo-714B67?style=for-the-badge&logo=odoo&logoColor=white)

Repo này tổng hợp các hướng dẫn, cheat sheet và các lưu ý quan trọng cho công việc lập trình hàng ngày.

## Mục lục

- [1. Docker & WSL](#1-docker--wsl)
- [2. Git](#2-git)
- [3. PHP & Laravel](#3-php--laravel)
- [4. Node.js](#4-nodejs)
- [5. Odoo](#5-odoo)
- [Cập nhật gần đây](#cập-nhật-gần-đây)
- [Đóng góp](#đóng-góp)
- [Tác giả](#tác-giả)

---

## 1. Docker & WSL
[Truy cập hướng dẫn chi tiết](Docker/README.md)

Hướng dẫn bao gồm:
- Cài đặt WSL (Windows Subsystem for Linux)
- Cài đặt Docker trên Windows/WSL
- Các lệnh Docker thường dùng (ps, images, run, stop, rm...)
- Cài đặt các công cụ hỗ trợ (Make, Windows Terminal, Cursor)

## 2. Git
[Truy cập hướng dẫn chi tiết](Git/README.md)

Hướng dẫn bao gồm:
- Các lệnh Git cơ bản (clone, init, add, commit, push, pull...)
- Clone theo nhánh cụ thể (`git clone -b <branch>`)
- Cấu hình Git (username, email)
- Các kỹ thuật nâng cao: Squash commit, Stash, Rebase interactive
- Quản lý Remote Repository
- Cấu hình SSH Key cho GitHub/GitLab

## 3. PHP & Laravel
[Truy cập hướng dẫn chi tiết](PHP/README.md)

Hướng dẫn bao gồm:
- Cài đặt và sử dụng Composer
- Cấu hình file .env
- Tích hợp Node.js trong dự án Laravel
- Sử dụng Laravel Mix để build assets

## 4. Node.js
[Truy cập hướng dẫn chi tiết](Nodejs/README.md)

Hướng dẫn bao gồm:
- Link tải Node.js
- Khắc phục lỗi "running scripts is disabled" trên PowerShell (Windows)

## 5. Odoo
[Truy cập hướng dẫn chi tiết](Odoo/README.md)

Hướng dẫn bao gồm:
- Cài đặt Odoo 18 trên Ubuntu/Debian
- Cài đặt các dependencies và PostgreSQL
- Cấu hình file `odoo.conf`
- Các lệnh tạo database và quản lý service
- Tối ưu performance và backup/restore

---

## Cập nhật gần đây

| Ngày | Nội dung |
|------|----------|
| 2025-12-08 | Thêm hướng dẫn clone theo nhánh cụ thể (Git) |
| 2025-12-08 | Cập nhật README với mô tả chi tiết |
| 2025-12-05 | Thêm hướng dẫn tạo database Odoo 18 |

---

## Đóng góp

Bạn muốn đóng góp thêm nội dung? Hãy làm theo các bước sau:

1. **Fork** repo này
2. **Tạo nhánh mới** cho feature của bạn:
   ```bash
   git checkout -b feature/ten-huong-dan-moi
   ```
3. **Thêm nội dung** vào thư mục tương ứng hoặc tạo thư mục mới
4. **Commit** thay đổi:
   ```bash
   git commit -m "Thêm hướng dẫn [tên hướng dẫn]"
   ```
5. **Push** và tạo **Pull Request**

### Quy tắc đóng góp
- Sử dụng tiếng Việt cho nội dung hướng dẫn
- Mỗi công nghệ/chủ đề nên có một thư mục riêng với file `README.md`
- Sử dụng Markdown chuẩn
- Thêm ví dụ code khi có thể

---

## Tác giả

👤 **UncleCat**

- GitHub: [@unclecatvn](https://github.com/unclecatvn)

---

⭐ Nếu repo này hữu ích, hãy cho một star nhé!
