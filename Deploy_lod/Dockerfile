FROM madnight/docker-alpine-wkhtmltopdf

RUN apk update

RUN apk add --no-cache build-base
RUN apk --update add libxml2-dev libxslt-dev libffi-dev gcc musl-dev libgcc openssl-dev curl
RUN apk add curl jpeg-dev zlib-dev freetype-dev lcms2-dev openjpeg-dev tiff-dev tk-dev tcl-dev python2

RUN curl https://bootstrap.pypa.io/pip/2.7/get-pip.py -o get-pip.py && python get-pip.py
# RUN apk add --update py-pip
# RUN apk add wkhtmltopdf
# RUN pip install --upgrade pip

RUN apk add libxml2-dev libxml2 libxslt-dev python2-dev

COPY lod_prj/requirements.txt /usr/src/lod_prj/
RUN pip install --no-cache-dir -r /usr/src/lod_prj/requirements.txt

RUN pip install PyPDF2

ENV TZ=Europe/Kiev
RUN apk update
RUN apk upgrade
RUN apk add ca-certificates && update-ca-certificates
RUN apk add --update tzdata
# RUN rm -rf /var/cache/apk/*
RUN apk --update add fontconfig
RUN apk add ttf-liberation

# `lod` expects wkhtmltopdf be in a specific place
RUN  mkdir -p /srv/apps/venvs/lod/bin/ \
    && ln -s $(which wkhtmltopdf)  /srv/apps/venvs/lod/bin/wkhtmltopdf


ADD lod_prj /usr/src/lod_prj

WORKDIR /usr/src/lod_prj/

ENV C_FORCE_ROOT=1

# to reset entrypoint from parent container
ENTRYPOINT []

CMD ["python", "/usr/src/lod_prj/server.py"]
#RUN ["chmod", "+x", "/usr/src/lod_prj/celery.sh"]
#CMD ./usr/src/lod_prj/celery.sh
