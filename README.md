![what-is-nginx](https://user-images.githubusercontent.com/54676091/91526395-b5bbb800-e92d-11ea-9b8b-2a2f0b6c4357.png)


Khái niệm, ưu điểm, nhược điểm, hoạt động thế nào, cài đặt ra sao, dùng thế nào
Nginx là một phần mềm web server mã nguồn mở nổi tiếng


-Ban đầu thì nó dùng để phuc vụ http tuy nhiên hiện nay nó còn có thể được dùng để làm reverse proxy HTTP load balancer và emial proxy như IMAP, POP3 và SMtp

-Vì khả năng mạnh mẽ, và để có thể xử lý hàng ngàn kết nối cùng lúc, nhiều website có traffic lớn đã sử dụng dịch vụ NGINX

-web server hoạt động thế nào?  khi gửi một yêu cầu để mở một trang web. Trình duyệt sẽ liên lạc với server chứa website đó. Sau đó, server sẽ tìm kiếm đúng file yêu cầu của trang đó và gửi ngược về cho server.

-(Đây là một loại truy vấn đơn giản nhất.)*single thread – một bộ các bước xử lý dữ liệu được thực thi theo 1 trình tự duy nhất.

-Về cơ bản, NGINX cũng hoạt động tương tự như các web server khác. Khi bạn mở một trang web, trình duyệt của bạn sẽ liên hệ với server chứa website đó. Server sẽ tìm kiếm đúng file yêu cầu của website và gửi về cho bạn. Đây là một trình tự xử lý dữ liệu single – thread, 
Nghĩa là các bước được thực hiện theo một trình tự duy nhất. Mỗi yêu cầu sẽ được tạo một thread riêng.
Tuy nhiên, NGINX hoạt động theo kiến trúc bất đồng bộ (asynchronous) hướng sự kiện (event driven). Nó cho phép các threads tương đồng được quản lý trong một tiến process. Mỗi process hoạt động sẽ bao gồm các thực thể nhỏ hơn, gọi là worker connections dùng để xử lý tất cả threads.

-Worker connections sẽ gửi các yêu cầu cho worker process, worker process sẽ gửi nó tới master process, và master process sẽ trả lời các yêu cầu đó. Đó là lý do vì sao một worker connection có thể xử lý đến 1024 yêu cầu tương tự nhau. 

-Nhờ vậy, NGINX có thể xử lý hàng ngàn yêu cầu khác nhau cùng một lúc.

![0_r2AvgpaSlbQtddsW](https://user-images.githubusercontent.com/54676091/91526592-34185a00-e92e-11ea-8970-3d41fd623d76.png)

Điều này có vẻ đơn giản, một worker connection có thể xử lý đến 1024 yêu cầu tương tự nhau. Vì vậy, NGINX có thể xử lý hàng ngàn yêu cầu mà không gặp rắc rối gì.

Ưu điểm: 

-Có thể xử lý hơn 10.000 kết nối cùng lúc với bộ nhớ thấp;

-Phục vụ tập tin tĩnh (static files) và lập chỉ mục tập tin;

-Tăng tốc proxy ngược bằng bộ nhớ đệm (cache); cân bằng tải đơn giản và khả năng chịu lỗi;

-Hỗ trợ tăng tốc với bộ nhớ đệm của FastCGI, uWSGI, SCGI, và các máy chủ memcached;

-Kiến trúc modular; tăng tốc độ nạp trang bằng nén gzip tự động;

-Hỗ trợ mã hoá SSL và TLS;

-Cấu hình linh hoạt; lưu lại nhật ký truy vấn;

-Chuyển hướng lỗi 3XX-5XX;

-Rewrite URL (URL rewriting) dùng regular expressions;

-Hạn chế tỷ lệ đáp ứng truy vấn;

-Giới hạn số kết nối đồng thời hoặc truy vấn từ 1 địa chỉ;

-Khả năng nhúng mã PERL;

-Hỗ trợ và tương thích với IPv6

-Hỗ trợ WebSockets;

-Hỗ trợ truyền tải file FLV và MP4.

-Xử lý nhiều truy vấn cùng lúc

-Dễ dàng để mở rộng cho website hơn cũng như traffic web

- Sử dụng như một HTTP proxy hay load balancer cho các web server khác. 

-Hiểu được NGINX là gì và cách NGINX làm việc và xử lý các request sẽ cung cấp nhiều sức mạnh để mở rộng (scaling) và cân bằng tải (balancing the load) cho ứng dụng của bạn.
Khuyết điểm:

-Có thể chạy trên nhiều hệ điều hành khác nhau của hệ thống Unix. Nhưng không may là, hiệu năng của NGINX trên Windows lại tỏ ra kém hiệu quả hơn khi hoạt động trên các platform khác.
Cài đặt ra sao, dùng thế nào

-sử dụng gói (package) dựng sẵn hoặc cài đặt từ source.

-Để cài đặt một gói Debian dựng sẵn, thứ duy nhất cần làm là:

sudo apt-get update
sudo apt-get install nginx

-Sau khi quá trình cài đặt kết thúc, bạn có thể kiểm tra mọi thứ là ỔN bằng cách chạy lệnh dưới đây, nó sẽ hiển thị phiên bản NGINX được cài đặt:
sudo nginx -v

nginx version: nginx/1.6.2


-Webserver mới sẽ được cài đặt tại /etc/nginx/. Nếu bạn vào trong thư mục này, bạn sẽ thấy nhiều tệp tin và thư mục. Nhưng thứ quan trọng nhất cần chú ý là tệp tin nginx.conf và thư mục sites-available.
Chi tiết
https://topdev.vn/blog/nginx-la-gi/ https://medium.com/@dongnguyenltqb/nginx-l%C3%A0-g%C3%AC-setup-m%E1%BB%99t-server-serve-static-file-v%E1%BB%9Bi-nginx-12e439e2109e
https://wiki.matbao.net/nginx-la-gi-huong-dan-kiem-tra-va-cai-dat-nginx-server/


Khởi động NGINX


-Sau khi chúng ta hoàn tất cấu hình và di chuyển ứng dụng web tới thư mục phù hợp, chúng ta có thể khởi động NGINX sử dụng lệnh dưới đây: sudo service nginx start

-Sau đó, bất cứ khi nào chúng ta thay đổi cấu hình, chúng ta chỉ cần tải lại (không có thời gian downtime) sử dụng lệnh dưới đây: service nginx reload Cuối cùng, chúng ta có thể kiểm tra trạng thái của NGINX sử dụng lệnh dưới đây: service nginx status


- So sánh nginx với các `web server` khác

![so-sanh-nginx-va-apache](https://user-images.githubusercontent.com/54676091/91528851-717ee680-e932-11ea-8cfa-c509eec95a2a.jpg)


Apache server 

-Apache thiếu hỗ trợ từ chính công ty của nó, Apache Foundation

-Hiệu năng của NGINX trên Windows lại tỏ ra kém hiệu quả hơn Apache

-NGINX xử lý cùng lúc 1000 kết nối tới nội dung tĩnh nhanh hơn 2 lần so với Apache và dùng ít bộ nhớ hơn .NGINX là lựa chọn tốt hơn cho những ai có website tĩnh

-NGINX là web server có thể hoạt động như là email proxy, reverse proxy và load balancer. Cấu trúc của phần mềm này là bất đồng bộ và hướng sự kiện; vì vậy cho phép phần mềm xử 
lý nhiều truy vấn cùng lúc. NGINX dễ dàng để mở rộng cho website hơn, đồng nghĩa với việc dịch vụ này có thể đi theo suốt qua trình phát triển của website, cũng như traffic web

