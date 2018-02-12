FROM python:3.6-alpine3.7

ADD requirements.txt /requirements.txt 

RUN apk add --no-cache --virtual .build-deps  gcc make libc-dev musl-dev linux-headers pcre-dev postgresql-dev git 

RUN apk add --no-cache --virtual .build-deps build-base python-dev py-pip jpeg-dev zlib-dev

ENV LIBRARY_PATH=/lib:/usr/lib

RUN pip install --upgrade -r requirements.txt

WORKDIR /code/
