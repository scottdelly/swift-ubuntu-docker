FROM omniprojects/ubuntu:16.04
MAINTAINER Omni Development Team <dev+docker@beomni.com>

USER root

# Set environment variables for image
ENV SWIFT_SNAPSHOT swift-3.1-RELEASE
ENV SWIFT_SNAPSHOT_LOWERCASE swift-3.1-release
ENV UBUNTU_VERSION ubuntu16.04
ENV UBUNTU_VERSION_NO_DOTS ubuntu1604
ENV HOME /root
ENV WORK_DIR /root
#ENV LD_LIBRARY_PATH /root/swift-lib:$LD_LIBRARY_PATH

# Set WORKDIR
WORKDIR ${WORK_DIR}

# Linux OS utils & Swift libraries
RUN apt-get update && apt-get dist-upgrade -y && apt-get install -y \
  libicu-dev \
  libgd-dev \
  libcurl4-openssl-dev \
  wget \
  && apt-get clean

RUN wget -q https://swift.org/builds/$SWIFT_SNAPSHOT_LOWERCASE/$UBUNTU_VERSION_NO_DOTS/$SWIFT_SNAPSHOT/$SWIFT_SNAPSHOT-$UBUNTU_VERSION.tar.gz \
     https://swift.org/builds/$SWIFT_SNAPSHOT_LOWERCASE/$UBUNTU_VERSION_NO_DOTS/$SWIFT_SNAPSHOT/$SWIFT_SNAPSHOT-$UBUNTU_VERSION.tar.gz.sig \
  && gpg --keyserver hkp://pool.sks-keyservers.net \
      --recv-keys \
      '7463 A81A 4B2E EA1B 551F  FBCF D441 C977 412B 37AD' \
      '1BE1 E29A 084C B305 F397  D62A 9F59 7F4D 21A5 6D5F' \
      'A3BA FD35 56A5 9079 C068  94BD 63BC 1CFE 91D3 06C6' \
  && gpg --keyserver hkp://pool.sks-keyservers.net --refresh-keys  \
  && gpg --verify $SWIFT_SNAPSHOT-$UBUNTU_VERSION.tar.gz.sig \
  && tar xzvf $SWIFT_SNAPSHOT-$UBUNTU_VERSION.tar.gz $SWIFT_SNAPSHOT-$UBUNTU_VERSION/usr/lib/swift/linux \
  && rm $SWIFT_SNAPSHOT-$UBUNTU_VERSION.tar.gz \
  && rm $SWIFT_SNAPSHOT-$UBUNTU_VERSION.tar.gz.sig \
  && find $SWIFT_SNAPSHOT-$UBUNTU_VERSION/usr/lib/swift/linux -type f ! -name '*.so' -delete \
  && rm -rf $SWIFT_SNAPSHOT-$UBUNTU_VERSION/usr/lib/swift/linux/*/ \

RUN apt-get remove gcc cpp sgml-base icu-devtools gcc-4.8 cpp-4.8 libc6-dev binutils manpages-dev manpages wget pkg-config perl \
  && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

CMD /bin/bash
