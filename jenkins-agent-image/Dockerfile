FROM maven:3-openjdk-17-slim
RUN apk add --no-cache docker-cli
# Install Docker CLI
# This block adds Docker's official GPG key and repository, then installs docker-ce-cli
RUN apt update && \
    apt install -y apt-transport-https ca-certificates curl gnupg lsb-release && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt update && \
    apt install -y docker-ce-cli && \
    rm -rf /var/lib/apt/lists/*

# Add git and other tools if needed for other pipeline steps
# RUN apt-get update && apt-get install -y git && rm -rf /var/lib/apt/lists/*

# Your existing WORKDIR and other commands
WORKDIR /app
