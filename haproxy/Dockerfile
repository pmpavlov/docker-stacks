FROM haproxy

# Create a system group and user to be used by HAProxy.
ENV HAPROXY_USER haproxy
RUN groupadd --system ${HAPROXY_USER} && \
    useradd --system --gid ${HAPROXY_USER} ${HAPROXY_USER} && \
    mkdir --parents /var/lib/${HAPROXY_USER} && \
    mkdir --parents /run/${HAPROXY_USER} && \
    chown -R ${HAPROXY_USER}:${HAPROXY_USER} /var/lib/${HAPROXY_USER}

#Adding Certificate
COPY server.bundle.pem /etc/ssl/certs/server.bundle.pem

# Now copy the configurations file
COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg

