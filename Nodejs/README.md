# Hướng dẫn sử dụng nodejs

<table style="width:100%;">
  <thead>
    <tr>
      <th> </th>
      <th>Đường dẫn</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Tải nodejs</td>
      <td><a href="https://nodejs.org/en">Download</a></td>
    </tr>
  </tbody>
</table>

## Các lỗi thường gặp:

### Lỗi 1:

npm : File C:\Program Files\nodejs\npm.ps1 cannot be loaded because running scripts is disabled on this system. For more information, see
about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:1

- npm run watch
- - CategoryInfo : SecurityError: (:) [], PSSecurityException
  - FullyQualifiedErrorId : UnauthorizedAccess

> Cách khắc phục

#### 1. **Mở PowerShell với quyền Administrator**

- Nhấn **Windows + S**, tìm **PowerShell**.
- Chuột phải vào **Windows PowerShell** và chọn **Run as Administrator**.

#### 2. **Kiểm tra Execution Policy hiện tại**

```
Get-ExecutionPolicy -List
```

Nếu bạn thấy chính sách hiện tại là **Restricted**, đó là nguyên nhân gây ra lỗi.

#### 3. **Thay đổi Execution Policy**

```
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

- **RemoteSigned**: Cho phép chạy các script được tạo cục bộ mà không cần ký, nhưng các script tải về từ Internet cần phải được ký.
- Khi được hỏi xác nhận, gõ **A** (Yes to All) để đồng ý.

#### 4. **Kiểm tra lại chính sách**

```
Get-ExecutionPolicy
```

Kết quả nên là **RemoteSigned**.

#### 5. **Chạy lại lệnh**

Sau khi hoàn thành các bước trên, đóng PowerShell và mở lại **Command Prompt** hoặc **PowerShell**. Sau đó chạy lại:

```
npm run watch
```

#### Giải thích thêm về Execution Policies

- **Restricted**: Không cho phép chạy bất kỳ script nào.
- **RemoteSigned**: Script tạo cục bộ có thể chạy, nhưng script từ Internet cần ký.
- **Unrestricted**: Tất cả các script đều có thể chạy, nhưng sẽ có cảnh báo cho script tải về từ Internet.
