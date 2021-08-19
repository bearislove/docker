
## Giới thiệu

Docker là nền tảng giúp chạy phần mềm trong container, là một nền tảng mã nguồn mở cho việc phát triển, vận chuyển và chạy các ứng dụng phân tán. Docker Container chứa tất cả các thành phần của phần mềm để chạy một ứng dụng. Khi sử dụng docker, bạn có thể tạo ra được một môi trường tách biệt cho mỗi ứng dụng riêng.

## Lợi ích chính của Docker 

Là cho phép người dùng đóng gói một ứng dụng với tất cả các phụ thuộc của nó vào một đơn vị được tiêu chuẩn hóa để phát triển phần mềm.
Không giống như các máy ảo, các container sử dụng ít tài nguyên hơn và do đó cho phép sử dụng hiệu quả hơn các tài nguyên hệ thống.
 
## Docker image
 
**Images**: hiểu nôm na là một khuôn mẫu để tạo một container. 
Thường thì image sẽ base trên 1 image khác với những tùy chỉnh thêm. 
ví dụ bạn build 1 image dựa trên image ubuntu để chạy Apache web service và ứng dụng của bạn và những tùy chỉnh, cấu hình để ứng dụng của bạn có thể chạy được. Bạn có thể tự build một image riêng cho mình hoặc sử dụng những image được publish từ cộng đồng Docker Hub. Một image sẽ được build dựa trên những chỉ dẫn của Dockerfile.
 
**Liệt kê danh sách các images**

Dùng lệnh **docker images** để liệt kê tất cả images có sẵn trên máy tính chạy docker của bạn.

`docker images`

**Tìm kiếm **docker images****

Dùng lệnh docker search để tìm kiếm các images trên docker hub. Ví dụ, dùng lệnh sau để tìm docker images centOS.

``docker search centos``

**Download **docker imag**e**

Bạn dùng lệnh **docker pull** để download bất kỳ image từ docker hub. Ví dụ để download image centOS phiên bản mới nhất từ docker hub về máy local và tạo container.

``docker pull centos``

**Xóa docker image**

Ta dùng lệnh docker rmi để xóa bất kỳ docker image từ hệ thống local. Ví dụ, để xóa image tên centos dùng lệnh sau:

``docker rmi centos``
 
 
## Docker Container

**Docker container** là một **instance** của **image**. Một container chỉ cần kết hợp với các thư viện và thiết lập cần thiết để làm cho ứng dụng hoạt động. Nó là một môi trường đóng gói gọn nhẹ và di động cho một ứng dụng.

Sự khác biệt giữa **Docker Images** và **Docker Containers**
 
Docker Images: Là một template **chỉ cho phép đọc**. 
   1. Ví dụ một image có thể chứa hệ điều hành Ubuntu và web app. 
   2. Images được dùng để tạo Docker container. 
   3. Docker cho phép chúng ta build và cập nhật các image có sẵn một cách cơ bản nhất, hoặc bạn có thể download Docker images của người khác.

Docker Containers: Docker container có nét giống với các directory. 
   1. Một Docker container giữ mọi thứ chúng ta cần để chạy một app. 
   2. Mỗi container được tạo từ Docker image.
   3. Docker container có thể có các trạng thái run, started, stopped, moved và deleted.

**Cách chạy một docker container**

Sử dụng lệnh docker để khởi chạy docker container trên hệ thống của bạn. Ví dụ lệnh bên dưới sẽ tạo một Docker Container từ image có tên “hello-world”.

``docker run hello-world``

Bây giờ tạo một instance docker chạy hệ điều hành CentOS. Tùy chọn -it sẽ cung cấp một phiên tương tác với pseudo-TTY. Nó cung cấp cho bạn shell của container ngay lập tức.
``
docker run -it centos
``
**Liệt kê danh sách docker container**

Dùng lệnh **docker ps** để liệt kê các container đang chạy trên hệ thống hiện tại. Nó sẽ không liệt kê các container bị dừng. Nó sẽ hiển thị Container ID, name và các thông tin hữu ích khác về container.

``docker ps ``

Dùng tùy chọn -a với lệnh ở trên để liệt kê tất cả các container bao gồm cả container bị dừng.

``docker ps -a``

**Tìm kiếm tất cả thông tin chi tiết về container**

``docker inspect cc5d74cf8250``

Trong đó: **cc5d74cf8250** là **id container**
**Xóa Docker container**

Dùng lệnh **docker rm để xóa docker container** đang tồn tại. Bạn cần cung cấp **docker container id** hoặc **container name** để xóa một container cụ thể.

``docker stop cc5d74cf8250``
``docker rm cc5d74cf8250``

## Thực hành tạo một container

- Cài thêm một package curl.
- start, stop, exec.

