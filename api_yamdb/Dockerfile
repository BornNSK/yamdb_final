FROM python:3.7-slim

WORKDIR /app

COPY requirements.txt .

RUN apt-get update \
    && apt-get -y install libpq-dev gcc \
    && pip3 install psycopg2 \
    && pip3 install -r requirements.txt --no-cache-dir

COPY api_yamdb/ .

CMD ["gunicorn", "api_yamdb.wsgi:application", "--bind", "0:8000" ]
