FROM ubuntu:latest

RUN apt update && \
    apt install -y curl zip unzip software-properties-common

RUN add-apt-repository ppa:deadsnakes/ppa && \
    apt update

RUN apt install -y python3.10 python3.10-venv python3.10-dev

RUN curl -s "https://get.sdkman.io" | bash

SHELL ["/bin/bash", "-c"]  

RUN apt update && \
    apt install -y openjdk-8-jdk openjdk-8-jre

RUN source "/root/.sdkman/bin/sdkman-init.sh" && \
    sdk install kotlin && \
    sdk install gradle

ENV PATH=/root/.sdkman/candidates/scala/current/bin:$PATH
ENV PATH=/root/.sdkman/candidates/sbt/current/bin:$PATH
    
RUN rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY . .

RUN ./gradlew build

CMD [ "./gradlew", "run" ]