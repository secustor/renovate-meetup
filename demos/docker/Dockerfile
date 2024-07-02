FROM ghcr.io/google/osv-scanner:v1.3.1 as osv

FROM node:20-slim@sha256:d71e0d460434ef500c6d962bcdc6ebe717e5939025dd8aa9746dd76fa12ee6e3

RUN apt-get update && apt-get install -y --no-install-recommends \
  wget \
  ca-certificates \
&& \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

# install tooling
COPY --from=osv osv-scanner /usr/local/bin

# renovate: datasource=github-releases depName=aquasecurity/trivy extractVersion=true
ARG TRIVY_VERSION=0.40.0
RUN wget -c https://github.com/aquasecurity/trivy/releases/download/v${TRIVY_VERSION}/trivy_${TRIVY_VERSION}_Linux-64Bit.tar.gz -O - | \
        tar -xzC /usr/local/bin trivy
