# Copyright 2019 Amazon.com, Inc. or its affiliates. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License").
# You may not use this file except in compliance with the License.
# A copy of the License is located at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# or in the "license" file accompanying this file. This file is distributed
# on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either
# express or implied. See the License for the specific language governing
# permissions and limitations under the License.

# Description:
# Dockerfile for building the docker image for open distro for elasticsearch
#
# This file was generated from the template at templates/Dockerfile.j2

################################################################################
# This Dockerfile was generated from the template at templates/Dockerfile.j2
#
# Beginning of multi stage Dockerfile
################################################################################


################################################################################
# Build stage 0 `prep_es_files`:
# Extract elasticsearch artifact
# Install required plugins
# Set gid=0 and make group perms==owner perms
################################################################################

FROM centos:7 AS prep_es_files

RUN date && echo OD_VERSION 1.11.0 ES_VERSION 7.9.1

ENV PATH /usr/share/elasticsearch/bin:$PATH
## Old methods, save here for possible revert
#RUN curl -s  https://download.java.net/java/GA/jdk12.0.2/e482c34c86bd4bf8b56c0b35558996b9/10/GPL/openjdk-12.0.2_linux-x64_bin.tar.gz | tar -C /opt -zxf -
#ENV JAVA_HOME /opt/jdk-12.0.2
# hadolint ignore=DL3033
RUN yum -y update \
    && yum -y groupinstall "Development Tools" \
    && yum install -y unzip glibc.x86_64 cmake \
    && yum clean all

RUN groupadd -g 1000 elasticsearch && \
    adduser -u 1000 -g 1000 -d /usr/share/elasticsearch elasticsearch

USER 1000


RUN rm -rf /tmp/plugins && mkdir /tmp/plugins
COPY plugins /tmp/plugins/

################################################################################

# Set WORKDIR here
WORKDIR /usr/share/elasticsearch

# Download and extract defined ES version.
# hadolint ignore=DL4006
RUN curl -fsSL https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-oss-7.9.1-linux-x86_64.tar.gz | \
    tar zx --strip-components=1

RUN set -ex && for esdirs in config data logs; do \
        mkdir -p "$esdirs"; \
    done

## Related to jdk version in docker, use the bundled one instead of jdk 12 here
USER 0
RUN cp -rp /usr/share/elasticsearch/jdk /opt/jdk
ENV JAVA_HOME /opt/jdk
ENV PATH $PATH:$JAVA_HOME/bin
RUN java -version

# Compile the C-library for kNN
USER 1000
# hadolint ignore=DL4006,SC2086
RUN set -ex; \

   export KNN_VERSION=`git ls-remote --tags "https://github.com/opendistro-for-elasticsearch/k-NN" v* | grep $(echo 1.11.0 | sed -E "s/.[0-9]+$//g") | grep -oh "v[0-9.]*" | sort | tail -n 1` \
 \
    && git ls-remote --tags https://github.com/opendistro-for-elasticsearch/k-NN.git v* \
 \
    && echo KNN_VERSION $KNN_VERSION \
 \
    && git clone --recursive --branch $KNN_VERSION https://github.com/opendistro-for-elasticsearch/k-NN.git /usr/share/elasticsearch/k-NN
WORKDIR /usr/share/elasticsearch/k-NN/jni

