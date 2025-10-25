FROM ubuntu:24.10

# Avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Update package list and install basic tools
RUN apt-get update && apt-get install -y \
    # System tools
    curl \
    wget \
    gnupg \
    software-properties-common \
    ca-certificates \
    lsb-release \
    # File editing tools
    nano \
    vim \
    # Archive tools
    unzip \
    zip \
    tar \
    gzip \
    bzip2 \
    # SSH tools
    openssh-server \
    openssh-client \
    # Network tools
    net-tools \
    iputils-ping \
    dnsutils \
    # Development tools
    git \
    build-essential \
    # Other utilities
    sudo \
    htop \
    tree \
    && rm -rf /var/lib/apt/lists/*

# Install JDK 21
RUN apt-get update && apt-get install -y openjdk-21-jdk && \
    rm -rf /var/lib/apt/lists/*

# Install Node.js 24.x
RUN curl -fsSL https://deb.nodesource.com/setup_24.x | bash - && \
    apt-get install -y nodejs && \
    rm -rf /var/lib/apt/lists/*

# Configure SSH
RUN mkdir /var/run/sshd && \
    echo 'root:password' | chpasswd && \
    sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config && \
    sed -i 's/#PasswordAuthentication yes/PasswordAuthentication yes/' /etc/ssh/sshd_config

# Create a non-root user for development
RUN useradd -m -s /bin/bash developer && \
    echo 'developer:developer' | chpasswd && \
    usermod -aG sudo developer

# Set up working directory
WORKDIR /workspace

# Expose SSH port
EXPOSE 22

# Start SSH service
CMD ["/usr/sbin/sshd", "-D"]
