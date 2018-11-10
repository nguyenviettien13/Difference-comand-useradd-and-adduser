# Difference-comand-useradd-and-adduser
 =====
  **_Khái quát về tài khoản trong linux và sự khác nhau giữa 2 cách tạo tài khoản 'useradd' và 'adduser'_**
 Mục lục
 =====
## 1. Khái niệm
Linux là một nền tảng sử dụng đa người dùng nên trong Linux có thể tạo nhiều người sử dụng. Mỗi ngưởi sử dụng được đặc chưng bởi một tài khoản đăng nhập hệ thống (account) và một password.

Có 3 loại tài khoản:

- Siêu tài khoản: root. được gọi là siêu tài khoản vì nó có quyển lực  cao nhất, nó có thể can thiệt vào mọi việc trong hệ thống
- Ngưởi sử dụng bình thường: được cấp một tài khoản và password để có thể thực hiện quyền sử dụng trên các hệ thống và bị hạn chế về quyền lực
- Tài khoản nobody: tài khoản này để chạy các chương trình dịch vụ trên hệ thống, tài khoản này không có thư mục home và môi trường shell để làm việc Chỉ có tài khoản root mới có thể tạo ra người sử dụng

