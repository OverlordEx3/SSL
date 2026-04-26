FROM ubuntu:26.04
ARG DEBIAN_FRONTEND=noninteractive

# Instalar paquetes de desarrollo:
# Versiones elegidas:
ARG BUILDESSENTIAL_VERSION=12.12ubuntu2
ARG MANDB_VERSION=2.13.1-1build1

# Borra man de la lista de exclusion, e instala los paquetes
# mencionados arriba
RUN set -eux && \
    rm /etc/dpkg/dpkg.cfg.d/excludes && \
    apt-get update -y -qq && \
    apt-get install -y -qq --no-install-recommends man-db=${MANDB_VERSION} && \
    apt-get install -y -qq --no-install-recommends build-essential=${BUILDESSENTIAL_VERSION} && \
    apt-get autoremove -y -qq && \
    apt-get clean -y -qq && \
    rm -f /usr/bin/man && \
    dpkg-divert --quiet --remove --rename /usr/bin/man && \
    rm -f /etc/update-motd.d/60-unminimize

# Configura el directorio de trabajo por defecto de la imagen, donde
# van a correr todos los comandos. En este directorio se deberian
# montar los archivos de código
WORKDIR /app

# Comando por defecto, inicia una shell para permitir ejecutar comandos
# Overrideable cuando se lance el project con CMD en docker-compose.yml
CMD ["/bin/bash"]