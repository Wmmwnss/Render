# Base image: Ubuntu 24.04
FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Ho_Chi_Minh

# Update hệ thống và cài đặt công cụ cơ bản
RUN apt-get update && apt-get upgrade -y && \
    apt-get install -y \
    sudo curl wget git vim nano unzip zip tar gzip xz-utils \
    openssh-server net-tools lsof htop build-essential software-properties-common \
    ca-certificates gnupg lsb-release iproute2 iputils-ping \
    && rm -rf /var/lib/apt/lists/*

# Cài Node.js 24.9
RUN curl -fsSL https://deb.nodesource.com/setup_24.x | bash - && \
    apt-get install -y nodejs && \
    npm install -g yarn pnpm

# Cài Java 21 (OpenJDK)
RUN apt-get update && \
    apt-get install -y openjdk-21-jdk && \
    java -version

# Cấu hình SSH
RUN mkdir /var/run/sshd && \
    echo 'root:root' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' /etc/pam.d/sshd && \
    echo "export VISIBLE=now" >> /etc/profile

# Tạo user vscode có sudo
RUN useradd -m vscode && echo "vscode:vscode" | chpasswd && adduser vscode sudo

# Tạo thư mục làm việc
WORKDIR /workspace
RUN chown vscode:vscode /workspace

# Cài các tiện ích server / network dev
RUN apt-get update && apt-get install -y \
    openssl socat netcat-traditional tcpdump telnet nmap \
    && rm -rf /var/lib/apt/lists/*

# Mở port SSH
EXPOSE 22

# Mặc định chạy shell
CMD ["/usr/sbin/sshd", "-D"]
