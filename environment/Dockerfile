# hash:sha256:e61b107a0ae41fb0effca91be19903eb9db75446ab2e4d0b49456a9a65e552d8
ARG REGISTRY_HOST
FROM $REGISTRY_HOST/codeocean/ubuntu-desktop-igv-fiji-mambaforge:23.1.0-4-python3.10.12-fiji20231107-1617-firefox120.0-igv2.16.1-guacamole1.5.2-ubuntu22.04

ARG DEBIAN_FRONTEND=noninteractive
ARG GIT_ASKPASS
COPY git-ask-pass /

ENV EPHYS_ALIGNMENT_INPUT_ROOT='/data'
ENV EPHYS_ALIGNMENT_OUTPUT_ROOT='/results'
ENV IBL_ASSET_ROOTS='/data'

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libxcb-cursor0=0.1.1-4ubuntu1 \
        libxcb-xinerama0=1.14-3ubuntu3 \
        zenity=3.42.1-0ubuntu1 \
    && rm -rf /var/lib/apt/lists/*

COPY postInstall /
RUN --mount=type=secret,id=secrets . /run/secrets/secrets \
    && /postInstall
