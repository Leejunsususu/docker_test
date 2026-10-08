FROM ubuntu:22.04

# non-interactive 모드 설정 (설치 중 입력을 기다리지 않음)
ENV DEBIAN_FRONTEND=noninteractive

# 메일 서버 필수 패키지 설치 (Postfix, Dovecot)
RUN apt-get update && apt-get install -y \
    postfix \
    dovecot-imapd \
    dovecot-pop3d \
    syslog-ng \
    net-tools \
    vim \
    && rm -rf /var/lib/apt/lists/*

# Postfix 기본 설정 (로컬 도메인 설정)
RUN postconf -e "myhostname = mail.example.com" \
    && postconf -e "mydomain = example.com" \
    && postconf -e "myorigin = example.com" \
    && postconf -e "inet_interfaces = all" \
    && postconf -e "mydestination = \$myhostname, localhost.\$mydomain, localhost, \$mydomain"

# 서비스 실행 스크립트 작성
RUN echo '#!/bin/bash\nservice syslog-ng start\nservice postfix start\nservice dovecot start\ntail -f /var/log/syslog' > /entrypoint.sh \
    && chmod +x /entrypoint.sh

# SMTP(25), IMAP(143), POP3(110) 포트 노출
EXPOSE 25 110 143

ENTRYPOINT ["/entrypoint.sh"]
