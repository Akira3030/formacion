---
layout: default
title: "Postgresql"
---

# Trabajando con PostgreSQL :snake:

![]({{ site.site_url }}/assets/img/measurement-4028994_1920_alt_600.jpg)

## 1. Instalar PostgreSQL en local

sudo apt-get install postgresql postgresql-contrib
sudo -u postgres createuser --superuser juan
sudo -u name_of_user createdb books_store

sudo pip install psycopg2
pip install pygresql


## 2. Variables de entorno

export DATABASE_URL="postgresql://localhost/books_store"
echo $DATABASE_URL

## 3. psql

sudo -u postgres psql
postgres=# create database books_store;
postgres=# create user juan with encrypted password 'mypass';
postgres=# grant all privileges on database books_store to juan;

postgres=# alter user <username> with encrypted password '<password>';
postgres=# grant all privileges on database <dbname> to <username>;

## 4. Queys

CREATE DATABASE yourdbname;
CREATE USER youruser WITH ENCRYPTED PASSWORD 'yourpass';
GRANT ALL PRIVILEGES ON DATABASE yourdbname TO youruser;









