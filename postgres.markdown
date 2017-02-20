
### Cygwin Postgres  
##### add /usr/sbin to PATH  
cygserver-config  
cygrunsrv -S cygserver  
initdb -D /usr/local/pgsql/data  
postmaster -D /usr/local/pgsql/data -i &  

#### CREATE DATABASE1  
##### psql -h localhost -p 5432 -U [user] -l   
psql -h localhost -p 5432 -U me -l  
psql -h localhost -p 5432 -U me postgres  
dropdb -h localhost -p 5432 -i -e testdb  
createdb -O me -T postgres testdb  

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




