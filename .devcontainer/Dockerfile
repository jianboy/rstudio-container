# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.233.0/containers/java-8/.devcontainer/base.Dockerfile

# [Choice] Debian OS version (use bullseye on local arm64/Apple Silicon): buster, bullseye
ARG VARIANT="bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/java:0-8-${VARIANT}

RUN apt-get update \
&& apt install r-base-core r-base-dev \
&& apt install wget  \
&& wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-2022.02.2-485-amd64.deb  \
&& apt-get install gdebi-core  \
&& gdebi rstudio-server-2022.02.2-485-amd64.deb

WORKDIR /workspaces
RUN adduser lyq -p admin \
&& usermod -a -G vscode lyq

ENV R_LIBS_USER=/root/RemoteWorking/tools/RPackages

CMD ["rstudio-server","start"]

# ENV PATH=$PATH:$FLUTTER_HOME/bin
