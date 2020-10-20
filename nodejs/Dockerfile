FROM node:10

RUN apt-get update && \
	apt-get install -y \
		curl \
		apt-transport-https

RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | APT_KEY_DONT_WARN_ON_DANGEROUS_USAGE=DontWarn apt-key add - && \
    echo "deb http://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
    apt-get update && \
    apt-get install --no-install-recommends yarn


#RUN /usr/bin/npm install -g gulp
#RUN /usr/bin/npm install -g babel-core
#RUN /usr/bin/npm install -g babel-preset-env
#RUN /usr/bin/npm install -g babel-register
#RUN /usr/bin/npm install -g babel-loader
#RUN /usr/bin/npm install -g gulp-babel

WORKDIR /var/www/symfony
