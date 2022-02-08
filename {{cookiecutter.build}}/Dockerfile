FROM python:3.9-alpine

ADD requirements.txt /requirements.txt

ENV LIBRARY_PATH=/lib:/usr/lib

RUN apk add --no-cache --virtual .build-deps  gcc make libc-dev musl-dev linux-headers pcre-dev postgresql-dev git libxml2 \
        libxml2-dev libxslt libxslt-dev\
    build-base python-dev py-pip jpeg-dev zlib-dev \
    && pip install --upgrade pip \
    && pip  install --upgrade -r requirements.txt \
    && find /usr/local \
        \( -type d -a -name test -o -name tests \) \
        -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
        -exec rm -rf '{}' + \
    && runDeps="$( \
        scanelf --needed --nobanner --recursive /usr/local \
                | awk '{ gsub(/,/, "\nso:", $2); print "so:" $2 }' \
                | sort -u \
                | xargs -r apk info --installed \
                | sort -u \
    )" \
    && apk add --virtual .rundeps $runDeps 

WORKDIR /code/
