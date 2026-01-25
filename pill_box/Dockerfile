FROM python:3.12-slim

WORKDIR /opt/app
RUN groupadd -r django_user && useradd -d /opt/app -r -g django_user django_user \
    && chown django_user:django_user -R /opt/app

COPY infra/configs/uwsgi/uwsgi.ini uwsgi.ini

RUN apt-get update && \
    apt-get install -y libpcre3 libpcre3-dev && \
    apt-get install -y build-essential && \
    pip install --upgrade pip

COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt

COPY . .

USER django_user

EXPOSE 8080

ENTRYPOINT ["uwsgi", "--strict", "--ini", "uwsgi.ini"]
