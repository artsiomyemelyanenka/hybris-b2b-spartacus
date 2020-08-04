FROM ubuntu
RUN apt-get update && apt-get install -y iputils-ping && apt-get install -y curl 
RUN apt-get install -y dnsutils
RUN apt-get install -y mongodb-clients
CMD ping localhost -c 1 & sleep infinity