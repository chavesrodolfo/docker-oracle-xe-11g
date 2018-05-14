docker-oracle-xe-11g
============================

Oracle Express Edition 11g Release 2 on Ubuntu 18.04 LTS

## Installation(with Ubuntu 18.04)

## Quick Start

Clone the project
```
git clone https://github.com/chavesrodolfo/docker-oracle-xe-11g.git
```
Move to the directory

Build an image
```
docker build --rm -t oracle-xe .
```

Save an image
```
docker save -o oracle-xe.tar oracle-xe
```

Load an image (if you need)
```
docker load -i oracle-xe.tar
```

Run a container 
```
docker run --name oracle-xe -d -p 1522:22 -p 1521:1521 oracle-xe
```

Get logs
```
docker logs -f oracle-xe
```

Connect database with following setting:
```
hostname: localhost
port: 1521
sid: xe
username: system
password: oracle
or
username: sys
password: oracle
or
username: XDB
password: xdb
```


## Oracle Setup
```
CREATE TEMPORARY TABLESPACE tbs_temp_01
  TEMPFILE 'tbs_temp_01.dbf'
    SIZE 5M
    AUTOEXTEND ON;
    
CREATE TABLESPACE tbs_perm_01
  DATAFILE 'tbs_perm_01.dat' 
    SIZE 10M
    REUSE
    AUTOEXTEND ON NEXT 10M MAXSIZE 200M;

CREATE USER LOCAL_OWNER
  IDENTIFIED
  BY pwd
  DEFAULT TABLESPACE tbs_perm_01
  TEMPORARY TABLESPACE tbs_temp_01
  QUOTA 50M on tbs_perm_01;
  
grant create session to LOCAL_OWNER;  
```
Now you can use LOCAL_OWNER with password pwd

Unlock User
```
ALTER USER XDB ACCOUNT UNLOCK;
```
