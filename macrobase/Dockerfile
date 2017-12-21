FROM ubuntu:16.04

RUN apt-get update \
  && apt-get install -y git curl sed vim openjdk-8-jdk python postgresql-client postgresql-client-common maven \
  && curl --silent --show-error --retry 5 https://bootstrap.pypa.io/get-pip.py | python \
  && pip install psycopg2

RUN ln -svT "/usr/lib/jvm/java-8-openjdk-$(dpkg --print-architecture)" /docker-java-home
ENV JAVA_HOME /docker-java-home

RUN cd /opt/ \
  && git clone https://github.com/stanford-futuredata/macrobase.git \
  && cd macrobase \
  && git checkout tags/v0.2 \
  && mvn package -DskipTests

COPY macrobase.yaml /opt/macrobase/conf/

WORKDIR /opt/macrobase

EXPOSE 8080

CMD ["bin/frontend.sh"]
