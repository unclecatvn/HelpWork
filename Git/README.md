# Huống dẫn sử dụng git

## 1. Sử dụng git cơ bản

- Link tải trang: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
- Kiểm tra version: git --version
- Sao chép kho lữu trữ về máy tính của bạn: git clone [repository url]
- Lệnh git init sẽ thêm kho lưu trữ Git cục bộ vào dự án.
- Thêm toàn bộ những thay đổi ở source code: git add .
- Sử dụng câu lệnh sau để commit file: git commit -m "Initial Commit"
- Đẩy code lên nhánh git push origin <branch>
- Nếu chưa có nhánh, tạo nhánh mới: git branch test và chuyển sang nhánh mong muốn: git checkout <branch>
- Lấy code từ kho lưu trữ: git pull origin <branch>

<br>
<br>

## 2. Config git

- git config --global user.name "<username>"
- git config --global user.email "<mailaddress>"
- Xem tài khoản git: git config --global --list

<br>
<br>

## 3. Stash code để rebase code develop

- Nếu có thay đổi -> chuyển hết vào stash : git stash -m "message"
- Chạy lệnh rebase code từ develop: git pull --rebase origin develop
- Lấy những thay đổi vừa lưu vào stash và xóa stash: git stash pop
- Lưu các thay đổi vào stage: git add .
- Lệnh commit: git commit -m "message"
- Đẩy code lên nhánh: git push origin <branch>

### 1. Linh tinh

- Thay đổi URL của remote origin hiện tại:

```
git remote set-url origin https://github.com/unclecatvn/BaseJava.git
```

- Xóa remote origin hiện tại và thêm lại:

```
git remote remove origin
git remote add origin https://github.com/unclecatvn/BaseJava.git
```

- Kiểm tra các remote hiện có:

```
git remote -v
git push -u origin main
```
