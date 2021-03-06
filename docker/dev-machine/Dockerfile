FROM ubuntu:16.04
MAINTAINER Martin Bonneville

RUN apt-get update --fix-missing

# Install x11vnc and dependencies
# Install icewm (window manager)
# Install xz-utils
# Install cmake
# Install screen
# Install git and some UI utilities
# Install utilities
# Qt5 and QtCreator
# Dependencies on which Visual Studio Code depends
# Firefox
RUN apt-get install -y x11vnc xvfb \
                       icewm \
                       xz-utils \
                       cmake \
                       screen \
                       git gitk git-gui \
                       wget bzip2 vim nano \
                       qt5-default qtcreator \
                       libnss3 libnotify4 \
                       firefox

# RUN DEBIAN_FRONTEND=noninteractive apt-get install -y kubuntu-desktop
# Install Konsole
RUN apt-get install -y konsole

# Fetch and install Visual Studio Code
RUN wget https://az764295.vo.msecnd.net/stable/653f8733dd5a5c43d66d7168b4701f94d72b62e5/code_1.10.1-1488415350_amd64.deb -O code.deb && \
    dpkg -i code.deb && \
    rm code.deb

# Fetch and install NodeJS
RUN wget https://nodejs.org/dist/v6.10.0/node-v6.10.0-linux-x64.tar.xz -O node.tar.xz && \
    tar xvf node.tar.xz && \
    mv node-* /opt/node && \
    rm node.tar.xz

# Clean
RUN apt-get clean

# Add a user
RUN useradd -m -s /bin/bash icebaby

# The next commands will be run as the new user
USER icebaby

# Add NodeJS to the PATH
ENV PATH /opt/node/bin:$PATH

# Create some useful default aliases
RUN bash -c 'echo "alias cp=\"cp -i\"" >> ~/.bash_aliases' && \
    bash -c 'echo "alias mv=\"mv -i\"" >> ~/.bash_aliases' && \
    bash -c 'echo "alias rm=\"rm -i\"" >> ~/.bash_aliases'

# Auto start icewm in the ~/.bashrc (if it's not running)
RUN bash -c 'echo "if ! pidof -x \"icewm\" > /dev/null; then nohup icewm &>> ~/icewm.log & fi" >> ~/.bashrc'

# Set the working directory
VOLUME /mydata
WORKDIR /mydata

# The port where x11vnc will be running
EXPOSE 5900

# Run x11vnc on start
CMD x11vnc -create -forever -usepw -repeat
