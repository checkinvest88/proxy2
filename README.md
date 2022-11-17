# proxy2
Admin
bash <(curl -s "https://raw.githubusercontent.com/checkinvest88/proxy2/main/createproxy.sh")
Cách tạo proxy từ server Centos.

I. Cài đặt Squid

Update :

Yum –y update

Cài Squid :

yum -y install squid

Tạo file backup :

cp /etc/squid/squid.conf /etc/squid/squid.conf.default

Sửa file :

Vi /etc/squid/squid.conf

Tìm dòng

# and finally deny all other access to this proxy

http_access deny all

Sửa thành

http_access allow all

Thay thế port mà bạn muốn sử dụng :

# Squid normally listens to port 3128

http_port 16861

Nếu muốn chặn chỉ mở port cho 1 IP thì thêm dòng sau :

#Your Personal IP to allow without authentication (Remove this line and one below to disable this)

acl myclients src ###.##.##.###

#Allow this IP without authentication

http_access allow myclients

Sửa ###.###.###.### thành IP cần mở port

Thêm đoạn mã sau để các hệ thống không nhận ra là bạn đang sử dụng máy chủ proxy :

forwarded_for off

request_header_access Allow allow all

request_header_access Authorization allow all

request_header_access WWW-Authenticate allow all

request_header_access Proxy-Authorization allow all

request_header_access Proxy-Authenticate allow all

request_header_access Cache-Control allow all

request_header_access Content-Encoding allow all

request_header_access Content-Length allow all

request_header_access Content-Type allow all

request_header_access Date allow all

request_header_access Expires allow all

request_header_access Host allow all

request_header_access If-Modified-Since allow all

request_header_access Last-Modified allow all

request_header_access Location allow all

request_header_access Pragma allow all

request_header_access Accept allow all

request_header_access Accept-Charset allow all

request_header_access Accept-Encoding allow all

request_header_access Accept-Language allow all

request_header_access Content-Language allow all

request_header_access Mime-Version allow all

request_header_access Retry-After allow all

request_header_access Title allow all

request_header_access Connection allow all

request_header_access Proxy-Connection allow all

request_header_access User-Agent allow all

request_header_access Cookie allow all

request_header_access All deny all

Xong lưu lại file và chạy lệnh /etc/squid/squid.conf

service squid restart

Thấy 2 dòng OK là xong.

II. Mở port .

Chạy trên console :



cp /etc/sysconfig/iptables /etc/sysconfig/iptables.backup

vi /etc/sysconfig/iptables

Thêm dòng sau vào file /etc/sysconfig/iptables (Trong hướng dẫn này tôi sử dụng Port : 16861)

-A INPUT -m state --state NEW -m tcp --dport 16861 -j ACCEPT

Lưu lại và chạy lệnh :

/etc/init.d/iptebles restart

Xuất hiện 2 dòng OK là xong.


Centos thì làm thế này là xong nhé.

Free luôn
