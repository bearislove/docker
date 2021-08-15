
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

docker images
sudo docker run -d --name myweb ubuntu:latest
docker exec -it myweb bash
Trườg hợp tạo container mà quên không cho tham số -d thì start bằng lệnh.
docker start myweb
docker exec -it myweb bash
-------------------
apt install  curl

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


