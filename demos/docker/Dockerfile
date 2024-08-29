FROM ghcr.io/google/osv-scanner:v1.3.1 as osv

FROM node:20-slim@sha256:611c19e435e4948c44936582d543f0e2790bfa0d7688a2a21a380fcd83799d7d

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
