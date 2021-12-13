FROM python:3.8-slim-buster

ENV PYTHONUNBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

RUN apt-get update \
  # dependencies for building Python packages
  && apt-get install -y apt-utils \
  && apt-get install -y build-essential \
  && python -m pip install --upgrade pip \
  # psycopg2 dependencies
  && apt-get install -y libpq-dev postgresql-client \
  # Translations dependencies
  && apt-get install -y gettext \
  # Django extensions
  && apt-get install -y graphviz libgraphviz-dev \
  # Weasyprint dependencies
  && apt-get install -y libcairo2 libpango-1.0-0 libpangocairo-1.0-0 libgdk-pixbuf2.0-0 libffi-dev shared-mime-info \
  # pdf2image dependencies
  && apt-get install -y poppler-utils \
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
