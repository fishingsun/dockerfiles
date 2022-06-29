FROM debian:stable-slim

RUN set -ex; \
    \
    # change a mirror for faster network if needed
    sed -i 's/deb.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list; \
    sed -i 's/security.debian.org/mirrors.tuna.tsinghua.edu.cn/g' /etc/apt/sources.list; \
    # refresh the os
    apt-get update; \
    apt-get -uy upgrade; \
    # install required package(s)
    apt-get -y install ca-certificates; \
    update-ca-certificates
    
FROM scratch

COPY --from=0 /usr/share/ca-certificates /usr/share/ca-certificates
COPY --from=0 /etc/ssl/certs /etc/ssl/certs

ADD coredns /coredns

EXPOSE 53 53/udp
ENTRYPOINT ["/coredns"]
