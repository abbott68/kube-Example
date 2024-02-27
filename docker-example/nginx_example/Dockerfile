FROM  centos:centos7.9.2009

ENV index=/usr/share/nginx/html
RUN yum -y install vim  net-tools  wget \
    && wget -O /etc/yum.repos.d/epel.repo https://mirrors.aliyun.com/repo/epel-7.repo  \
    && yum -y install nginx
#拷贝index页面文件

COPY index.html ${index}  
# 释放容器的端口号
EXPOSE  80/tcp

CMD [ "nginx", "-g", "daemon off;" ]