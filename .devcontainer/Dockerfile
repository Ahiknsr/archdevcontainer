FROM archlinux:latest

RUN sed -i 's/#en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && locale-gen && echo "LANG=en_US.UTF-8" > /etc/locale.conf

RUN pacman -Syu --noconfirm && \
    pacman -S --noconfirm sudo && \
    useradd --create-home --shell /bin/bash --groups wheel vscode && \
    echo '%wheel ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers

RUN useradd -m builder && echo "builder ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers

RUN pacman -Syu --noconfirm && \
    pacman -S --noconfirm base-devel git gcc htop lsof 

# For GUI and OpenGL with nvidia
RUN pacman -Syu --noconfirm && \
    pacman -S --noconfirm mesa mesa-utils mesa-libgl glfw nvidia nvidia-utils    

RUN usermod -aG video,render vscode    

# yay can't run as root
USER builder
WORKDIR /home/builder

# RUN git clone https://aur.archlinux.org/yay.git && \
#     cd yay && \
#     makepkg -si --noconfirm

# RUN yay -S --noconfirm julia-bin

USER vscode
CMD [ "/bin/bash" ]