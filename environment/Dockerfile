# hash:sha256:cdf3699239c15d9fa5716ee935d0b0e7df53f434e7f0f609db2ceebb418c1115
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/ubuntu-desktop-igv-fiji-mambaforge:23.1.0-4-python3.10.12-fiji20231107-1617-firefox120.0-igv2.16.1-guacamole1.5.2-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG AWS_ACCESS_KEY_ID
ARG AWS_DEFAULT_REGION
ARG AWS_SECRET_ACCESS_KEY

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libxcb-xinerama0=1.14-3ubuntu3 \
    && rm -rf /var/lib/apt/lists/*

RUN pip install -U --no-cache-dir \
    simpleitk==2.5.2 \
    -e git+https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui.git@3c787f7c23c098ec1591f535de3757c5cb1994ef#egg=ibl-ephys-alignment-gui
