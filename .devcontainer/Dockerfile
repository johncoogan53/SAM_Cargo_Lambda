# Use the official Rust image as the base
FROM rust:latest

# Install dependencies
RUN apt-get update && apt-get install -y \
    sudo \
    curl \
    build-essential \
    libssl-dev \
    pkg-config \
    && rm -rf /var/lib/apt/lists/*

# Install Homebrew
RUN curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh | bash \
    && echo 'eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)' >> /root/.profile \
    && echo 'eval $(/home/linuxbrew/.linuxbrew/bin/brew shellenv)' >> /root/.bashrc

# Use /bin/bash to source the profile and bashrc
RUN /bin/bash -c "source /root/.profile && source /root/.bashrc"

# Install cargo-lambda
RUN /bin/bash -c "source /root/.profile && brew tap cargo-lambda/cargo-lambda && brew install cargo-lambda"
  
# Install AWS SAM CLI
RUN curl -Lo aws-sam-cli.zip https://github.com/aws/aws-sam-cli/releases/latest/download/aws-sam-cli-linux-x86_64.zip \
    && unzip aws-sam-cli.zip -d sam-installation \
    && ./sam-installation/install

# Update Rust and add components
RUN rustup update \
    && rustup component add clippy \
    && rustup component add rustfmt

# Set the working directory
WORKDIR /workspaces/SAM_Lambda_DynDB