RUN sed -i 's/-march=native/-march=x86-64/g' external/nmslib/similarity_search/CMakeLists.txt \
\
    && cmake . \
 \
    && make \
 \
    && mkdir /tmp/jni/ && cp release/*.so /tmp/jni/ && ls -ltr /tmp/jni/ \
 \
    && rm -rf /usr/share/elasticsearch/k-NN

WORKDIR /usr/share/elasticsearch

# Bust cache for wgets
ENV BUST_CACHE 1608623340

# Install the required modules
#RUN for plugin_path in opendistro_sql-1.11.0.0.zip opendistro_alerting-1.11.0.0.zip opendistro-job-scheduler-1.11.0.0.zip opendistro_security-1.11.0.0.zip opendistro_performance_analyzer-1.11.0.0.zip opendistro_index_management-1.11.0.0.zip opendistro-knn-1.11.0.0.zip opendistro-anomaly-detection-1.11.0.0.zip; do \
# hadolint ignore=SC2086
RUN for plugin_path in `cat /tmp/plugins/plugins.list`; do \
      elasticsearch-plugin install --batch file:/tmp/plugins/$plugin_path; \
    done

# Pull performance analyzer agent(RCA) from the plugin directory out into ESHOME and make the agent executable.
RUN if [ -d plugins/opendistro_performance_analyzer/performance-analyzer-rca ]; then \
     mv plugins/opendistro_performance_analyzer/performance-analyzer-rca ./ && \
     chmod 755 performance-analyzer-rca/pa_bin/performance-analyzer-agent; fi
# Make the certificate installer script executable. This script has to be executed before ES is started.
# hadolint ignore=DL4006,SC2086
RUN security=`ls /tmp/plugins/|grep opendistro_security|wc -l` && \
    if [ $security -gt 0 ]; then chmod +x /usr/share/elasticsearch/plugins/opendistro_security/tools/install_demo_configuration.sh; \
    else echo "Security plugin is not yet installed"; fi

COPY --chown=1000:0 elasticsearch.yml log4j2.properties config/

# hadolint ignore=DL3002
USER 0

# Set gid to 0 for opendistroforelasticsearch and make group permission similar to that of user
RUN chown -R elasticsearch:0 . && \
    chmod -R g=u /usr/share/elasticsearch

# hadolint ignore=DL4006,SC2086
RUN pfa=`ls /tmp/plugins/|grep opendistro_performance_analyzer|wc -l` && \ 
    if [ $pfa -gt 0 ]; then chmod 755 /usr/share/elasticsearch/plugins/opendistro_performance_analyzer/pa_bin/performance-analyzer-agent; \
    else echo "Performace Analyzer plugin is not yet installed"; fi

RUN chmod -R 755 /dev/shm
################################################################################
# Build stage 1 (the actual opendistroforelasticsearch image):
# Copy opendistroforelasticsearch from stage 0
# Add entrypoint
################################################################################

FROM centos:7

ENV ELASTIC_CONTAINER true

# hadolint ignore=DL4006,DL3033
RUN rpm --rebuilddb && yum clean all && \
    yum install -y epel-release && \
    yum update -y && \
    yum install -y iproute && \
    yum install -y hostname && \
    yum install -y inotify-tools && \
    yum install -y yum-utils && \
    yum install -y which && \
    yum install -y jq && \
    yum install -y rsync && \
    yum search pip | grep python3 && \
    yum install -y python34-pip && \
    /usr/bin/pip3.4 install supervisor && \
    yum clean all

# hadolint ignore=DL3033
RUN yum update -y && \
    yum install -y nc unzip wget which && \
    yum clean all
COPY CENTOS_LICENSING.txt /root
##COPY --from=prep_es_files --chown=1000:0 /opt/jdk-12.0.2 /opt/jdk-12.0.2

COPY --from=prep_es_files --chown=1000:0 /opt/jdk /opt/jdk
ENV JAVA_HOME /opt/jdk
ENV PATH $PATH:$JAVA_HOME/bin
RUN java -version

# Replace OpenJDK's built-in CA certificate keystore with the one from the OS
# vendor. The latter is superior in several ways.
##RUN ln -sf /etc/pki/ca-trust/extracted/java/cacerts /opt/jdk-12.0.2/lib/security/cacerts
# hadolint ignore=DL3059
RUN ln -sf /etc/pki/ca-trust/extracted/java/cacerts $JAVA_HOME/lib/security/cacerts


RUN mkdir /usr/share/elasticsearch && \
    groupadd -g 1000 elasticsearch && \
    adduser -u 1000 -g 1000 -G 0 -d /usr/share/elasticsearch elasticsearch && \
    chmod 0775 /usr/share/elasticsearch && \
    chgrp 0 /usr/share/elasticsearch

RUN mkdir -p /usr/share/supervisor/performance_analyzer/ && \
    chown 1000 /usr/share/supervisor/performance_analyzer

WORKDIR /usr/share/elasticsearch
COPY --from=prep_es_files --chown=1000:0 /usr/share/elasticsearch /usr/share/elasticsearch
COPY --from=prep_es_files /tmp/jni/libKNNIndex*.so /usr/lib

ENV PATH /usr/share/elasticsearch/bin:$PATH

COPY --chown=1000:0 bin/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh

# Openshift overrides USER and uses ones with randomly uid>1024 and gid=0
# Allow ENTRYPOINT (and ES) to run even with a different user
RUN chgrp 0 /usr/local/bin/docker-entrypoint.sh && \
    chmod g=u /etc/passwd && \
    chmod 0775 /usr/local/bin/docker-entrypoint.sh

EXPOSE 9200 9300 9600 9650

LABEL org.label-schema.schema-version="1.0" \
  org.label-schema.name="opendistroforelasticsearch" \
  org.label-schema.version="1.11.0" \
  org.label-schema.url="https://opendistro.github.io" \
  org.label-schema.vcs-url="https://github.com/opendistro-for-elasticsearch/opendistro-build" \
  org.label-schema.license="Apache-2.0" \
  org.label-schema.vendor="Amazon" \
  org.label-schema.build-date="20.12.22"

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
# Dummy overridable parameter parsed by entrypoint
CMD ["eswrapper"]

################################################################################
# End of multi-stage Dockerfile
################################################################################
