FROM registry.access.redhat.com/ubi8/ubi:8.1
COPY requirements /tmp/
RUN yum update -y && \
    yum install python39 -y && \
    yum install rsyslog -y && \
    pip3 install -r /tmp/flask_requirements
COPY flask/app /app
copy flask/gunicorn.sh /gunicorn.sh
RUN chmod +x /gunicorn.sh
RUN echo 'module(load="imtcp")' >> /etc/rsyslog.conf
RUN echo 'imput(type="imtcp" port="514")' >> /etc/rsyslog.conf

EXPOSE 8080/tcp
ENTRYPOINT [ "/gunicorn.sh" ]
