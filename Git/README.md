
# Hướng dẫn sử dụng Git

## 1. Sử dụng Git cơ bản

- **Link tải Git**: [Git Installation Guide](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
- **Kiểm tra version**: 
  ```bash
  git --version
  ```
- **Sao chép kho lưu trữ về máy**: 
  ```bash
  git clone [repository-url]
  ```
- **Khởi tạo kho lưu trữ cục bộ**: 
  ```bash
  git init
  ```
- **Thêm thay đổi vào stage**: 
  ```bash
  git add .
  ```
- **Commit các thay đổi**: 
  ```bash
  git commit -m "Initial Commit"
  ```
- **Đẩy code lên nhánh từ xa**: 
  ```bash
  git push origin <branch>
  ```
- **Tạo và chuyển sang nhánh mới**:
  ```bash
  git branch <branch>
  git checkout <branch>
  ```
- **Lấy code mới nhất từ nhánh**: 
  ```bash
  git pull origin <branch>
  ```

<br>

## 2. Cấu hình Git

- **Cấu hình username và email**:
  ```bash
  git config --global user.name "<username>"
  git config --global user.email "<mailaddress>"
  ```
- **Kiểm tra cấu hình tài khoản**:
  ```bash
  git config --global --list
  ```

<br>

## 3. Stash code để rebase với develop

- **Chuyển các thay đổi vào stash**:
  ```bash
  git stash -m "message"
  ```
- **Rebase code từ develop**:
  ```bash
  git pull --rebase origin develop
  ```
- **Lấy lại các thay đổi từ stash và xóa stash**:
  ```bash
  git stash pop
  ```
- **Lưu các thay đổi vào stage và commit**:
  ```bash
  git add .
  git commit -m "message"
  ```
- **Đẩy code lên nhánh từ xa**:
  ```bash
  git push origin <branch>
  ```

<br>

## 4. Quản lý Remote Repository

- **Thay đổi URL của remote origin hiện tại**:
  ```bash
  git remote set-url origin https://github.com/unclecatvn/BaseJava.git
  ```
- **Xóa remote origin và thêm lại**:
  ```bash
  git remote remove origin
  git remote add origin https://github.com/unclecatvn/BaseJava.git
  ```
- **Kiểm tra các remote hiện tại**:
  ```bash
  git remote -v
  ```
- **Thiết lập nhánh chính khi đẩy code**:
  ```bash
  git push -u origin main
  ```