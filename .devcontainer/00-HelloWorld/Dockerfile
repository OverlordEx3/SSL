FROM ubuntu:26.04

# Instalar paquetes de desarrollo:
# Versiones elegidas:
ARG GCC_VERSION=15
ARG GPP_VERSION=15
ARG GDB_VERSION=17.1-2ubuntu1
ARG MAKE_VERSION=4.4.1-3
ARG MANDB_VERSION=2.13.1-1build1
ARG USER_ID=1001
ARG USER_NAME=compiler

# Borra man de la lista de exclusion, e instala los paquetes
# mencionados arriba
RUN set -eux && \
    rm /etc/dpkg/dpkg.cfg.d/excludes && \
    apt-get update -y -qq && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y -qq --no-install-recommends \
        man-db=${MANDB_VERSION} \
        gcc-${GCC_VERSION} \
        g++-${GCC_VERSION} \
        gdb=${GDB_VERSION} \
        make=${MAKE_VERSION} && \
    apt-get autoremove -y -qq && \
    apt-get clean -y -qq && \
    rm -rf /var/lib/apt/lists/* && \
    rm -f /usr/bin/man && \
    dpkg-divert --quiet --remove --rename /usr/bin/man && \
    rm -f /etc/update-motd.d/60-unminimize && \
    update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-15 100 && \
    update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-15 100

# Configura el directorio de trabajo por defecto de la imagen, donde
# van a correr todos los comandos. En este directorio se deberian
# montar los archivos de código
RUN mkdir /src
VOLUME /src

RUN mkdir /output
VOLUME /output

RUN useradd -u ${USER_ID} -m ${USER_NAME}

# Comando por defecto, inicia una shell para permitir ejecutar comandos
# Overrideable cuando se lance el project con CMD en docker-compose.yml
# Configura  el prompt de la terminal para mostrar ssl en lugar del host, que es dinámico
RUN cat <<-EOF >> /home/${USER_NAME}/.bashrc
    # Configura el prompt para que quede ${USER_NAME}@ssl:/src $, por ejemplo
    PS1='\[\e[1;32m\]\u@ssl\[\e[m\]:\[\e[1;34m\]\w\[\e[m\] \$ '

    # Banner
    echo "   __________     _____  _____                _ __       
  / __/ __/ /    / ___/ / ___/__  __ _  ___  (_) /__ ____
 _\ \_\ \/ /__  / /__  / /__/ _ \/  ' \/ _ \/ / / -_) __/
/___/___/____/  \___/  \___/\___/_/_/_/ .__/_/_/\__/_/   
                                     /_/                 "

    # Obtengo la version de la tool
    echo "Version de GCC: $(gcc -dumpfullversion)"
    echo "Versiones de lenguaje soportadas:"
    gcc -v --help 2>/dev/null | egrep "^[[:space:]]*-std=(c|gnu)(\+\+)?[1-9]+\S*"

EOF

RUN SNIPPET="export PROMPT_COMMAND='history -a' && export HISTFILE=/commandhistory/.bash_history" \
    && mkdir /commandhistory \
    && touch /commandhistory/.bash_history \
    && chown -R ${USER_NAME} /commandhistory \
    && echo "$SNIPPET" >> "/home/${USER_NAME}/.bashrc"

USER ${USER_NAME}
WORKDIR /src
ENTRYPOINT ["/bin/bash"]