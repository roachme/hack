FROM kalilinux/kali-rolling:latest

# Set non-interactive mode to avoid prompts during package installation
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install vim, exploitdb, and sudo
RUN apt-get update && \
    apt-get install -y \
    vim \
    exploitdb \
    sudo \
    bsdextrautils \
    python3 \
    python3-requests \
    iputils-ping \
    curl \
    nmap \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Create user 'roach' with home directory and add to sudo group
RUN useradd -m -s /bin/bash roach && \
    echo "roach:roach" | chpasswd && \
    usermod -aG sudo roach

# Configure sudo to allow 'roach' to run commands without password (optional)
# Remove this line if you want to require password for sudo
RUN echo "roach ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Set the default working directory to roach's home
WORKDIR /home/roach

# Switch to non-root user
USER roach

# Create a .vimrc with basic settings for the user
RUN echo "syntax on" >> /home/roach/.vimrc && \
    echo "set number" >> /home/roach/.vimrc && \
    echo "set tabstop=4" >> /home/roach/.vimrc && \
    echo "set shiftwidth=4" >> /home/roach/.vimrc && \
    echo "set expandtab" >> /home/roach/.vimrc

# Default command
CMD ["/bin/bash"]
