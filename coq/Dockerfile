FROM debian:9
LABEL maintainer="erik@martin-dorel.org"

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    aspcud \
    build-essential \
    ca-certificates \
    curl \
    git \
    m4 \
    ocaml-best-compilers \
    ocaml-core \
    opam \
    pkg-config \
    rsync \
    time \
  && echo "ocamlc -version => $(ocamlc -version)" \
  && echo "opam --version => $(opam --version)" \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*

# Add system group and user
RUN groupadd -r coq \
  && useradd --no-log-init -r -m -s /bin/bash -g coq coq

USER coq
WORKDIR /home/coq

# Create dirs for user scripts
RUN mkdir -p -v bin .local/bin
# no need for "chown -v coq:coq bin .local/bin"

ENV NJOBS="2"
ENV COMPILER="4.02.3"

# Setup OPAM
RUN ["/bin/bash", "--login", "-c", "set -x \
  && opam init --auto-setup --yes --jobs=${NJOBS} --compiler=${COMPILER} \
  && eval $(opam config env) \
  && opam update \
  && opam config list && opam list"]

ENV COQ_VERSION="8.8.1"

# Install Coq
RUN ["/bin/bash", "--login", "-x", "-c", \
  "opam pin add -n -k version coq ${COQ_VERSION} \
  && opam install -j ${NJOBS} coq \
  && opam list"]

# opam config exec -- make
