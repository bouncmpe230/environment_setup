FROM docker.io/library/ubuntu:24.04

ARG TARGETARCH TARGETOS TARGETPLATFORM TARGETVARIANT
ENV DEBIAN_FRONTEND=noninteractive

# ---- Base tooling for systems programming: Unix + C/C++ + debugging + build ----
RUN apt-get update && apt-get install -y --no-install-recommends \
    # Core toolchain
    build-essential \
    gcc g++ gdb \
    clang llvm lldb \
    make cmake ninja-build meson \
    binutils \
    pkg-config \
    bash-completion \
    coreutils \
    findutils \
    grep sed gawk \
    less \
    man-db manpages manpages-dev \
    file \
    tree \
    curl wget \
    git \
    openssh-client \
    ca-certificates gnupg2 \
    sudo \
    net-tools iproute2 iputils-ping \
    # Debugging / tracing / profiling
    strace ltrace \
    valgrind \
    perf-tools-unstable \
    # (optional but nice) editors
    nano vim \
    # Python minimal for scripting / tooling in PS
    python3-minimal python3-pip \
    # Locale
    locales \
    && rm -rf /var/lib/apt/lists/*

# ---- Code quality / documentation tools ----
RUN apt-get update && apt-get install -y --no-install-recommends \
    clang-format clang-tidy cppcheck \
    doxygen graphviz \
    zip unzip \
    netcat-openbsd tcpdump \
    && rm -rf /var/lib/apt/lists/*

# ---- Locale (UTF-8) ----
RUN locale-gen en_US.UTF-8
ENV LC_ALL=en_US.UTF-8 \
    LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en

# ---- Light Qt development (no IDE; just build tools + libs) ----
# This keeps it “light”: Qt base + qmake/cmake integration, but not Qt Creator.
# RUN apt-get update && apt-get install -y --no-install-recommends \
#     qtbase5-dev \
#     qtchooser \
#     qt5-qmake \
#     qtbase5-dev-tools \
#     && rm -rf /var/lib/apt/lists/*

# ---- User setup ----
RUN groupadd -g 2000 bouncmpe230 && \
    useradd -m -s /bin/bash -u 2000 -g 2000 bouncmpe230 && \
    printf "bouncmpe230 ALL=(ALL) NOPASSWD: ALL\n" >> /etc/sudoers

USER bouncmpe230
WORKDIR /home/bouncmpe230

# ---- Python packages (keep small + useful for PS) ----
# NOTE: --break-system-packages is OK on 24.04 but we install --user anyway.
RUN python3 -m pip install --no-cache-dir --break-system-packages --user \
    numpy pandas matplotlib

# Convenience: ensure ~/.local/bin is on PATH for pip --user installs
ENV PATH="/home/bouncmpe230/.local/bin:${PATH}"

CMD ["/bin/bash"]