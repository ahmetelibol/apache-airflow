# Apache Airflow'un resmi Docker imajını temel al
FROM apache/airflow:2.10.5

# Apache Airflow ortam değişkenlerini belirleyelim
ARG AIRFLOW_VERSION=2.10.5
ARG PYTHON_VERSION=3.8
ARG CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"


# Root olarak gerekli bağımlılıkları yükle
USER root
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    build-essential libopenmpi-dev \
    gcc \
    g++ \
    libaio1 \
    libodbc2 \
    unixodbc \
    unixodbc-dev \
    freetds-dev \
    freetds-bin \
    libssl-dev \
    libsasl2-dev \
    libkrb5-dev \
    libgssapi-krb5-2 \
    krb5-user \
    libkrb5-dev \
    make \ 
    build-essential \
    cmake \ 
    git \
    libopenblas-dev \ 
    libomp-dev \
    curl \
    wget \
    nano \
    unzip \
    libffi-dev \
    samba-client \
    libsmbclient-dev \
    && apt-get autoremove -yqq --purge \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
# Root olarak krb5-config dosyasına yetki ver
RUN chmod +x /usr/bin/krb5-config

RUN apt-get update && apt-get install -y tzdata
ENV TZ=Europe/Istanbul

# Airflow kullanıcısına geç
USER airflow

# Oracle Instant Client
RUN mkdir /opt/airflow/oracle \
    && cd /opt/airflow/oracle

RUN curl -L -o /opt/airflow/oracle/instantclient-basic-linux.x64-23.5.0.24.07.zip https://download.oracle.com/otn_software/linux/instantclient/2350000/instantclient-basic-linux.x64-23.5.0.24.07.zip

RUN  unzip /opt/airflow/oracle/instantclient-basic-linux.x64-23.5.0.24.07.zip -d /opt/airflow/oracle \
    && rm -rf /opt/airflow/oracle/*.zip

ENV LD_LIBRARY_PATH=/opt/airflow/oracle/instantclient_23_5:${LD_LIBRARY_PATH}
ENV ORACLE_HOME=/opt/airflow/oracle

COPY requirements.txt /

# Pip komutunu güncelle ve gerekli bağımlılıkları yükle
RUN pip install --upgrade pip

RUN pip install "apache-airflow[celery]==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"

RUN pip install --no-cache-dir \
    "apache-airflow-providers-openlineage==1.12.1" \
    "apache-airflow-providers-microsoft-mssql==3.9.1" \
    "apache-airflow-providers-oracle==3.11.0"  \
    "apache-airflow-providers-github==2.7.0" \
    "apache-airflow-providers-opensearch==1.4.0" \
    "apache-airflow-providers-apprise==1.4.0" \
    "apache-airflow-providers-samba==4.8.0" \
    --constraint "${CONSTRAINT_URL}"

RUN pip install --no-cache-dir -r /requirements.txt
