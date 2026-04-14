FROM pengchuanzhang/pytorch:ubuntu20.04_torch1.9-cuda11.3-nccl2.9.9

# Set user arguments (being username, echo $UID, and id -g)
ARG USERNAME=user
ARG USER_UID=1000
ARG USER_GID=1000

# Install GLIP dependencies
RUN pip install einops shapely timm yacs tensorboardX ftfy prettytable pymongo && \
    pip install transformers

# Create a non-root user with matching UID/GID
RUN groupadd --gid ${USER_GID} ${USERNAME} && \
    useradd --uid ${USER_UID} --gid ${USER_GID} -m ${USERNAME} && \
    usermod -aG sudo ${USERNAME} && \
    echo "${USERNAME} ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

# Add a custom .bashrc with warm colors and fixed hostname
RUN echo 'export PS1="\\[\\e[1;31m\\]\\u@glip_container\\[\\e[0m\\]:\\[\\e[1;33m\\]\\w\\[\\e[0m\\]\\$ "' > /home/${USERNAME}/.bashrc && \
    chown ${USERNAME}:${USERNAME} /home/${USERNAME}/.bashrc

# Set default user & shell
USER ${USERNAME}
WORKDIR /home/${USERNAME}
SHELL ["/bin/bash", "-c"]
RUN echo "export USER=${USERNAME}" >> ~/.bashrc
