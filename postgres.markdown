
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

#### CREATE NEW USER  
##### do with postgres  
createuser -P -e park  
##### or this is better  
DROP ROLE me  
CREATE ROLE me WITH PASSWORD 'mypassword' VALID UN-TIL '2020-12-31' CREATEDB LOGIN  


#### file load  
psql -U user -d database -a -f pathtofile  


#### record lock release  
select * from pg_locks l, pg_stat_all_tables t where l.relation = t.relid and relname = 'table_name';  
select pg_terminate_backend('pid');  


#### prepared statement  
prepare sel_sql (varchar, integer) as select $1 as code from table where key = $2;  
execute sel_sql('01', 1);  


