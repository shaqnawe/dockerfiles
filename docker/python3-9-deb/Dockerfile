
# Last modified: 2024-08-08T00:14:37.838087+00:00
FROM python:3.9.19-slim-bullseye

RUN echo 'deb http://deb.debian.org/debian bullseye-backports main' >> /etc/apt/sources.list

# Basic linux utilities
RUN apt-get update && apt-get install -y --no-install-recommends \
  procps \
&& rm -rf /var/lib/apt/lists/*

# Upgrade all packages to latest
RUN apt-get update && apt-get -y --no-install-recommends upgrade \
&& rm -rf /var/lib/apt/lists/*

# Upgrade using backports
RUN apt-get update && apt-get -t bullseye-backports -y --no-install-recommends upgrade \
&& rm -rf /var/lib/apt/lists/*

COPY requirements.txt .

#Install tools for building binary deps (will be reomved later on)
RUN apt-get update && apt-get install -y --no-install-recommends \
  gcc \
  python3.9-dev \
  build-essential \
&& pip install --upgrade pip setuptools && pip install --no-cache-dir -r requirements.txt \
&& apt-get purge -y --auto-remove \
  gcc \
  python3.9-dev \
  build-essential \
&& rm -rf /var/lib/apt/lists/*


RUN groupadd --gid 4000 demisto \
  && useradd --uid 4000 --gid demisto --shell /bin/bash --create-home demisto
