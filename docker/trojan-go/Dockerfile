# Dockerfile for trojan-go based alpine
# Copyright (C) 2019 - 2020 Teddysun <i@teddysun.com>
# Reference URL:
# https://github.com/p4gefau1t/trojan-go
# https://github.com/v2ray/v2ray-core
# https://github.com/v2ray/geoip
# https://github.com/v2ray/domain-list-community

FROM alpine:latest
MAINTAINER Jay

ENV TZ=Asia/Shanghai

# Select folder
WORKDIR /app
COPY . .

# Assign authority
RUN chgrp -R 0 . && \
    chmod -R g=u .
	
RUN set -ex \
	&& apk add --no-cache tzdata ca-certificates \
	&& chmod +x /app/trojan-go.sh \
	&& /app/trojan-go.sh \
	&& rm -fv /app/trojan-go.sh \
	&& wget -O /usr/bin/geosite.dat https://github.com/v2ray/domain-list-community/releases/latest/download/dlc.dat \
	&& wget -O /usr/bin/geoip.dat https://github.com/v2ray/geoip/releases/latest/download/geoip.dat

USER 1001

EXPOSE 443
CMD [ "/usr/bin/trojan-go", "-config", "/etc/trojan-go/config.json" ]
