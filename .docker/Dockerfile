# Container image that runs your code
FROM ubuntu:latest

ARG USERNAME=user
ARG USER_UID=10001
ARG USER_GID=$USER_UID

COPY ./conanfile.txt /tmp

RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && apt-get update \
    && apt-get install -y --no-install-recommends \
    sudo \
    && rm -rf /var/lib/apt/lists/* \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME \
    && mkdir -p /home/$USERNAME \
    && chown $USER_UID:$USER_GID /home/$USERNAME


RUN apt-get update && sudo apt-get upgrade -y && apt-get install -y --no-install-recommends\
    binutils \
    cmake \
    pkg-config \
    clang \
    clang-format \
    clang-tidy \
    clangd \
    git \
    make \
    valgrind \
    ssh \
    python3 \ 
    pipx \ 
    llvm \
    ninja-build \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update && apt-get install -y --no-install-recommends\
    libfontconfig1-dev \
    libfreetype-dev \
    libx11-dev \
    libx11-xcb-dev \
    libxext-dev \
    libxfixes-dev \
    libxi-dev \
    libxrender-dev \
    libxcb1-dev \
    libxcb-cursor-dev \
    libxcb-glx0-dev \
    libxcb-keysyms1-dev \
    libxcb-image0-dev \
    libxcb-shm0-dev \
    libxcb-icccm4-dev \
    libxcb-sync-dev \
    libxcb-xfixes0-dev \
    libxcb-shape0-dev \
    libxcb-randr0-dev \
    libxcb-render-util0-dev \
    libxcb-util-dev \
    libxcb-xinerama0-dev \
    libxcb-xkb-dev \
    libxkbcommon-dev \
    libxkbcommon-x11-dev \
    libgl1-mesa-dev \
    libgl-dev \
    libfontenc-dev \
    libice-dev \
    libsm-dev \ 
    libxaw7-dev \
    libxcomposite-dev \
    libxcursor-dev \
    libxdamage-dev \
    libxinerama-dev \
    libxkbfile-dev \
    libxmu-dev \
    libxmuu-dev \
    libxpm-dev \
    libxrandr-dev \
    libxres-dev \
    libxss-dev \
    libxt-dev \
    libxtst-dev \
    libxv-dev \
    libxxf86vm-dev \
    libxcb-dri3-dev \
    libxcb-dri2-0-dev \
    libxcb-dri3-dev \
    libxcb-present-dev \
    libxcb-composite0-dev \
    libxcb-ewmh-dev \
    libxcb-res0-dev \
    llvm-dev \
    libclang-dev \
    && rm -rf /var/lib/apt/lists/*
   
USER $USER_UID:$USER_GID

RUN pipx ensurepath && pipx install conan

WORKDIR /workspaces/MyTest

ENV CONAN_CMAKE_GENERATOR=Ninja

RUN /home/user/.local/bin/conan profile detect 
# && /home/user/.local/bin/conan install -v --build=missing /tmp/conanfile.txt

ENV TERM=xterm-256-colors