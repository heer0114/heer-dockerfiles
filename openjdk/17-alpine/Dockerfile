# 使用 Alpine Linux 作为基础镜像
FROM alpine:latest
# 作者
MAINTAINER  "Heer Liu"
# 安装 OpenJDK 17
RUN apk update && apk -U --no-cache add openjdk17 \
    && rm -rf /var/cache/apk/*
# 设置 Java 环境变量
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk
ENV PATH="$PATH:$JAVA_HOME/bin"
# 打印Java版本
ENTRYPOINT java -version
