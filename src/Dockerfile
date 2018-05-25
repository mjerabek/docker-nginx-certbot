FROM nginx:alpine
LABEL maintainer="Elliot Saba <staticfloat@gmail.com>, Valder Gallo <valergallo@gmail.com>, Bruno Zell <bruno.zzell@gmail.com>"

VOLUME /etc/letsencrypt
EXPOSE 80
EXPOSE 443

RUN   apk add --update certbot bash ncurses \
   && rm -rf /var/cache/apk/*

# Copy in scripts for certbot
COPY ./scripts/ /scripts
RUN chmod +x /scripts/*.sh

# Add /scripts/startup directory to source more startup scripts
RUN mkdir -p /scripts/startup

# Copy in default nginx configuration (which just forwards ACME requests to
# certbot, or redirects to HTTPS, but has no HTTPS configurations by default).
RUN rm -f /etc/nginx/conf.d/*
COPY nginx_conf.d/ /etc/nginx/conf.d/

ENTRYPOINT []
CMD ["/bin/bash", "/scripts/entrypoint.sh"]