```
docker images
sudo docker run -d --name myweb ubuntu:latest
docker exec -it myweb bash
Trườg hợp tạo container mà quên không cho tham số -d thì start bằng lệnh.
docker start myweb
docker exec -it myweb bash
-------------------
apt install  curl
```

Bài 2 Tạo container từ image của nginx
https://hub.docker.com/_/nginx
https://linuxways.net/ubuntu/how-to-install-docker-in-ubuntu-20-04-and-run-nginx-container/

## Dockerfile
Dockerfile là một file được dùng để build một image bằng cách đọc các chỉ dẫn từ file đó. Tên file mặc định được dùng là Dockerfile. Bạn có thể tạo dockerfile trong thư mục hiện tại với các chỉ dẫn cụ thể và build một image tùy chỉnh theo yêu cầu của bạn.

**Cách build image với Dockerfile**

Dockerfile là một file được đặt ở vị trí gốc trong container khi build xong. Bạn có thể dùng lệnh sau đây để build docker image. Trong câu lệnh bên dưới, docker sẽ đọc Dockerfile tại vị trí thư mục hiện tại.

**docker build -t image_name .**

Bạn cũng có thể dùng cờ **-f** với lệnh docker build để trỏ đến Dockerfile tại bất kỳ nơi nào trong hệ thống file của bạn.

**docker build  -t image_name -f /path/to/Dockerfile .**


## Có gì bên trong Dockerfile

Trong Dockerfile, có một số điểm mà các bạn cần phải biết với những chỉ thị như sau

**FROM**

**FROM** được dùng để thiết lập image cơ sở cho chỉ dẫn tiếp theo. Dockerfile phải có chỉ thị FROM với tên image hợp lệ là chỉ thị đầu tiên.

``FROM ubuntu``
``FROM php:7.4-fpm``

**LABEL**
Sử dụng label, bạn có thể tổ chức các image đúng cách. Nó cực kỳ hữu ích để thiết lập địa chỉ nhà phát triển, tên nhà cung cấp, phiên bản image, ngày phát hành,…

```
LABEL maintainer="anhtt1@kaopiz.com"
LABEL vendor="anhtt"
LABEL com.example.version="1.1.1"
```
**RUN**

Dùng chỉ thị RUN, bạn có thể chạy bất kỳ lệnh nào tới image trong thời gian build. Ví dụ, bạn có thể cài đặt các package bắt buộc trong thời gian build.

```
RUN apt-get update 
RUN apt-get install -y apache2 automake build-essential curl
```
Hoặc sử dụng chạy một chỉ thị RUN như sau:

```
RUN apt-get update && apt-get install -y \
    automake \
    build-essential \
    curl \
```

**COPY**

