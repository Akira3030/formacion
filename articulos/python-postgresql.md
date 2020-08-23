---
layout: default
title: "Postgresql"
---

# Trabajando con PostgreSQL :snake:

![]({{ site.site_url }}/assets/img/measurement-4028994_1920_alt_600.jpg)

## 1. Instalar PostgreSQL en local

```bash
sudo apt-get install postgresql postgresql-contrib
sudo -u postgres createuser --superuser juan
sudo -u name_of_user createdb books_store

sudo pip install psycopg2
pip install pygresql
```


## 2. Variables de entorno

```bash
export DATABASE_URL="postgresql://localhost/books_store"
echo $DATABASE_URL
```

## 3. psql

```bash
sudo -u postgres psql
postgres=# create database books_store;
postgres=# create user juan with encrypted password 'mypass';
postgres=# grant all privileges on database books_store to juan;

postgres=# alter user <username> with encrypted password '<password>';
postgres=# grant all privileges on database <dbname> to <username>;
```

## 4. Queys

```bash
CREATE DATABASE yourdbname;
CREATE USER youruser WITH ENCRYPTED PASSWORD 'yourpass';
GRANT ALL PRIVILEGES ON DATABASE yourdbname TO youruser;
```

## 5. Conexión a PostgreSQL desde Python

```python
conexion = psycopg2.connect("dbname=empleados user=neoguias password=pimientos44")
conexion = psycopg2.connect(host="localhost", database="empleados", user="neoguias", password="pimientos44")
Por defecto el puerto es 5432
```

```python
cur = conexion.cursor()
cur.execute( "SELECT nombre, apellidos FROM empleados" )

for nombre, apellidos in cur.fetchall() :
    print nombre, apellidos

conexion.close()
```

## 6. Archivo de configuración de la BD

 Almacenar la configuración de acceso a la base de datos en un archivo .ini

```txt
[postgresql]
host=localhost
database=empleados
user=neoguias
password=pimientos44
port=5432
```

## 7. Querys

### Creación de tablas

```bash
CREATE TABLE datacamp_courses(
 course_id SERIAL PRIMARY KEY,
 course_name VARCHAR (50) UNIQUE NOT NULL,
 course_instructor VARCHAR (100) NOT NULL,
 topic VARCHAR (20) NOT NULL
);
```

```bash
CREATE TABLE table_name (
 column_name TYPE column_constraint,
 table_constraint table_constraint
)
```


### Insertar datos en las tablas

INSERT INTO datacamp_courses(course_name, course_instructor, topic)
VALUES('Deep Learning in Python','Dan Becker','Python');
INSERT INTO datacamp_courses(course_name, course_instructor, topic)
VALUES('Joining Data in PostgreSQL','Chester Ismay','SQL');

### Aptualizar un registro en una tabla

UPDATE datacamp_courses SET course_name = 'Joining Data in SQL'
WHERE course_instructor = 'Chester Ismay';

### Leer datos de una tabla

select * from datacamp_courses;

### Borrar datos de una tabla

delete from datacamp_courses where course_name = 'Deep Learning in Python';

### Crear una tabla desde python

```python
import psycopg2

#Establishing the connection
conn = psycopg2.connect(
   database="mydb", user='postgres', password='password', host='127.0.0.1', port= '5432'
)
#Creating a cursor object using the cursor() method
cursor = conn.cursor()

#Doping EMPLOYEE table if already exists.
cursor.execute("DROP TABLE IF EXISTS EMPLOYEE")

#Creating table as per requirement
sql ='''CREATE TABLE EMPLOYEE(
   FIRST_NAME CHAR(20) NOT NULL,
   LAST_NAME CHAR(20),
   AGE INT,
   SEX CHAR(1),
   INCOME FLOAT
)'''
cursor.execute(sql)
print("Table created successfully........")

#Closing the connection
conn.close()
```














