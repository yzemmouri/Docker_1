FROM ubuntu:20.04
RUN apt-get update  && apt-get upgrade -y &&\
    DEBIAN_FRONTEND=noninteractive apt-get install apt-utils apt-transport-https curl openssh-server ca-certificates postfix -y && \
    DEBIAN_FRONTEND=noninteractive curl https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.deb.sh | bash && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y gitlab-ce && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y tzdata

WORKDIR /etc/gitlab

ARG MY_HOST
RUN    mkdir -p ssl && chmod 755 ssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout ssl/$MY_HOST.key -out ssl/$MY_HOST.crt -subj "/C=MA/ST=KH/L=KH/O=1337/OU=1337/CN=[$MY_HOST]/emailAddress=[email]"

RUN sed -i "s/http:\/\/gitlab.example.com/https:\/\/$MY_HOST/" gitlab.rb && \
    echo "nginx['enable'] = true" >> gitlab.rb && \
    echo "nginx['redirect_http_to_https'] = true" >> gitlab.rb && \
    echo "letsencrypt['enable'] = false" >> gitlab.rb && \
    echo "gitlab_rails['gitlab_shell_ssh_port'] = 2222" >> gitlab.rb && \
    echo "Port 2222" >> /etc/ssh/sshd_config

WORKDIR /


EXPOSE 80 443 2222
CMD /opt/gitlab/embedded/bin/runsvdir-start& gitlab-ctl reconfigure ; service ssh restart ; bash

#docker build --build-arg MY_HOST=$(docker-machine ip char) -t gitlab 01_dockerfiles/ex03
#docker run -it -e GITLAB_ROOT_PASSWORD=root_root --privileged -p 80:80 -p 443:443 -p 2222:2222 gitlab
#git -c http.sslVerify=false clone