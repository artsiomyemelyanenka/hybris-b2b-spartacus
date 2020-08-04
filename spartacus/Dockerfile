FROM ubuntu:18.04

RUN apt-get update && apt-get -y install curl jq
RUN curl -sL https://deb.nodesource.com/setup_12.x | bash -
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add -
RUN echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list
RUN apt-get update && apt-get -y install dirmngr apt-transport-https lsb-release nodejs yarn curl
RUN npm install -g @angular/cli

RUN useradd --create-home spartacus
USER spartacus
WORKDIR /home/spartacus

RUN ng new mystore --routing false --style=scss
WORKDIR /home/spartacus/mystore
RUN ng add @spartacus/schematics
RUN yarn install
COPY app.module.ts ./src/app/app.module.ts
#COPY webApplicationInjector.js ./src
#COPY angular.json .

RUN yarn build

EXPOSE 4200
CMD sed -i -E "s|baseUrl: 'https://localhost:9002',|baseUrl: '$OCC_URL',|" ./src/app/app.module.ts && ng serve --host 0.0.0.0 --port 4200