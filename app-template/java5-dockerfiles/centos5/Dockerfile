FROM docker.io/fatherlinux/centos5-base
MAINTAINER tangfeixiong <fxtang@qingyuanos.com>

ENV JAVA_VERSION jre-1_5_0_22
ENV JAVA_HOME /usr/java/jre1.5.0_22

ENV PATH=${PATH}:/usr/java/jre1.5.0_22/bin

ADD * /tmp/

WORKDIR /tmp

# Notice: wget should not work, download through browser first
RUN \
  [[ -f ${JAVA_VERSION}-linux-amd64-rpm.bin ]] || \
  { wget --no-check-certificate --no-cookies --header \
	  "Cookie: oraclelicense=accept-securebackup-cookie" \
	  http://download.oracle.com/otn/java/jdk/1.5.0_22/${JAVA_VERSION}-linux-amd64-rpm.bin; \
  }; \
  chmod +x ${JAVA_VERSION}-linux-amd64-rpm.bin && \
  yes | ./${JAVA_VERSION}-linux-amd64-rpm.bin && \
  rm -rf ${JAVA_VERSION}-linux-amd64* *.bin Dockerfile
 
#RUN curl --fail --silent --location --retry 3 \
#    --header "Cookie: oraclelicense=accept-securebackup-cookie; " \
#    http://download.oracle.com/otn/java/jdk/1.5.0_22/${JAVA_VERSION}-linux-amd64-rpm.bin
  
