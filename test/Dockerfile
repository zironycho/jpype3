FROM jpype

RUN set -ex \
  && apk add --no-cache --virtual .fetch-deps \
    libressl \
    tar \
    xz \
  \
  && wget -O jpype.tar.gz "https://github.com/originell/jpype/archive/master.tar.gz" \
  && mkdir /jpype \
  && tar -xvf jpype.tar.gz -C /jpype --strip-components=1 \
  && cd /jpype \
  && apk del .fetch-deps

RUN apk add --no-cache --virtual .prep-deps apache-ant \
  && cd /jpype \
  && ant -f test/build.xml

RUN cd /jpype \
  && pip install -r test-requirements.txt \
  && python -c "import jpype" \
  && python test/testsuite.py

