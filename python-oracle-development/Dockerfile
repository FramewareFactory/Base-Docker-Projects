FROM python:3.8-slim-buster

ENV PYTHONUNBUFFERED 1

ADD ./../libs/instantclient-basic-linux.x64-21.4.zip instantclient-basic-linux.x64.zip

RUN apt-get update \
  # dependencies for building Python packages
  && apt-get install -y apt-utils \
  && apt-get install -y build-essential \
  && python -m pip install --upgrade pip \
  # psycopg2 dependencies
  && apt-get install -y libpq-dev postgresql-client \
  # Instalar “libaio” (The Linux-native asynchronous I/O facility):
  && apt-get install -y unzip libaio1 \
    && unzip instantclient-basic-linux.x64.zip -d /opt/oracle \
    && sh -c "echo /opt/oracle/instantclient_21_4 > /etc/ld.so.conf.d/oracle-instantclient.conf" ldconfig \
  # Translations dependencies
  && apt-get install -y gettext \
  # Django extensions
  && apt-get install -y graphviz libgraphviz-dev \
  # Weasyprint dependencies
  && apt-get install -y libcairo2 libpango-1.0-0 libpangocairo-1.0-0 libgdk-pixbuf2.0-0 libffi-dev shared-mime-info \
  # Locales
  && apt-get install -y locales locales-all \
  # cleaning up unused files
  && apt-get purge -y --auto-remove -o APT::AutoRemove::RecommendsImportant=false \
  && rm -rf /var/lib/apt/lists/*

# Set the locale
RUN sed -i '/es_MX.UTF-8/s/^# //g' /etc/locale.gen && locale-gen
ENV LANG es_MX.UTF-8
ENV LANGUAGE es_MX:en
ENV LC_ALL es_MX.UTF-8

ENTRYPOINT ["/entrypoint"]
