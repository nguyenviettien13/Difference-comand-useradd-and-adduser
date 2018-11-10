# Difference-comand-useradd-and-adduser
## Khái quát về tài khoản trong linux và sự khác nhau giữa 2 cách tạo tài khoản 'useradd' và 'adduser'
## Mục lục
## 1. Khái niệm
Linux là một nền tảng sử dụng đa người dùng nên trong Linux có thể tạo nhiều người sử dụng. Mỗi ngưởi sử dụng được đặc chưng bởi một tài khoản đăng nhập hệ thống (account) và một password.

Có 3 loại tài khoản:

- Siêu tài khoản: root. được gọi là siêu tài khoản vì nó có quyển lực  cao nhất, nó có thể can thiệt vào mọi việc trong hệ thống
- Ngưởi sử dụng bình thường: được cấp một tài khoản và password để có thể thực hiện quyền sử dụng trên các hệ thống và bị hạn chế về quyền lực
- Tài khoản nobody: tài khoản này để chạy các chương trình dịch vụ trên hệ thống, tài khoản này không có thư mục home và môi trường shell để làm việc Chỉ có tài khoản root mới có thể tạo ra người sử dụng
 ```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false
systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false
systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false
systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false
syslog:x:104:108::/home/syslog:/bin/false
_apt:x:105:65534::/nonexistent:/bin/false
messagebus:x:106:110::/var/run/dbus:/bin/false
uuidd:x:107:111::/run/uuidd:/bin/false
lightdm:x:108:114:Light Display Manager:/var/lib/lightdm:/bin/false
whoopsie:x:109:116::/nonexistent:/bin/false
avahi-autoipd:x:110:119:Avahi autoip daemon,,,:/var/lib/avahi-autoipd:/bin/false
avahi:x:111:120:Avahi mDNS daemon,,,:/var/run/avahi-daemon:/bin/false
dnsmasq:x:112:65534:dnsmasq,,,:/var/lib/misc:/bin/false
colord:x:113:123:colord colour management daemon,,,:/var/lib/colord:/bin/false
speech-dispatcher:x:114:29:Speech Dispatcher,,,:/var/run/speech-dispatcher:/bin/false
hplip:x:115:7:HPLIP system user,,,:/var/run/hplip:/bin/false
kernoops:x:116:65534:Kernel Oops Tracking Daemon,,,:/:/bin/false
pulse:x:117:124:PulseAudio daemon,,,:/var/run/pulse:/bin/false
rtkit:x:118:126:RealtimeKit,,,:/proc:/bin/false
saned:x:119:127::/var/lib/saned:/bin/false
usbmux:x:120:46:usbmux daemon,,,:/var/lib/usbmux:/bin/false
tiennv000:x:1000:1000:tiennv000,,,:/home/tiennv000:/bin/bash
mysql:x:121:129:MySQL Server,,,:/var/lib/mysql:/bin/false
 ```
##### a. Chỉ số UID
UID (User ID) là một số nguyên dương đại diện cho từng người sử dụng. Để xem UID của người sử dụng ta dùng câu lệnh sau
````
	# vi /etc/passwd
````
<img src="http://i.imgur.com/VLJljRL.png">
##### b. Chỉ số GID
GID (Group ID): Group là một nhóm gồm nhiều tài khoản. Trong Linux có thể tạo ra nhiều group và trong mỗi group chứa một số lượng tài khoản người dùng: VD: group "congnhan" chứa người dùng là công nhân group "vanphong" chứa người dùng làm văn phòng
<img src="http://i.imgur.com/VLJljRL.png">
##### 2. Cách tạo người sử dụng
Để có thể tạo được tài khoản trong Linux nhất thiết bạn phải đăng nhập bằng tài khoản root. Xét riêng trường hợp tạo tài khoản trong Linux bằng câu lệnh có 2 cách được sử dụng: useradd và adduser. Tôi sẽ sử dụng cả 2 câu lệnh này để tạo tài khoản và chỉ ra sự khác nhau giữa 2 câu lệnh này.
 ***_Lưu ý: để có thể thấy rõ sự khác nhau giữa hai câu lệnh bạn nên sử dụng Linux có phiên bản là Ubuntu
###### a. Sử dụng lệnh useradd
Tạo tài khoản:
 ```
	#useradd [option] <Tên tài khoản>
 ```
*Trong đó:*Trường option bao gồm các tùy chọn
|Tùy chọn | Ý nghĩa |
|---------|---------|
|-p | nhập password cho tài khoản |
|-c | thêm thông tin cho tài khoản |
|-d | chỉ đường dẫn chưa thư mục home của tài khoản, nếu không chỉ định thì mặc định nó sẽ tạo thư mục tại /home |
|-g | chỉ ra nhóm tài khoản muốn thuộc, nếu không chỉ mặc định nó sẽ tạo ra một group để cho tài khoản đó vào |
|-s | xác định shell cho hệ thống, mặc định là /bin/bash |
|-u | xác định chỉ số UID của người dùng |
|-e | có định dạng là yyyy-mm-dd xác định thời gian hệ hạn của tài khoản |
|-f | yyyy-mm-dd xác định số ngày password sẽ vô hiệu hóa khi tài khoản hết hạn |

Đây là một số tùy chọn thường được sử dụng. Ngoài ra nó còn một số các tùy chọn khác nữa, bạn có thể dùng command để biết thêm các tùy chọn khác ` man useradd `.

VD: #useradd -c 'Nguyen Hoai Nam' -d /home/hoainam -e 2014-12-11 -p admin1234 hoainam

###### b. Sử dụng lệnh adduser







