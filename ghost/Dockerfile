FROM node:0.12
MAINTAINER Tiago Griffo "tiago@griffo.me"

# Download and install latest version of ghost
#RUN cd /tmp
#RUN wget https://ghost.org/zip/ghost-latest.zip

# Copy ghost to container
COPY packages/ghost-0.7.8.zip /tmp/ghost-latest.zip

RUN apt-get update
RUN apt-get install zip unzip 

# RUN cd /tmp
RUN unzip /tmp/ghost-latest.zip -d /ghost 
RUN rm -f /tmp/ghost-latest.zip 
RUN mkdir -p /var/www
RUN mv /ghost /var/www 
RUN npm install sqlite3 --build-from-source
RUN cd /var/www/ghost && npm install --production 

# # Move ghost into the system neighbourhood. Welcome yo!
ENV HOME /var/www/ghost
RUN useradd ghost --home /var/www/ghost
WORKDIR /var/www/ghost

ADD /theme $HOME/content/themes/casper

# Add config and script to start the engine
ADD config.js /var/www/ghost/config.js
ADD run-ghost.sh /run-ghost.sh
#ADD install_newrelic.sh /install_newrelic.sh
RUN chmod 0500 /run-ghost.sh

CMD /run-ghost.sh
