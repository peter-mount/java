################################################################################
# Based on jeanblanchard/java by Jean Blanchard <jean@blanchard.io>
#
# This generates a custom image with the following additions:
# 1: The letsencrypt CA is added to the certificates. Required if you want to
#    use https to a server using that CA. This will be removed once Oracle add
#    it to the jdk.
#
################################################################################
FROM area51/alpine
MAINTAINER Peter Mount <peter@retep.org>

ENV JAVA_VERSION_MAJOR 8
ENV JAVA_VERSION_MINOR 172
ENV JAVA_VERSION_BUILD 11
ENV JAVA_PACKAGE       server-jre
ENV URL_ELEMENT        a58eab1ec242421181065cdc37240b08

ENV PATH $PATH:/opt/jdk/bin

# Download and add the pem to the trust store
RUN mkdir -p /opt &&\
    curl -jkLH "Cookie: oraclelicense=accept-securebackup-cookie" \
	-o java.tar.gz \
	http://download.oracle.com/otn-pub/java/jdk/${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-b${JAVA_VERSION_BUILD}/${URL_ELEMENT}/${JAVA_PACKAGE}-${JAVA_VERSION_MAJOR}u${JAVA_VERSION_MINOR}-linux-x64.tar.gz &&\
    gunzip -c java.tar.gz | tar -xf - -C /opt && rm -f java.tar.gz &&\
    ln -s /opt/jdk1.${JAVA_VERSION_MAJOR}.0_${JAVA_VERSION_MINOR} /opt/jdk &&\
    rm -rf /opt/jdk/*src.zip \
         /opt/jdk/lib/missioncontrol \
         /opt/jdk/lib/visualvm \
         /opt/jdk/lib/*javafx* \
         /opt/jdk/jre/lib/plugin.jar \
         /opt/jdk/jre/lib/ext/jfxrt.jar \
         /opt/jdk/jre/bin/javaws \
         /opt/jdk/jre/lib/javaws.jar \
         /opt/jdk/jre/lib/desktop \
         /opt/jdk/jre/plugin \
         /opt/jdk/jre/lib/deploy* \
         /opt/jdk/jre/lib/*javafx* \
         /opt/jdk/jre/lib/*jfx* \
         /opt/jdk/jre/lib/amd64/libdecora_sse.so \
         /opt/jdk/jre/lib/amd64/libprism_*.so \
         /opt/jdk/jre/lib/amd64/libfxplugins.so \
         /opt/jdk/jre/lib/amd64/libglass.so \
         /opt/jdk/jre/lib/amd64/libgstreamer-lite.so \
         /opt/jdk/jre/lib/amd64/libjavafx*.so \
         /opt/jdk/jre/lib/amd64/libjfx*.so &&\
    sed -e "s|export PATH=|export PATH=/opt/jdk/bin:|" -i /etc/profile

