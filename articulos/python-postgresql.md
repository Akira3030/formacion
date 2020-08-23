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

 Almacenar la configuración de acceso a la base de datos en un archivo .ini (database.ini)

```txt
[postgresql]
host=localhost
database=empleados
user=neoguias
password=pimientos44
port=5432
```

```python
#!/usr/bin/python
from configparser import ConfigParser


def config(filename='database.ini', section='postgresql'):
    # create a parser
    parser = ConfigParser()
    # read config file
    parser.read(filename)

    # get section, default to postgresql
    db = {}
    if parser.has_section(section):
        params = parser.items(section)
        for param in params:
            db[param[0]] = param[1]
    else:
        raise Exception('Section {0} not found in the {1} file'.format(section, filename))

    return db
```

```python
#!/usr/bin/python
import psycopg2
from config import config

def connect():
    """ Connect to the PostgreSQL database server """
    conn = None
    try:
        # read connection parameters
        params = config()

        # connect to the PostgreSQL server
        print('Connecting to the PostgreSQL database...')
        conn = psycopg2.connect(**params)
		
        # create a cursor
        cur = conn.cursor()
        
	# execute a statement
        print('PostgreSQL database version:')
        cur.execute('SELECT version()')

        # display the PostgreSQL database server version
        db_version = cur.fetchone()
        print(db_version)
       
	# close the communication with the PostgreSQL
        cur.close()
    except (Exception, psycopg2.DatabaseError) as error:
        print(error)
    finally:
        if conn is not None:
            conn.close()
            print('Database connection closed.')


if __name__ == '__main__':
    connect()
    
```

## 7. Querys

### 7.1 Creación de tablas

```bash
postgres=# CREATE TABLE CRICKETERS (
   First_Name VARCHAR(255),
   Last_Name VARCHAR(255),
   Age INT,
   Place_Of_Birth VARCHAR(255),
   Country VARCHAR(255)
);
CREATE TABLE
```

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


### 7.2 Insertar datos en las tablas

```bash
INSERT INTO datacamp_courses(course_name, course_instructor, topic)
VALUES('Deep Learning in Python','Dan Becker','Python');
INSERT INTO datacamp_courses(course_name, course_instructor, topic)
VALUES('Joining Data in PostgreSQL','Chester Ismay','SQL');
```

### 7.3 Aptualizar un registro en una tabla

```bash
UPDATE datacamp_courses SET course_name = 'Joining Data in SQL'
WHERE course_instructor = 'Chester Ismay';
```

### 7.4 Leer datos de una tabla

```bash
select * from datacamp_courses;
```

### 7.5 Borrar datos de una tabla

```bash
delete from datacamp_courses where course_name = 'Deep Learning in Python';
```

```python
cur.execute("DELETE FROM parts WHERE part_id = %s", (part_id,))
# get the number of updated rows
rows_deleted = cur.rowcount

conn.commit()

cur.close()
conn.close()
```

### 7.6 Crear una tabla desde python

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


```python
#!/usr/bin/python

import psycopg2
from config import config


def create_tables():
    """ create tables in the PostgreSQL database"""
    commands = (
        """
        CREATE TABLE vendors (
            vendor_id SERIAL PRIMARY KEY,
            vendor_name VARCHAR(255) NOT NULL
        )
        """,
        """ CREATE TABLE parts (
                part_id SERIAL PRIMARY KEY,
                part_name VARCHAR(255) NOT NULL
                )
        """,
        """
        CREATE TABLE part_drawings (
                part_id INTEGER PRIMARY KEY,
                file_extension VARCHAR(5) NOT NULL,
                drawing_data BYTEA NOT NULL,
                FOREIGN KEY (part_id)
                REFERENCES parts (part_id)
                ON UPDATE CASCADE ON DELETE CASCADE
        )
        """,
        """
        CREATE TABLE vendor_parts (
                vendor_id INTEGER NOT NULL,
                part_id INTEGER NOT NULL,
                PRIMARY KEY (vendor_id , part_id),
                FOREIGN KEY (vendor_id)
                    REFERENCES vendors (vendor_id)
                    ON UPDATE CASCADE ON DELETE CASCADE,
                FOREIGN KEY (part_id)
                    REFERENCES parts (part_id)
                    ON UPDATE CASCADE ON DELETE CASCADE
        )
        """)
    conn = None
    try:
        # read the connection parameters
        params = config()
        # connect to the PostgreSQL server
        conn = psycopg2.connect(**params)
        cur = conn.cursor()
        # create table one by one
        for command in commands:
            cur.execute(command)
        # close communication with the PostgreSQL database server
        cur.close()
        # commit the changes
        conn.commit()
    except (Exception, psycopg2.DatabaseError) as error:
        print(error)
    finally:
        if conn is not None:
            conn.close()


if __name__ == '__main__':
    create_tables()
    
```














