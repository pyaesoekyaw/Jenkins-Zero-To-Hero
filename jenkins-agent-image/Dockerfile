FROM maven:3-openjdk-17-slim

# Install essential tools: curl, gnupg, and apt-transport-https
# These are needed to correctly add and use Docker's APT repository.
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release && \
    rm -rf /var/lib/apt/lists/*

# Add Docker's official GPG key
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

# Set up the stable Docker repository
# Using 'debian' path as 'maven:*-slim' images are typically Debian-based.
# Adjust 'stable' to 'bookworm', 'bullseye', etc., if 'lsb_release -cs' gives a specific Debian codename
# that isn't mapping to 'stable' correctly. For now, 'stable' should be fine.
RUN echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install the Docker CLI (only the client, not the daemon)
RUN apt-get update && \
    apt-get install -y --no-install-recommends docker-ce-cli && \
    rm -rf /var/lib/apt/lists/*

# Add git (if not already present and needed for other steps)
# RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*
RUN apt-get update && apt-get install -y --no-install-recommends git && rm -rf /var/lib/apt/lists/*
# Set working directory (your existing part)
WORKDIR /app
