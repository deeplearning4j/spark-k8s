#
#   deeplearning4j docker image
#

FROM ubuntu:bionic as builder

LABEL Description="Deeplearning4j Spark snapshots container"  Vendor="SkyMind.ai"  Version="1.0.0-SNAPSHOT"

RUN apt-get update && \
    apt-get -y --no-install-recommends install \
            git openjdk-8-jdk maven gcc g++ automake cmake build-essential autoconf libtool pkg-config libgflags-dev libgtest-dev clang libc++-dev libgomp1 libprotobuf-dev && \
    apt-get clean


RUN git clone https://github.com/deeplearning4j/deeplearning4j.git && cd deeplearning4j && ./change-scala-versions.sh 2.11 && ./change-spark-versions.sh 2
RUN cd deeplearning4j/libnd4j && ./buildnativeoperations.sh -a native -j 6 && cd ../
RUN cd deeplearning4j/nd4j && mvn clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dmaven.test.skip=true
RUN cd deeplearning4j/datavec && mvn clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dmaven.test.skip=true
RUN cd deeplearning4j/deeplearning4j && mvn clean install -DskipTests=true -Dmaven.javadoc.skip=true -Dmaven.test.skip=true
