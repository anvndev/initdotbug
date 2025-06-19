FROM node:18-bullseye

# Install Ruby and development dependencies
RUN apt-get update && apt-get install -y \
    ruby \
    ruby-dev \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Install Bundler
RUN gem install bundler