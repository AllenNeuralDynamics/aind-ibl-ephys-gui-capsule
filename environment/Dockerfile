# hash:sha256:236858d5c5e2492c292704120c82ec8c1e1550d29606586db186efb2fa5c6b5d
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
    -e git+https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui.git#egg=ibl-ephys-alignment-gui
