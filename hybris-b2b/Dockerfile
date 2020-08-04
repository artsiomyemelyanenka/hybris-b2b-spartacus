FROM ubuntu:18.04
RUN apt-get update && apt-get install -y unzip
WORKDIR /tmp
RUN mkdir -p /tmp/hybris/
COPY CXCOM200500P_0-70004955.ZIP hybris.zip
RUN unzip -q /tmp/hybris.zip -d /tmp/hybris/

FROM ubuntu:18.04

RUN apt-get update && \
	apt-get install -y openjdk-11-jdk && \
	apt-get install -y ant && \
	apt-get install -y curl && \
	apt-get install -y unzip

RUN apt-get install -y ca-certificates-java && \
	apt-get clean && \
	update-ca-certificates -f && \
	rm -rf /var/lib/apt/lists/* && \
	rm -rf /var/cache/oracle-jdk11-installer;

ENV JAVA_HOME /usr/lib/jvm/java-11-openjdk-amd64/
RUN export JAVA_HOME

RUN useradd --create-home hybris
COPY --chown=hybris --from=0 /tmp/hybris /home/hybris/
USER hybris

WORKDIR /home/hybris/installer
RUN mkdir /home/hybris/installer/recipes/cx-for-spa
COPY build.gradle /home/hybris/installer/recipes/cx-for-spa
COPY custom.properties /home/hybris/installer/customconfig

RUN mkdir /home/hybris/hybris/bin/custom
WORKDIR /home/hybris/hybris/bin/custom/
RUN curl -LJO https://github.com/SAP/spartacus/releases/download/storefront-2.0.5/spartacussampledataaddon.2005.zip -o /home/hybris/hybris/bin/custom/spartacussampledataaddon.2005.zip
RUN unzip /home/hybris/hybris/bin/custom/spartacussampledataaddon.2005.zip -d /home/hybris/hybris/bin/custom/
RUN rm /home/hybris/hybris/bin/custom/spartacussampledataaddon.2005.zip

WORKDIR /home/hybris/installer
RUN ./install.sh -r cx-for-spa setup
RUN ./install.sh -r cx-for-spa initialize

EXPOSE 9001
EXPOSE 9002

CMD ["./install.sh",  "-r",  "cx-for-spa", "start"]
