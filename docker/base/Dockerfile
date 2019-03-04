FROM ubuntu:18.04
RUN echo "Europe/London"|tee /etc/timezone

ENV DAEMON_RUN=true
ENV SPARK_VERSION=2.4.0
ENV HADOOP_VERSION=2.7
ENV SCALA_VERSION=2.12.8
ENV SCALA_HOME=/usr/share/scala
ENV SPARK_HOME=/spark

RUN apt-get update && apt-get install -y gnupg gnupg1 gnupg2 apt-utils

RUN echo "deb https://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823

RUN apt-get update; apt-get install -y wget ca-certificates sbt openjdk-8-jdk && \
    cd "/tmp" && \
    wget "https://downloads.lightbend.com/scala/${SCALA_VERSION}/scala-${SCALA_VERSION}.tgz" && \
    tar xzf "scala-${SCALA_VERSION}.tgz" && \
    mkdir "${SCALA_HOME}" && \
    mv "/tmp/scala-${SCALA_VERSION}" "${SCALA_HOME}" && \
    ln -s "${SCALA_HOME}/bin/"* "/usr/bin/" && \
    rm -rf "/tmp/"*
    
#Scala installation
RUN export PATH="/usr/local/sbt/bin:$PATH" &&  mkdir -p "/usr/local/sbt" && wget -qO - --no-check-certificate "https://piccolo.link/sbt-1.2.8.tgz" | tar xz -C /usr/local/sbt --strip-components=1 && sbt sbtVersion

#Spark installation
RUN wget http://apache.mirror.iphh.net/spark/spark-${SPARK_VERSION}/spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz && tar -xvzf spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz \
      && mv spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION} ${SPARK_HOME} \
      && rm spark-${SPARK_VERSION}-bin-hadoop${HADOOP_VERSION}.tgz