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
- **Sao chép một nhánh cụ thể**:
  ```bash
  git clone -b <branch_name> [repository-url]
  # Hoặc dùng --branch (tương đương với -b)
  git clone --branch <branch_name> [repository-url]
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

## 3. Git hay dùng

### 1. Squash commit

```bash
  git add .
  git commit --amend --no-edit
  git push --force-with-lease
```

### 2. Xoá tất cả stash

```bash
  git stash clear
```

### 3. Xoá stash mới nhất

```bash
  git stash drop
```

### 4. Xoá stash cụ thể (Ví dụ stash@{0})

```bash
  git stash drop stash@{0}
```

### 5. Apply và drop stash cụ thể (ví dụ stash@{1})

```bash
  git stash pop stash@{1}
```

### 6. Rebase interactive để chỉnh sửa commit (xóa, sửa, squash, reorder)

```bash
git rebase -i HEAD~2
```

**Chi tiết cách thực hiện:**

Sau khi chạy lệnh trên, một editor (thường là vim hoặc nano) sẽ mở ra với nội dung tương tự như này:

```
pick 1a2b3c4 [IMP] dtg_sale_report: Add COD report. (#1249)
pick 5d6e7f8 [IMP] Improved invoice and transaction update process

# Rebase 9g8h7i6..5d6e7f8 onto 9g8h7i6 (2 commands)
#
# Commands:
# p, pick <commit> = use commit
# r, reword <commit> = use commit, but edit the commit message
# e, edit <commit> = use commit, but stop for amending
# s, squash <commit> = use commit, but meld into previous commit
# f, fixup <commit> = like "squash", but discard this commit's log message
# x, exec <command> = run command (the rest of the line) using shell
# b, break = stop here (continue rebase later with 'git rebase --continue')
# d, drop <commit> = remove commit
# l, label <name> = label current HEAD with a name
# t, reset <name> = reset HEAD to a label
# m, merge [-C <commit> | -c <commit>] <label> [# <oneline>]
```

**Để loại bỏ commit không mong muốn:**

1. Thay đổi `pick` thành `drop` cho commit muốn xóa:

   ```
   drop 1a2b3c4 [IMP] dtg_sale_report: Add COD report. (#1249)
   pick 5d6e7f8 [IMP] Improved invoice and transaction update process
   ```

2. Lưu và thoát:

   - **Nếu dùng vim**: Nhấn `Esc`, gõ `:wq`, nhấn `Enter`
   - **Nếu dùng nano**: Nhấn `Ctrl+X`, nhấn `Y`, nhấn `Enter`

3. Đẩy thay đổi lên remote:
   ```bash
   git push origin <branch_name> --force
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

<br>

## 5. Cấu hình SSH cho Git

### 1. Tạo SSH key mới

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

**Lưu ý**: Nhấn Enter để sử dụng đường dẫn mặc định (`~/.ssh/id_ed25519`)

### 2. Thêm SSH key vào SSH agent

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### 3. Sao chép public key để thêm vào GitHub/GitLab

```bash
cat ~/.ssh/id_ed25519.pub
```

**Lưu ý**: Copy toàn bộ nội dung hiển thị (từ `ssh-ed25519` hoặc `ssh-rsa` đến cuối)

### 4. Thêm SSH key vào GitHub

1. Vào **Settings** → **SSH and GPG keys**
2. Click **New SSH key**
3. Dán public key đã copy vào
4. Click **Add SSH key**

### 5. Kiểm tra kết nối SSH với GitHub

```bash
ssh -T git@github.com
```

**Kết quả mong đợi**: "Hi username! You've successfully authenticated..."

### 6. Clone repository qua SSH

```bash
git clone git@github.com:username/repository.git
```

### 7. Thay đổi remote URL từ HTTPS sang SSH

```bash
git remote set-url origin git@github.com:username/repository.git
```

Hoặc xóa và thêm lại:

```bash
git remote remove origin
git remote add origin git@github.com:username/repository.git
```

### 8. Kiểm tra remote URL hiện tại

```bash
git remote -v
```
