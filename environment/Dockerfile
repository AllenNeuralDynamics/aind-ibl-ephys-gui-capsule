# hash:sha256:da766ec41f1c62fcf98c534d742ba624da8dfb3bbac6b6bb10e720d667ff0bc8
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/ubuntu-desktop-igv-fiji-mambaforge:23.1.0-4-python3.10.12-fiji20231107-1617-firefox120.0-igv2.16.1-guacamole1.5.2-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-askpass /

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libxcb-xinerama0=1.14-3ubuntu3 \
    && rm -rf /var/lib/apt/lists/*

RUN --mount=type=secret,id=git-access-token \
    GIT_ACCESS_TOKEN="$(cat /run/secrets/git-access-token)" \
    pip install -U --no-cache-dir \
    simpleitk==2.5.2 \
    -e git+https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui.git@a4557113344225a569c56bc4c86285f09acb0109#egg=ibl-ephys-alignment-gui
