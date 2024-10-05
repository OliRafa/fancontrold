FROM rust:1.81

# Install common packages
RUN apt update \
    && apt upgrade -y \
    && apt install -y curl git \
    && apt autoremove \
    && apt-get clean

# Install Docker
RUN curl -fsSL https://get.docker.com -o get-docker.sh \
    && sh get-docker.sh \
    && usermod -aG docker root \
    && apt autoremove \
    && apt-get clean

# Install Docker Compose
RUN LATEST_COMPOSE_VERSION=$(curl -sSL "https://api.github.com/repos/docker/compose/releases/latest" | grep -o -P '(?<="tag_name": ").+(?=")') \
    && curl -sSL "https://github.com/docker/compose/releases/download/${LATEST_COMPOSE_VERSION}/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

# Install ZSH, Oh My Zsh, p10k and ZSH-Autosuggestions
RUN apt install -y zsh \
    && apt autoremove \
    && apt-get clean

RUN sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)" \
    && git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k \
    && git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# Make ZSH the default shell
RUN usermod -s $(which zsh) root

# Install and configure Commitizen and iPython
# RUN pip3 install --no-cache-dir -U commitizen ipython
