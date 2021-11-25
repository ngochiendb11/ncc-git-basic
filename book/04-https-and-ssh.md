# 1. HTTPS và SSH là gì?

HTTPS và SSH đều là những giao thức để truyền dữ liệu từ client đến server giống như HTTP, FTP, sFTP, FTPs, vv.

![Https-ssh](../assets/04-https-and-ssh.png)

# HTTPS

Đây là giao thức bảo mật hơn của HTTP, dữ liệu được truyền đi đều được mã hóa. HTTPS sử dụng cổng 443 đều tạo kết nối. Phương thức xác thực là sử dụng cặp public/private key. Đây là phương thức được sử dụng phổ biến.

# SSH

Nó cũng là 1 giao thức an toàn, dữ liệu đều được mã hóa. SSH sử dụng cổng 22 để tạo kết nối và xác thực. Việc xác thực các thiết bị từ xa sử dụng mã khóa công khai (public-key cryptography). Phương thức xác thực là cặp public/private key hoặc userid/password.

## Cơ chế làm việc của SSH

Bạn sẽ có 2 key: public key và private key. Bạn sẽ gửi public key của mình cho git server của bạn (gitlab hay github chẳng hạn).

Xong ssh-agent sẽ làm tất cả những việc còn lại cho bạn. Mỗi lần bạn push, ssh-agent sẽ tự gửi kèm các thông tin chứng thực đi, github sẽ nhận diện ra bạn, và bạn không cần phải nhập mật khẩu nữa.

- ## Sinh SSH Key

  # Bước 1: Kiểm tra xem máy bạn có ssh key nào chưa

  Mở cửa sổ dòng lệnh (terminal) và chạy lệnh:

**$ ls -al ~/.ssh**

Bash
Lệnh trên sẽ kiểm tra trong thư mục .ssh (nằm ở thư mục gốc của user bạn đang đăng nhập vào máy, Vd trên Linux: /root/.ssh) có ssh key nào chưa, mặc định, các ssh key thường sẽ có dạng:

<!--
% id_rsa
% id_rsa.pub
% id_dsa.pub
% id_ecdsa.pub
% id_ed25519.pub -->

public key sẽ có đuôi .pub (id_rsa.pub), private key thì không có đuôi (id_rsa) Nếu có một cặp ssh key nào trong thư mục này (giả sử là id_rsa và id_rsa.pub), bạn có thể bỏ qua Bước 2 và chuyển thẳng sang Bước 3.

##

# Bước 2: Sinh một SSH key mới

Chạy lệnh sau trên terminal:

**ssh-keygen -t rsa -b 4096 -C "email_cua_ban@example.com"**

Để ngắn gọn hơn bạn có thể sử dụng lệnh này:

**ssh-keygen -t rsa**
Bash
Để tránh phiền phức sau này, mình khuyên bạn nên để các cài đặt ở mặc định, như lần này, ssh-agent hỏi bạn muốn lưu key của mình ở đâu thì bạn cứ thế mà Enter thôi:

Enter file in which to save the key (/root/.ssh/id_rsa): [Press enter]
Bash
Nếu bạn muốn tạo một tên ssh-key khác thì hãy nhập đường dẫn cần lưu vào đây (Vd: /root/.ssh/id_rsa)

Tiếp đến thì nhập mật khẩu cho key của bạn:

**Enter passphrase (empty for no passphrase): [Type a passphrase]**

# Bước 3: Thêm key của bạn vào ssh-agent

ssh-agent là trình quản lý ssh key của bạn, công việc của nó thì nãy mình có nói qua ở trên rồi đó.

Đảm bảo rằng ssh-agent đã được kích hoạt bằng lệnh:

**eval "$(ssh-agent -s)"**

Add ssh key của bạn vào ssh-agent:

**ssh-add ~/.ssh/id_rsa**

# Bước 4: Thêm ssh public key vào tài khoản trên server của bạn (github, gitlab…)

Copy ssh key vào clipboard:

**pbcopy < ~/.ssh/id_rsa.pub**
