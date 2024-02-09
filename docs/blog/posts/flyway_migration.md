---
title: Flyway Migration Documentation
date: 2024-01-30
authors: [amanw]
slug: Flyway-Migration-Documentation
description: >
  Guide to Flyway migration and configuration
categories:
  - DevOps
tags:
  - DevOps
  - Database
  - Flyway
---
# Flyway Migration Documentation

## Overview

The Flyway migration process involves configuring Flyway with database connection details, creating an initial migration script (`V1__Create_person_table.sql`), and executing the migration using a Docker command. This applies defined changes to the database schema.

Verification is performed through a separate Docker run using the `info` command, displaying the current schema version and migration history. This systematic approach ensures organized and version-controlled database schema evolution.

<!-- more -->

## Prerequisites

Begin your Flyway journey by grabbing the Flyway Teams or Enterprise Docker image for your Docker environment.
```bash
docker pull redgate/flyway
```

## Setup

### Configuration (flyway.conf)

Ensure your `flyway.conf` file is properly configured with the necessary database connection details:

```properties
flyway.url=jdbc:postgresql://localhost:5432/test?user=postgres&password=postgres
flyway.user=postgres
flyway.password=postgres
```

## Creating the First Migration

Forge ahead and craft your inaugural migration SQL, naming it `V1__Create_person_table.sql`:

```sql
-- V1__Create_person_table.sql
create table PERSON (
    ID int not null,
    NAME varchar(100) not null
);
```

## Migrating the Database

Execute Flyway to migrate schemas to database with below command

```bash
docker run --rm -v "{absolute path to folder for postgresql db file}:/flyway/db" \
    -v "{absolute path to sql migrations folder}:/flyway/sql" \
    -v "{absolute path to conf file folder}:/flyway/conf" \
    redgate/flyway migrate
```
for example
```bash
docker run --rm -v "/home/ubuntu/dbfile:/flyway/db" \
    -v "/home/ubuntu/sqlfile:/flyway/sql" \
    -v "/home/ubuntu/flwayconf:/flyway/conf" \
    redgate/flyway migrate
```


If the stars align, your terminal should gleefully declare:

```bash
Database: jdbc:postgresql://localhost:5432/test (PostgreSQL 16.1)
Schema history table "public"."flyway_schema_history" does not exist yet
Successfully validated 1 migration (execution time 00:00.047s)
Creating Schema History table "public"."flyway_schema_history" ...
Current version of schema "public": << Empty Schema >>
Migrating schema "public" to version "1 - Create person"
Successfully applied 1 migration to schema "public", now at version v1 (execution time 00:00.011s)
```

## Verification

Double-check Flyway's magic with the info command:

```bash
docker run --rm -v "{absolute path to folder for SQLite db file}:/flyway/db" \
    -v "{absolute path to sql migrations folder}:/flyway/sql" \
    -v "{absolute path to conf file folder}:/flyway/conf" \
    redgate/flyway info
```

Behold the revelation:

```bash
Database: jdbc:sqlite:/flyway/db/test_db.sqlite3 (SQLite 3.34)
Schema version: 2

+-----------+---------+---------------------+------+---------------------+---------+----------+
| Category  | Version | Description         | Type | Installed On        | State   | Undoable |
+-----------+---------+---------------------+------+---------------------+---------+----------+
| Versioned | 1       | Create person table | SQL  | 2023-04-26 13:01:02 | Success | No       |
| Versioned | 2       | Add people          | SQL  | 2023-04-26 13:05:04 | Success | No       |
+-----------+---------+---------------------+------+---------------------+---------+----------+
```
