FROM ubuntu:bionic
LABEL maintainer thaterwilcox <thater@gmail.com>
# OpenRefine 3.0 Beta Version

# Install JDK after system updates
RUN apt-get update && apt-get install -y wget ant unzip openjdk-8-jdk && apt-get clean

WORKDIR /app

# Build OpenRefine
RUN wget --no-check-certificate https://github.com/OpenRefine/OpenRefine/archive/3.0-beta.zip
RUN unzip 3.0-beta.zip  && rm 3.0-beta.zip
RUN OpenRefine-3.0-beta/refine build

# Remove JDK and install JRE
RUN apt-get remove -y openjdk-8-jdk
RUN apt-get install openjdk-8-jre-headless

# Now clean it all up
RUN apt-get autoremove -y && apt-get autoclean -y

VOLUME /data
WORKDIR /data

EXPOSE 3333

ENTRYPOINT ["/app/OpenRefine-3.0-beta/refine"]
CMD ["-i", "0.0.0.0", "-d", "/data"]