FROM ubuntu:20.04

ENV DEBIAN_DRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    python3 \
    python3-pip \
    python3-dev \ 
    build-essential \ 
    wget \
    mysql-server \
    postgresql postgresql-contrib \
    gnupg \
    && apt-get clean

# Configurar MongoDB
RUN mkdir -p /etc/apt/keyrings && \
    wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | gpg --dearmor | tee /etc/apt/keyrings/mongodb.gpg > /dev/null && \
    echo "deb [ arch=amd64,arm64 signed-by=/etc/apt/keyrings/mongodb.gpg ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-6.0.list

# Instalar MongoDB
RUN apt-get update && apt-get install -y mongodb-org && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip && \
    pip3 install notebook mysql-connector-python psycopg2-binary pymongo

WORKDIR /workspace

EXPOSE 8888 3306 5432 27017

CMD service mysql start && \
    service postgresql start && \
    mongo --fork --logpath /var/log/mongodb.log && \
    jupyter notebook --ip=0.0.0.0 --port=8888 --no-browser --allow_root
