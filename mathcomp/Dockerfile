FROM erikmd/coq:8.8.1
LABEL maintainer="erik@martin-dorel.org"

ENV MATHCOMP_VERSION="1.7.0"

RUN ["/bin/bash", "--login", "-x", "-c", \
  "opam repository add coq-released https://coq.inria.fr/opam/released \
  && opam update \
  && opam pin add -n -k version coq-mathcomp-character ${MATHCOMP_VERSION} \
  && opam install -j ${NJOBS} coq-mathcomp-character \
  && opam config list && opam list"]

# opam config exec -- make
