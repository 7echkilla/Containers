FROM ubuntu:22.04

# avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# install core dependencies
RUN apt-get update && apt-get install -y apt-utils \
    libx11-6 libxi6 libxrandr2 libxinerama1 libxcursor1 libxkbcommon0 \
    libasound2 libpulse0 alsa-utils \
    pulseaudio \
    wget unzip git build-essential \
    libgl1-mesa-dev mesa-utils libwayland-cursor0 x11-apps \
    && rm -rf /var/lib/apt/lists/*

# download and install Godot
RUN wget https://github.com/godotengine/godot/releases/download/4.5-stable/Godot_v4.5-stable_linux.x86_64.zip -O /tmp/godot.zip \
    && unzip /tmp/godot.zip -d /usr/local/bin \
    && mv /usr/local/bin/Godot_v4.5-stable_linux.x86_64 /usr/local/bin/godot \
    && chmod +x /usr/local/bin/godot \
    && rm /tmp/godot.zip

ARG USER_ID=1000
ARG GROUP_ID=1000

RUN groupadd -g $GROUP_ID devuser && \
    useradd -m -u $USER_ID -g $GROUP_ID -s /bin/bash devuser

# set working directory and home
USER devuser
WORKDIR /workspace
