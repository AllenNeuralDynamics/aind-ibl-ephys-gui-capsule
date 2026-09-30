# hash:sha256:0105c62702527a5e969a81124626dacb985cac5cad8e2a06a3805244b74a33ef
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/ubuntu-desktop-igv-fiji-mambaforge:23.1.0-4-python3.10.12-fiji20231107-1617-firefox120.0-igv2.16.1-guacamole1.5.2-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-ask-pass /

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libxcb-cursor0=0.1.1-4ubuntu1 \
        libxcb-xinerama0=1.14-3ubuntu3 \
        zenity=3.42.1-0ubuntu1 \
    && rm -rf /var/lib/apt/lists/*

COPY postInstall /
RUN --mount=type=secret,id=secrets . /run/secrets/secrets \
    && /postInstall
