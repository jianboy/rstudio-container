# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.233.0/containers/java-8/.devcontainer/base.Dockerfile

# [Choice] Debian OS version (use bullseye on local arm64/Apple Silicon): buster, bullseye
ARG VARIANT="bullseye"
FROM mcr.microsoft.com/vscode/devcontainers/java:0-8-${VARIANT}

WORKDIR /home/vscode
ENV CRAN_URL=https://cloud.r-project.org/
ENV R_LIBS_USER=/workspaces/RStudio-container/tools/RPackages

# install R
RUN apt-get update \
&& apt install -y r-base-core r-base-dev

# install RStudio-server
RUN apt install -y wget  \
&& wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-2022.02.2-485-amd64.deb  \
&& apt-get install -y gdebi-core  \
&& gdebi -n rstudio-server-2022.02.2-485-amd64.deb \
&& rm rstudio-server-2022.02.2-485-amd64.deb

# set user and pwd: rstudio/rstudio
WORKDIR /workspaces
# RUN set -eo pipefail \
#       && ln -s /dev/stdout /var/log/syslog \
RUN echo "r-cran-repos=${CRAN_URL}" >> /etc/rstudio/rsession.conf \
      && useradd -m -d /home/rstudio rstudio \
      && usermod -a -G vscode rstudio \
      && echo rstudio:rstudio | chpasswd  \
      && mkdir -p /home/rstudio/workspaces \
      && ln -s /workspaces/RStudio-container /home/rstudio/workspaces

RUN apt-get -y autoremove \
&& apt-get clean \
&& rm -rf /var/lib/apt/lists/*

EXPOSE 8787

ENTRYPOINT ["/usr/lib/rstudio-server/bin/rserver"]
CMD ["--server-daemonize=0", "--server-app-armor-enabled=0"]