Chỉ thị COPY được dùng để copy file và thư mục từ hệ thống host tới image trong khi build. Ví dụ, lệnh đầu tiên sẽ copy tất cả file từ thư mục host html/ tới thư mục /var/www/html trên image. Lệnh thứ hai sẽ copy tất cả file với phần mở rộng .conf tới địa chỉ thư mục 
**/etc/apache2/sites-available/** .


```
COPY html/* /var/www/html/
COPY *.conf /etc/apache2/sites-available/
```

**WORKDIR**

Chỉ thị WORKDIR được dùng để thiết lập thư mục làm việc hiện tại cho bất kỳ chỉ thị RUN, CMD, ENTRYPOINT, COPY… trong quá trình build.

```
WORKDIR /opt
```


**CMD**

Chỉ thị CMD được dùng để chạy các dịch vụ hoặc phần mềm có chứa bên trong image, cùng với bất kỳ tham số khác trong khi khởi chạy container. CMD dùng cú pháp đơn giản sau đây:

```
CMD ["executable","param1","param2"]
CMD ["executable","param1","param2"]
```
Ví dụ, để khởi động dịch vụ Apache khi khởi chạy container, dùng lệnh sau đây:

```
CMD ["apachectl", "-D", "FOREGROUND"]
```

**EXPOSE**

Chỉ thị EXPOSE chỉ ra các port mà container sẽ lắng nghe cho các kết nối. Sau đó bạn có thể liên kết các port hệ thống với container và dùng chúng.

```
EXPOSE 80
EXPOSE 443
```
**ENV**
Chỉ thị ENV được dùng để thiết lập biến môi trường cho các dịch vụ cụ thể của container.

```
ENV PATH=$PATH:/usr/local/pgsql/bin/ \
    PG_MAJOR=9.6.0
```
**VOLUME**

Chỉ thị VOLUME tạo một mount point với tên được chỉ định và đánh dấu nó là nơi giữ mount volume từ host bên ngoài hoặc container khác.
```
VOLUME ["/data"]
```
## Docker – quản lý ports

Docker containers chạy các dịch vụ bên trong nó trên các port được chỉ định cụ thể. Để truy cập dịch vụ của một container đang chạy trên một port, bạn cần liên kết container port với port trên Docker host (máy thật).

Ví dụ 1:

Nhìn vào hình bên dưới, bạn sẽ thấy docker host đang chạy hai containers, một cái chạy Apache và cái còn lại chạy MySQL.

![image](https://user-images.githubusercontent.com/31482352/130097684-b563e2ce-7901-42a5-a4b1-a66d248193a8.png)

Bây giờ, bạn cần truy cập vào website đang chạy Apache container trên port 80. Chúng ta sẽ liên kết docker port 8080 tới container port 80. Bạn cũng có thể dùng port 80 trên docker port.

Container thứ hai chạy MySQL trên port 3306. Có nhiều cách khác để truy cập MySQL từ docker host. Nhưng trong bài viết này, mình sẽ liên kết docker port 6603 tới container port 3306. Bây giờ, mình sẽ truy cập trực tiếp MySQL từ Docker container bằng cách kết nối docker host trên port 6603.

Câu lệnh bên dưới sẽ liên kết host docker port với container port.
```
$ docker run -it -p 8080:80 apache_image
$ docker run -it -p 6603:3066 mysql_image
```
Ví dụ 2:

Trong ví dụ thứ hai dùng project có sẵn của mình trên github. Nó sẽ show cho bạn ví dụ đang chạy trên port 8080 trên docker host. Đơn giản bạn chỉ cần clone repository bằng cách chạy câu lệnh sau:

```
$ git clone https://github.com/tecrahul/dockerfile
$ cd dockerfile
```
Bây giờ, build docker image với tên apacheimage

```docker build -t apacheimage .```

Chạy container bằng cách sử dụng lệnh docker run. Dịch vụ apache sẽ khởi động trên container port 80. Bạn cần chỉ ra port cụ thể bằng cách dùng option -p 8080:80 để liên kết host system port 8080 với container port 80.

**docker run -it -p 8080:80 apacheimage**

Bây giờ truy cập địa chỉ IP docker host với port 8080 trên trình duyệt web. Bạn sẽ xem được trang web đang chạy trên Apache của container

**Thêm một ví dụ nữa:**

Bạn có thể liên kết nhiều ports với một container, nhưng cần đảm bảo bạn đã sử dụng chỉ dẫn EXPOSE tất cả các ports trong Dockerfile trước khi build image.

```
docker run -it -p 8080:80,8081:443 image_name
```

Nếu bạn cần liên kết port với interface của docker host cụ thể, khai báo địa chỉ IP như bên dưới. Trong ví dụ bên dưới, port 8080, 8081 sẽ có thể truy cập với địa chỉ 127.0.0.1

```
$ docker run -it -p 127.0.0.1:8080:80,127.0.0.1:8081:443 image_name
$ docker run -it -p 192.168.1.111:8080:80,92.168.1.111:8081:443 image_name
```

## Networking
Docker cung cấp một tùy chọn để tạo và quản lý network riêng giữa các container. Dùng lệnh docker network để quản lý Docker networking.

**Cú pháp**
```
docker network [options]
```
Dùng cách lệnh theo hướng dẫn bên dưới để tạo, liệt kê và quản lý Docker networking.

**Liệt kê Docker networks**

Dùng tùy chọn ls với lệnh docker network để liệt kê các network khả dụng trên system host.

```
docker network ls
```

**Tạo docker network**

Docker cung cấp nhiều loại network. Lệnh bên dưới sẽ tạo bridge network trên hệ thống của bạn.

Cú pháp

```
docker network create -d [network_type] [network_name]
```
Ví dụ

docker network create -d bridge my-bridge-network
Kết nối container với network

Bạn có thể kết nối bất kỳ container nào tới một docker network đang tồn tại bằng cách sử dụng tên container hoặc ID. Một khi container được kết nối tới network, nó có thể giao tiếp với các container khác trong cùng mạng.

Cú pháp

docker network connect [network_name] [container_name]
Ví dụ

docker network connect my-bridge-network centos
Ngắt kết nối docker khỏi network

Bạn có thể ngắt kết nối một container khỏi một network cụ thể bất cứ khi nào bằng cách dùng lệnh dưới đây

Cú pháp

docker network disconnect [network_name] [container_name]
Ví dụ

docker network disconnect my-bridge-network centos
Kiểm tra Docker network

Dùng tùy chọn inspect để kiểm tra với lệnh docker network để xem chi tiết docker network

docker network inspect my-bridge-network
Bạn sẽ nhận được kết quả như sau

Xóa Docker network

Dùng tùy chọn rm để xóa bất kỳ Docker network nào đang không sử dụng. Bạn có thể chỉ định một hoặc nhiều network hơn bằng cách sử dụng dấu cách (space) để xóa.

Ví dụ

docker network rm my-bridge-network network2 network3
Bạn cũng có thể xóa tất cả network không sử dụng khỏi system host bằng cách sử dụng tùy chọn prune.

docker network prune


