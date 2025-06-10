FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
  && apt-get install -y openssh-server \
  && mkdir /var/run/sshd

RUN useradd -m -s /bin/bash deployer \
  && mkdir /home/deployer/.ssh \
  && mkdir /home/deployer/site

COPY id_ed25519.pub /home/deployer/.ssh/authorized_keys

RUN chown -R deployer:deployer /home/deployer/.ssh /home/deployer/site \
  && chmod 700 /home/deployer/.ssh \
  && chmod 600 /home/deployer/.ssh/authorized_keys

RUN sed -i 's/#PasswordAuthentication yes/PasswordAuthentication no/' /etc/ssh/sshd_config \
  && sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin no/' /etc/ssh/sshd_config \
  && echo 'AllowUsers deployer' >> /etc/ssh/sshd_config

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]

