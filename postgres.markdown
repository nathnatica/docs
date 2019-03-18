
### Cygwin Postgres  
##### add /usr/sbin to PATH  
cygserver-config  
cygrunsrv -S cygserver  
initdb -D /usr/local/pgsql/data  
postmaster -D /usr/local/pgsql/data -i &  

#### CREATE DATABASE1  
##### psql -h localhost -p 5432 -U [user] -l   
psql -h localhost -p 5432 -U park -l  
dropdb -h localhost -p 5432 -i -e testdb  
psql -h localhost -p 5432 -U park -l  
createdb -O park -T postgres testdb  
psql -h localhost -p 5432 -U park testdb  

#### CREATE DATABASE2  
##### create a new database from other database  
sudo su postgres  
psql  
CREATE DATABASE new_database_name WITH TEMPLATE originaldb OWNER me;  
GRANT ALL PRIVILEGES ON DATABASE new_database_name TO my_user;  
\l  

#### CREATE DATABASE3  
psql -h localhost -p 5432 -U postgres;
DROP ROLE me;
CREATE ROLE me WITH PASSWORD 'password' VALID UNTIL '2030-12-31' CREATEDB LOGIN;
alter user me VALID UNTIL 'infinity';

CREATE DATABASE test_db OWNER me;
GRANT ALL PRIVILEGES ON DATABASE test_db TO me;

psql -h jmas001 -p 5432 -U me -d test_db;

drop schema test_db_psgr cascade;
create schema test_db_psgr;

alter user me set search_path to test_db_psgr;
grant usage on schema test_db_psgr to me;

drop table test_db_psgr.temp;
create table test_db_psgr.temp(
  ID INT NOT NULL,
  NAME VARCHAR(30),
  QTY INT NOT NULL
);


#### CREATE NEW USER  
##### do with postgres  
createuser -P -e park  
##### or this is better  
DROP ROLE me  
CREATE ROLE me WITH PASSWORD 'mypassword' VALID UNTIL '2020-12-31' CREATEDB LOGIN  
alter user me VALID UNTIL 'infinity';


#### show user list
postgres=# select * from pg_user;
postgres=# select * from pg_shadow;


#### file load  
psql -U user -d database -a -f pathtofile  


#### record lock release  
select * from pg_locks l, pg_stat_all_tables t where l.relation = t.relid and relname = 'table_name';  
select pg_terminate_backend('pid');  


#### prepared statement  
prepare sel_sql (varchar, integer) as select $1 as code from table where key = $2;  
execute sel_sql('01', 1);  


#### copy  
##### load data from csv  
###### input.sql  
\copy table_name FROM 'path/to/csv/file' WITH CSV;  
###### load command  
psql -h <host> -p <port> -U <user> -d <database> -a -f ./input.sql  

##### out table data to csv (wrap all element with double quote)  
###### output.sql  
\copy table_name TO 'path/to/csv/file' WITH CSV ENCODING 'SJIS' FORCE QUOTE *;  
###### load command  
psql -h <host> -p <port> -U <user> -d <database> -a -f ./output.sql  
