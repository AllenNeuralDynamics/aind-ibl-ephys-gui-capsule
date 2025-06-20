# hash:sha256:edfac2966ef85e7a556d57d7afa3d3c8596e65a9b453eecf058f314833bf6a40
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/ubuntu-desktop-igv-fiji-mambaforge:23.1.0-4-python3.10.12-fiji20231107-1617-firefox120.0-igv2.16.1-guacamole1.5.2-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG AWS_ACCESS_KEY_ID
ARG AWS_DEFAULT_REGION
ARG AWS_SECRET_ACCESS_KEY

ARG GIT_ASKPASS
ARG GIT_ACCESS_TOKEN
COPY git-askpass /

RUN pip install -U --no-cache-dir \
    -e git+https://github.com/AllenNeuralDynamics/ibl-ephys-alignment-gui.git@3c787f7c23c098ec1591f535de3757c5cb1994ef#egg=ibl-ephys-alignment-gui
