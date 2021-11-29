FROM node:5

EXPOSE 3000

WORKDIR /tripfez-ean

RUN npm install -g gulp bower

RUN apt-get update && apt-get install -y rubygems ruby-dev

RUN gem install sass compass

RUN rm -rf /var/lib/apt/lists/*

CMD [ "npm", "start" ]
