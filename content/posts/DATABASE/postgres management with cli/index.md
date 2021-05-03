---
title: Postgres Management with the CLI
date: 2021-04-25
tags: [database]
image: "postgres.png"
---

PostgreSQL is an object-relational database management system (ORDBMS). It is widely used as an enterprise database management system. In this article I will show you what commands I use on the postgres CLI to install, manage and run the database for my projects

#### Installation

```bash
$ sudo apt-get install postgresql # latest version
# or
$ sudo apt-get install postgresql-12 # specific version
```

#### Run postgres CLI with a particular user

```bash
$ sudo su username  # Change user to postgres
$ psql              # Go to the postgres CLI
```

Or do it one go

```bash
$ psql -U username  
```

#### Login with the default postgres user

```bash
$ psql -U postgres 
```

#### Create a user

```bash
$ psql -U postgres -c "create user john createdb password 'john_snow'"
```

#### Export a database in SQL form

```bash
$ pg_dump -U postgres db_name > export_file.sql
```

#### Import database

```bash
$ sudo su postgres
$ psql teq-db < export_file.sql 
```

#### Create and delete database

```sql
postgres=# drop database "db_name";
```

```sql
postgres=# create database "db_name";
```
