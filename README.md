# Cài đặt Docker trên Windows WSL

## 1. Cài đặt WSL

- Truy cập link sau và làm theo hướng dẫn, thực hiện đến Step 5, không làm theo Step 6 trở đi

- https://learn.microsoft.com/en-us/windows/wsl/install-manual#step-1---enable-the-windows-subsystem-for-linux

<br>
<br>

## 2. Tạo thư mục lưu máy ảo WSL

- 2.1. Sử dụng email công ty, tải file zip sau: https://drive.google.com/file/d/1dXRJ72S7PFdNbOwPlcgu4nk3p6thcoH_/view?usp=drive_link

- 2.2. Tạo thư mục để lưu máy ảo WSL, ví dụ `D:\WSL`

- 2.3. Giải nén file zip trên, copy file `install.tar.gz` và `ubuntu.exe` vào thư mục vừa tạo (VD là `D:\WSL`)

- 2.4. Chạy file `ubuntu.exe` để cài đặt ubuntu vào WSL

- 2.5 Màn hình hiện yêu cầu **Enter new UNIX username** thì nhập tên cho máy Ubuntu (Không dùng ký tự viết hoa)

- 2.6 Nhập lại mật khẩu 2 lần

- 2.7 Chạy `sudo apt update` và `sudo apt upgrade` để cập nhật Ubuntu

- 2.8 Thêm user hiên tại vào nhóm sudo: `sudo usermod -aG sudo $USER`

- Nếu mỗi lần sử dụng git lại phải nhập lại username/password. <br>
Chạy lệnh `git config --global credential.helper store` <br>
Sẽ chỉ cần nhập username/password một lần và lưu trong store để sử dụng cho các lần sau

<br>
<br>

## 3. Cài đặt Docker

- Truy cập link sau và thực hiện đầy đủ theo phần **Uninstall old versions** và **Install using the apt repository**

- https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

- Check docker: `docker --version`

- Thêm user hiện tại vào nhóm docker: `sudo usermod -aG docker $USER`

- Check docker-compose: `docker-compose --version`

- Nếu chưa có docker-compose thì chạy thêm lệnh: `sudo apt install docker-compose`

- Bật service docker trên WSL: `sudo service docker start`

- Kiểm tra service đã bật bằng  `sudo service --status-all`. Nếu thấy trước docker là dấu [+] tức là đang hoạt động

### Chú ý

- Nếu bật service docker mà lỗi (hoặc bật lên OK nhưng lại tắt ngay lập tức) thì kiếm tra log tại vị trí `/var/log/docker.log`

- Có thể dùng lệnh `cat /var/log/docker.log` để in ra màn hình terminal luôn

- Xem dòng cuối cùng có lỗi liên quan đến `iptables` thì chạy lệnh sau trong terminal ubuntu:
`sudo update-alternatives --config iptables`

- Xem tùy chọn nào là `iptables-legacy` thì chọn, nhập số ở cột **Selection** tương ứng với **Path** muốn chọn, rồi **Enter**

- Tắt và bật lại terminal


<br>
<br>

## 4. Cài đặt Make

* Chạy lệnh sau trên WSL để cài đặt Make: `sudo apt install -y make`

<br>
<br>

## 5. Cài đặt Windows Terminal

- Mở Microsoft Store, tìm `Windows Terminal` và cài đặt

<br>
<br>

## 6. Cài đặt Extension trên VSCode

- Mở một file bất kỳ bằng VSCode, vào mục `Extension` (phím tắt `Ctrl + Shift + X`).

- Nhập `ms-vscode-remote.remote-wsl` vào thanh tìm kiếm và cài đặt. Khi cài đặt xong thì tắt VSCode

- Mở terminal, mở một tab mới sử dụng Ubuntu. 

- Tạo thư mục project `mkdir project`

- Mở thư mục project bằng VSCode `code project`

- Vào mục `Extension` (phím tắt `Ctrl + Shift + X`). Khi đó sẽ có `LOCAL - INSTALLED` và `WSL: UBUNTU - INSTALLED`

    + Bắt buộc: Nhập `ms-azuretools.vscode-docker` và chọn install để cài đặt Docker Extension

    + Không bắt buộc: Trên thanh `WSL: UBUNTU - INSTALLED` sẽ có biểu tượng download hình đám mây, click vào đó và chọn những extension đã cài ở LOCAL để cài lên trên WSL

- Mở một dự án trên WSL bằng VSCode bằng cách `cd` vào thư mục và nhập `code .` hoặc thay dấu chấm bằng đường dẫn đến dự án (VD: `code /project/library/docker`). Khi đó Docker extension sẽ tự tìm các container trên wsl và có thể thao tác với docker qua extension này

<br>
<br>

# Một số lệnh Docker

### Show

- `docker ps` Show các container đang chạy (trạng thái up)

- `docker ps -a` Show tất cả các container (cả up và stop)

- `docker images` Show tất cả các image đã pull về máy

- `docker volume ls` Show các volume

### Run

- `docker-compose up -d` Chạy các container của một project

- `docker-compose down` Dừng và xóa các container của một project

- `docker-compose stop` Dừng các container của một project

- `docker-compose restart` Chạy lại các container của một project

- `docker run -d --name my_container -p 8080:80 my_image`

### Stop container

- `docker stop <container_id>` Dừng một container theo id

- `docker stop $(docker ps -q)` Dừng tất cả các container đang bật

### Remove

- `docker rm -vf $(docker ps -aq)` Xóa tất cả các container

- `docker rmi -f $(docker images -aq)` Xóa tất cả các images

- `docker volume prune -a -f` Xóa các volume

- `docker compose exec names_dockerps php artisan config:cache` Cache config php dự án
