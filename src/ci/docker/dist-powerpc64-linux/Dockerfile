FROM ubuntu:16.04

RUN apt-get update && apt-get install -y --no-install-recommends \
  g++ \
  make \
  file \
  curl \
  ca-certificates \
  python2.7 \
  git \
  cmake \
  sudo \
  gdb \
  xz-utils \
  g++-powerpc64-linux-gnu \
  g++-powerpc64le-linux-gnu

ENV SCCACHE_DIGEST=7237e38e029342fa27b7ac25412cb9d52554008b12389727320bd533fd7f05b6a96d55485f305caf95e5c8f5f97c3313e10012ccad3e752aba2518f3522ba783
RUN curl -L https://api.pub.build.mozilla.org/tooltool/sha512/$SCCACHE_DIGEST | \
      tar xJf - -C /usr/local/bin --strip-components=1

RUN curl -OL https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64.deb && \
    dpkg -i dumb-init_*.deb && \
    rm dumb-init_*.deb
ENTRYPOINT ["/usr/bin/dumb-init", "--"]

ENV \
    AR_powerpc64_unknown_linux_gnu=powerpc64-linux-gnu-ar \
    CC_powerpc64_unknown_linux_gnu=powerpc64-linux-gnu-gcc \
    CXX_powerpc64_unknown_linux_gnu=powerpc64-linux-gnu-g++

ENV HOSTS=powerpc64-unknown-linux-gnu
ENV HOSTS=$HOSTS,powerpc64le-unknown-linux-gnu

ENV RUST_CONFIGURE_ARGS --host=$HOSTS
ENV SCRIPT python2.7 ../x.py dist --host $HOSTS --target $HOSTS
