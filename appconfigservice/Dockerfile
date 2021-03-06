FROM python:3-alpine3.11

LABEL maintainer="wzhu26@illinois.edu"

WORKDIR /app

COPY appconfigservice ./appconfigservice
COPY lib ../lib/
COPY appconfigservice/appconfig.yaml .

ENV APP_CONFIG_MONGO_URL=""
ENV APP_CONFIG_URL_PREFIX=""

RUN apk --update add python py-pip openssl ca-certificates py-openssl && \
  apk --update add --virtual build-dependencies libffi-dev openssl-dev python-dev py-pip build-base && \
  pip install --upgrade pip && \
  pip install -r appconfigservice/requirements.txt --no-cache-dir && \
  apk del build-dependencies
  
WORKDIR /app/appconfigservice/api

VOLUME /var/cache/app

CMD ["gunicorn", "appconfig_rest_service:app", "--config", "../gunicorn.config.py"]