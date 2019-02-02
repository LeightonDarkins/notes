# POSTGRES

## PSQL

**CONNECT TO DB**

- `psql -U username -d database-name`
  - TRACKER - `psql -U trackeruser -d tracker`
  - PSS - `psql -U pssadmin -d pssemr`

**LIST ALL USERS**

- `\du`

**CREATE A NEW DB**

- `CREATE DATABASE [db-name];`

**CREATE A NEW USER**

- `CREATE USER [username] WITH ENCRYPTED PASSWORD ‘[some-password]’;`

**GIVE USER ALL PERMS TO DB**

- `GRANT ALL PRIVILEGES ON DATABASE [db-name] TO [username];`

## PG_CTL

- pg_ctl commands need to be executed by the “postgres” user

  - `sudo su postgres`
  - [enter local admin password]
  - now working as the user “postgres”

- `pg_ctl —help`
- `pg_ctl stop -D /Library/PostgreSQL/9.3/data`
- `pg_ctl start -D /Library/PostgreSQL/9.3/data -l /Library/PostgreSQL/9.3/data/server.log`
