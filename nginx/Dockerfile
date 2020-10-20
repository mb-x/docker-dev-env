FROM nginx:latest
ARG SYMFONY_VERSION

ENV SYMFONY_VERSION "$SYMFONY_VERSION"

COPY default-${SYMFONY_VERSION}.conf /etc/nginx/conf.d/
RUN rm /etc/nginx/conf.d/default.conf
RUN mv /etc/nginx/conf.d/default-${SYMFONY_VERSION}.conf /etc/nginx/conf.d/default.conf