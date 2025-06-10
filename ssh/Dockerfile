FROM alpine

RUN apk add --no-cache openssh rsync \
  && adduser -D deployer \
  && mkdir -p /home/deployer/.ssh /srv/site \
  && chown -R deployer:deployer /srv/site /home/deployer

COPY authorized_keys /home/deployer/.ssh/authorized_keys

RUN chmod 600 /home/deployer/.ssh/authorized_keys \
  && chmod 700 /home/deployer/.ssh \
  && chown -R deployer:deployer /home/deployer/.ssh \
  && ssh-keygen -A

RUN echo "PasswordAuthentication no" >> /etc/ssh/sshd_config \
  && echo "PermitRootLogin no" >> /etc/ssh/sshd_config \
  && echo "PubkeyAuthentication yes" >> /etc/ssh/sshd_config

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]

