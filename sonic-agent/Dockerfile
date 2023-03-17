FROM ubuntu:jammy-20221130

ENV DEBIAN_FRONTEND=noninteractive

ENV SDK_VERSION=commandlinetools-linux-7583922_latest

WORKDIR /root

RUN apt-get -qqy update && \
    apt-get -qqy --no-install-recommends install \
    ca-certificates \
    usbmuxd \
    zip \
    unzip \
    curl \
    wget \
    libqt5webkit5 \
    libgconf-2-4 \
    gnupg \
    salt-minion \
    libasound2-dev freeglut3-dev libgtk2.0-dev libusb-dev zlib1g libffi-dev libnss3 libbz2-dev zlib1g-dev \
  && rm -rf /var/lib/apt/lists/* \
  && apt-get clean

RUN wget -O java.tar.gz https://github.com/AdoptOpenJDK/openjdk17-binaries/releases/download/jdk-2021-05-07-13-31/OpenJDK-jdk_x64_linux_hotspot_2021-05-06-23-30.tar.gz && \
    tar zxvf java.tar.gz && rm java.tar.gz && \
    chmod a+x -R /root/jdk-17+20 && \
    chown -R root:root /root/jdk-17+20

ENV JAVA_HOME="/root/jdk-17+20" \
    PATH=$PATH:$JAVA_HOME/bin

ENV ANDROID_HOME=/root

RUN mkdir -p $ANDROID_HOME/cmdline-tools && \
    cd $ANDROID_HOME/cmdline-tools && \
    wget -O tools.zip https://dl.google.com/android/repository/${SDK_VERSION}.zip && \
    unzip tools.zip && rm tools.zip && \
    mv ./* ./latest && \
    chmod a+x -R $ANDROID_HOME && \
    chown -R root:root $ANDROID_HOME

ENV PATH=$PATH:$ANDROID_HOME/cmdline-tools/latest:$ANDROID_HOME/cmdline-tools/latest/bin

RUN mkdir -p ~/.android && \
    touch ~/.android/repositories.cfg && \
    echo y | sdkmanager "platform-tools"

ENV PATH=$PATH:$ANDROID_HOME/platform-tools

RUN adb devices && mkdir -p mini plugins config
