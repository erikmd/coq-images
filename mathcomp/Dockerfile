FROM erikmd/coq:8.6.1
LABEL maintainer="erik@martin-dorel.org"

ENV MATHCOMP_VERSION="1.7.0"

# Remark 1. This command has already be run in the base image:
# opam repository add coq-released https://coq.inria.fr/opam/released

# Remark 2. This command is unneeded due to the "--login" flag below:
# eval $(opam config env)

RUN ["/bin/bash", "--login", "-c", "set -x \
  && opam update -y \
  && opam pin add -n -k version coq-mathcomp-character ${MATHCOMP_VERSION} \
  && opam install -y -j ${NJOBS} coq-mathcomp-character \
  && opam config list && opam list"]

# opam config exec -- make
