FROM maven:3-openjdk-17-slim

# Install Docker CLI and Git (your existing RUN commands from previous steps)
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    apt-transport-https ca-certificates curl gnupg lsb-release git && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && \
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/debian \
    $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null && \
    apt-get update && \
    apt-get install -y docker-ce-cli && \
    rm -rf /var/lib/apt/lists/*

# --- ADD THESE NEW LINES WITH YOUR SPECIFIC UIDs/GIDs ---
ARG JENKINS_UID=111  # <--- YOUR SPECIFIC UID
ARG JENKINS_GID=113  # <--- YOUR SPECIFIC GID

# Create a group (if it doesn't exist) and a user inside the container
# with the exact UID and GID of the Jenkins user on the host.
# Then, add this user to the 'docker' group *inside the container*.
RUN if ! getent group "${JENKINS_GID}"; then groupadd -g "${JENKINS_GID}" jenkins; fi && \
    useradd -u "${JENKINS_UID}" -g "${JENKINS_GID}" -m jenkins && \
    usermod -aG docker jenkins # Add 'jenkins' user inside container to 'docker' group inside container

USER jenkins # Switch to this newly created user for all subsequent commands and at runtime
# --- END NEW LINES ---

WORKDIR /app # Your existing WORKDIR line
