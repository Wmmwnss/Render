FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

# Install basic tools
RUN apt-get update && apt-get install -y \
    curl wget gnupg software-properties-common \
    nano vim unzip zip tar gzip bzip2 \
    openssh-server openssh-client \
    net-tools iputils-ping dnsutils \
    git build-essential sudo htop tree \
    && rm -rf /var/lib/apt/lists/*

# Install Java 21
RUN apt-get update && apt-get install -y openjdk-21-jdk && \
    rm -rf /var/lib/apt/lists/*

# Install Node.js 20
RUN curl -fsSL https://deb.nodesource.com/setup_24.x | bash - && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*

# Create user
RUN useradd -m -s /bin/bash developer && \
    echo 'developer:developer' | chpasswd && \
    usermod -aG sudo developer

WORKDIR /workspace

USER developer

CMD ["sleep", "infinity"]