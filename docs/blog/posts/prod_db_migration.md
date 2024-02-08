# Migrating RDS MySQL Community Database to Aurora MySQL (8.0.33)

## Overview
This document outlines the steps involved in migrating an RDS MySQL Community Database (version 8.0.33) to Aurora MySQL. The migration process involves creating an EC2 instance, taking a database dump, and restoring it to the Aurora MySQL instance.

### Step 1: EC2 Instance Setup
1.1. Create an EC2 instance with security group configurations allowing connections to both the source (RDS MySQL) and destination (Aurora MySQL) databases.

### Step 2: Dump Configuration
2.1. Ensure that the EC2 instance has access to both the source (RDS MySQL) and destination (Aurora MySQL) databases.

2.2. Determine which databases need to be migrated. Exclude internal databases like `mysql`, `performance_schema`, and include only user-created databases.

### Step 3: Dump Command
3.1. Execute the following command to take a dump from the source RDS MySQL database:

```bash
nohup sh -c "(mysqldump -h SOURCE_DB_ENDPOINT -u 'admin' -p'PASSWORD' --databases DB1 DB2 DB3 --no-create-info --set-gtid-purged=OFF | gzip > newdump.sql.gz) 2> pr.logs &"
```

Replace the following placeholders:
- `SOURCE_DB_ENDPOINT`: Endpoint of the source RDS MySQL database.
- `PASSWORD`: Password for the 'admin' user.
- `DB1 DB2 DB3`: List of user-created databases to be included in the dump.

3.2. Explanation of command:
   - `mysqldump`: MySQL database dump utility.
   - `-h`: Hostname of the source RDS MySQL database.
   - `-u`: MySQL user ('admin' in this case).
   - `-p`: Password for the MySQL user.
   - `--databases`: List of databases to be included in the dump.
   - `--no-create-info`: Do not include CREATE TABLE statements.
   - `--set-gtid-purged=OFF`: Disable GTID purging to ensure consistency during restoration.
   - `gzip`: Compress the dump.
   - `> newdump.sql.gz`: Save the compressed dump to a file.
   - `2> pr.logs`: Redirect error output to a log file.

### Step 4: Restore Command
4.1. Execute the following command to restore the dump to the Aurora MySQL database:

```bash
gunzip -dv newdump.sql.gz | mysql -h DESTINATION_DB_ENDPOINT -u 'admin' -p'PASSWORD'
```

Replace the following placeholders:
- `DESTINATION_DB_ENDPOINT`: Endpoint of the destination Aurora MySQL database.
- `PASSWORD`: Password for the 'admin' user.

4.2. Explanation of command:
   - `gunzip -dv newdump.sql.gz`: Decompress the dump file.
   - `|`: Pipe the decompressed data to the next command.
   - `mysql -h`: Connect to the Aurora MySQL database.
   - `DESTINATION_DB_ENDPOINT`: Endpoint of the destination Aurora MySQL database.
   - `-u`: MySQL user ('admin' in this case).
   - `-p`: Password for the MySQL user.

### Conclusion
By following these steps, you can successfully migrate your RDS MySQL Community Database to Aurora MySQL (8.0.33). Ensure to validate the migration in the destination environment before making any production changes.