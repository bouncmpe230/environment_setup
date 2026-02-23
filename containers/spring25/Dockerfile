FROM docker.io/library/ubuntu:24.04
ARG TARGETARCH TARGETOS TARGETPLATFORM TARGETVARIANT

# Set noninteractive mode to avoid prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install necessary tools
RUN apt-get update && apt-get install -y \
    build-essential \
    gcc \
    g++ \
    make \
    cmake \
    nasm \
    nano \
    vim \
    gdb \
    clang \
    llvm \
    lldb \
    binutils \
    manpages-dev \
    strace \
    ltrace \
    valgrind \
    git \
    wget \
    gnupg2 \
    ca-certificates \
    sudo \
    net-tools \
    openssh-client \
    ninja-build \
    python3-minimal \
    python3-pip \
    && apt-get autoremove -y && rm -rf /var/lib/apt/lists/*

# Set up user environment
RUN groupadd bouncmpe230 -g 2000 && \
    useradd -ms /bin/bash bouncmpe230 -g bouncmpe230 -u 2000 && \
    printf "bouncmpe230 ALL=(ALL) NOPASSWD: ALL\n" >> /etc/sudoers

# Set locale and theme
ENV LC_ALL=C.UTF-8 \
    LANG=C.UTF-8 \
    LANGUAGE=C.UTF-8

USER bouncmpe230
WORKDIR /home/bouncmpe230

# Install Python packages
RUN python3 -m pip install --no-cache-dir --break-system-packages --user meson numpy pandas matplotlib

# Default command: Open a shell
CMD ["/bin/bash"]