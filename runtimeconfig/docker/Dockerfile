From quay.io/gravitational/debian-mirror@sha256:4b6ec644c29e4964a6f74543a5bf8c12bed6dec3d479e039936e4a37a8af9116

ENV DEBIAN_FRONTEND=noninteractive
ENV APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=1

RUN apt-get update && apt-get install -y --no-install-recommends \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    jq \
    moreutils \
    software-properties-common

RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - \
 && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" \
 && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | apt-key add - \
 && distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
 && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | \
    tee /etc/apt/sources.list.d/nvidia-docker.list \
 && apt-get update \
 && apt-get install -y --no-install-recommends \
    nvidia-container-runtime \
    docker-ce-cli \
 && rm -rf /var/lib/apt/lists/*

WORKDIR /work

COPY src/. .
RUN cp /etc/nvidia-container-runtime/config.toml ./

RUN chmod +x /work/run.sh

CMD ["bash"]
