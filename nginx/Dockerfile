FROM nginx:latest

RUN groupadd -g 48 nfsaccess \
 && usermod -aG nfsaccess nginx \
 && usermod -aG nfsaccess www-data

