# Use a Maven image that includes OpenJDK 17
# You can find various options on Docker Hub, e.g., 'maven:3.9.6-openjdk-17-slim'
FROM maven:3-openjdk-17-slim

# You need Docker CLI inside this agent if it needs to run Docker commands itself.
# Your current Jenkinsfile mounts the host's Docker socket, which is good,
# but the agent container still needs the 'docker' CLI.
# This part might already be included in 'abhishekf5/maven-abhishek-docker-agent:v1'
# but if you start from a 'maven' base, you might need to add it.
# Check the documentation for 'maven:*-openjdk-17-slim' if it includes docker cli.
# If not, you might need to install it:
# RUN apt-get update && apt-get install -y --no-install-recommends \
#     docker.io \
#     && rm -rf /var/lib/apt/lists/*

# Set up a non-root user if desired for better security (optional but recommended)
# ARG UID=1000
# ARG GID=1000
# RUN groupadd -g ${GID} jenkins && useradd -u ${UID} -g jenkins -m jenkins
# USER jenkins

# Set working directory
WORKDIR /app

# The original 'abhishekf5/maven-abhishek-docker-agent:v1' likely has other tools.
# Add any other tools your pipeline needs (e.g., git, curl, etc.)
# RUN apt-get update && apt-get install -y git curl && rm -rf /var/lib/apt/lists/*

# Set JAVA_HOME explicitly if needed, though most OpenJDK images set it
# ENV JAVA_HOME /usr/lib/jvm/java-17-openjdk-amd64
# ENV PATH $JAVA_HOME/bin:$PATH
