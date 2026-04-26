# hash:sha256:14be51104ef8e9485808b5e03e003836e249b30d61e557275b9a4e35a11f86c6
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/ubuntu-desktop-igv-fiji-mambaforge:23.1.0-4-python3.10.12-fiji20231107-1617-firefox120.0-igv2.16.1-guacamole1.5.2-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-ask-pass /

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libxcb-xinerama0=1.14-3ubuntu3 \
    && rm -rf /var/lib/apt/lists/*

RUN --mount=type=secret,id=git-access-token \
    GIT_ACCESS_TOKEN="$(cat /run/secrets/git-access-token)" \
    pip install -U --no-cache-dir \
    simpleitk==2.5.2 \
    -e git+https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui.git@2bf42c7077059d58055193bf7cef3f98760821cb#egg=ibl-ephys-alignment-gui
