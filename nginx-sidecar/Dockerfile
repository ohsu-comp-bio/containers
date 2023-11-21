ARG AZLINUX_VERSION=2023

FROM public.ecr.aws/amazonlinux/amazonlinux:${AZLINUX_VERSION}


# install any available security and bugfix updates
RUN dnf update \
        --assumeyes \
    && dnf update \
        --security \
        --bugfix \
        --assumeyes \
    && dnf clean all \
    && rm -rf /var/cache/yum

# install nginx
RUN yum update -y && \
    yum install -y nginx && \
    yum clean all && \
    rm -rf /var/cache/yum

# create nginx user/group for unprivileged execution. Give it uid/gid 1000 and guid 1000
# Give it access to all nginx folders
RUN groupadd --gid 1000 gen3 && \
    useradd --uid 1000 --gid gen3 --shell /bin/bash --create-home gen3 && \
    mkdir -p /var/cache/nginx && \
    mkdir -p /var/log/nginx && \
    mkdir -p /var/run/nginx && \
    chown -R gen3:gen3 /var/cache/nginx && \
    chown -R gen3:gen3 /var/log/nginx && \
    chown -R gen3:gen3 /var/run/nginx && \
    chown -R gen3:gen3 /var/cache/nginx/ && \
    chown -R gen3:gen3 /var/lib/nginx/ && \
    touch /run/nginx.pid && \
    chown -R gen3:gen3 /run/nginx.pid && \
    chown -R gen3:gen3 /etc/nginx/

# Send logs to sdtout and stderr
RUN ln -sf /dev/stdout /var/log/nginx/access.log && \
    ln -sf /dev/stderr /var/log/nginx/error.log

COPY nginx.conf /etc/nginx/nginx.conf

USER gen3

EXPOSE 80
STOPSIGNAL SIGTERM
CMD nginx -g 'daemon off;'
