FROM docker.io/fatherlinux/centos4-base
MAINTAINER tangfeixiong <fxtang@qingyuanos.com>

ENV JAVA_VERSION jre-1_5_0_22
ENV JAVA_HOME /usr/java/jre1.5.0_22

ENV PATH=${PATH}:/usr/java/jre1.5.0_22/bin

ADD * /tmp/pkg2bld/

WORKDIR /tmp

# Notice: wget should not work, download through browser first
RUN \
  [[ -f ${JAVA_VERSION}-linux-amd64-rpm.bin ]] || \
  { wget --no-check-certificate --no-cookies --header \
	  "Cookie: oraclelicense=accept-securebackup-cookie; \
	  s_nr=1466987862671; s_cc=true; s_sq=oraclecom%3D%2526pid%253DSearch%25253A%252520All%25253A%252520Results%2526pidt%253D1%2526oid%253Dhttp%25253A%252F%252Fwww.oracle.com%252Ftechnetwork%252Fcn%252Ftopics%252Fentarch%252Fspring-2-weblogic-server-9-integrat-088905-zhs.h%2526ot%253DA; \
	  gpw_e24=no%20value" \
	  http://download.oracle.com/otn/java/jdk/1.5.0_22/${JAVA_VERSION}-linux-amd64-rpm.bin \
	  --continue -O docker/${JAVA_VERSION}-linux-amd64-rpm.bin; \
  }; \
  chmod +x pkg2bld/${JAVA_VERSION}-linux-amd64-rpm.bin && \
  yes | pkg2bld/${JAVA_VERSION}-linux-amd64-rpm.bin && \
  rm -rf pkg2bld/
 
#RUN curl --fail --silent --location --retry 3 \
#    --header "Cookie: oraclelicense=accept-securebackup-cookie; " \
#    http://download.oracle.com/otn/java/jdk/1.5.0_22/jdk-1_5_0_22-linux-amd64-rpm.bin
