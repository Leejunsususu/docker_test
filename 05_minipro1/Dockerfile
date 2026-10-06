FROM quay.io/centos/centos:stream10

RUN dnf install -y vsftpd \ 
    && dnf clean all   

COPY vsftpd.conf.template /etc/vsftpd/vsftpd.conf

VOLUME /var/ftp/pub
COPY WelcomeToMyFTPServer.txt /var/ftp/pub/

EXPOSE 21/tcp
EXPOSE 20/tcp

ENTRYPOINT ["/usr/sbin/vsftpd"]