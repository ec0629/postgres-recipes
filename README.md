# Table of Contents
  - [Getting a DB up and running using docker](#getting-a-db-up-and-running-using-docker)
  - [Customizing the psql command prompt](#customizing-the-psql-command-prompt)

## Getting a DB up and running using docker
1. Uncomment the desired database name from the docker-compose.yml file
2. start the container
```shell
$ docker-compose up
```
3. start a interactive terminal session into the running docker container
```shell
$ docker exec -it postgres-recipes_db_1 psql -U postgres
```

---

## Customizing the psql command prompt
- 3 psql variables available PROMPT1, PROMPT2, PROMPT3
- PROMPT1 is shown for new command input
- PROMPT2 is showm for commands spanning multiple lines, starting with the second line
```sql
\set PROMPT1 '(%n@%M:%>) [%/]%R%#%x > '
```
 the prompt will now appear as: (*username*@*hostname*:*port*) \[*dbname*\]=# >
- **%** is a substitution placeholder
- **%n** db session username
- **%M** full host name
- **%>** port number
- **%/** current db
- **%R** substituted by = unless db connection is lost then !
- **%#** distinguishes normal users vs superusers, # superuser, > normal user
- **%x** transaction status, * transaction block, ! failed transaction block

---

## Adding a sql comand shortcut in psql
[PostgreSQL Docs - Prompting](https://www.postgresql.org/docs/current/app-psql.html#APP-PSQL-PROMPTING)
```sql
\set activity 'select datname, pid from pg_stat_activity;'
:activity
```