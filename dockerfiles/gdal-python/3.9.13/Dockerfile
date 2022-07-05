# -----
FROM python:3.9.13-slim-buster 

ENV \
    # python:
    PYTHONFAULTHANDLER=1 \
    PYTHONUNBUFFERED=1 \
    PYTHONHASHSEED=random \
    PYTHONDONTWRITEBYTECODE=1 \
    # pip:
    PIP_NO_CACHE_DIR=off \
    PIP_DISABLE_PIP_VERSION_CHECK=on \
    PIP_DEFAULT_TIMEOUT=100 

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN  apt-get update \
  && apt-get install --no-install-recommends -y \
    build-essential=12.6 \
    curl=7.64.0-4+deb10u2 \
    binutils=2.31.1-16 \
    libproj-dev=5.2.0-1 \
    libgdal-dev=2.4.0+dfsg-1+b1 \
    gdal-bin=2.4.0+dfsg-1+b1 \
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
  && apt-get clean -y  \
  && rm -rf /var/lib/apt/lists/*
