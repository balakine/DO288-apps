FROM registry.access.redhat.com/ubi8:8.0

LABEL io.k8s.description="A basic nginx Server child image" \
      io.k8s.display-name="nginx HTTP Server" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="nginx"

ENV BACKEND_HOST=localhost:8081

RUN yum install -y --disableplugin=subscription-manager --nodocs \
  nginx nginx-mod-http-perl \
  && yum clean all

COPY nginx.conf /etc/nginx/

RUN touch /run/nginx.pid \
  && chgrp -R 0 /var/log/nginx /run/nginx.pid \
  && chmod -R g+rwx /var/log/nginx /run/nginx.pid
  
COPY src/ /usr/share/nginx/html

EXPOSE 8080

USER 1001

CMD nginx -g "daemon off;"

