# Oracle-APEX-Install-
How to Install Oracle Database 19c and Oracle APEX with ORDS
Create Tablespace apex
logging
datafile 'D:\Oracle\oradata\LIVE\APEX.DBF' size 1024m
autoextend on
next 64m maxsize 8G
extent management local;

@apexins apex apex temp /i/

@apxchpwd.sql


@apex_rest_config.sql
--- Enter password like 123

select username,account_status  from dba_users where username like 'APEX%'

ALTER USER APEX_LISTENER  ACCOUNT UNLOCK identified by 123;

ALTER USER APEX_PUBLIC_USER ACCOUNT UNLOCK identified by 123;

ALTER USER APEX_REST_PUBLIC_USER ACCOUNT UNLOCK identified by 123;

ALTER USER APEX_220100 ACCOUNT UNLOCK identified by 123;


BEGIN
DBMS_NETWORK_ACL_ADMIN.APPEND_HOST_ACE(
host => '*',
ace => xs$ace_type(privilege_list => xs$name_list('connect'),
principal_name => 'APEX_220100',
principal_type => xs_acl.ptype_db));
END;
/

BEGIN
DBMS_NETWORK_ACL_ADMIN.APPEND_HOST_ACE(
host => 'localhost',
ace => xs$ace_type(privilege_list => xs$name_list('connect'),
principal_name => 'APEX_220100',
principal_type => xs_acl.ptype_db));
END;
/


EXEC DBMS_XDB.sethttpport(0);


download jdk

https://www.oracle.com/java/technologies/javase-downloads.html

--Download Ords file as you required or support your apex versions....

https://www.oracle.com/database/technologies/appdev/rest-data-services-v192-downloads.html

#unzip ords file

copy images folder from apex directory and past to ords folder.


go to cmd

and enter ords directory

example

CD D:\Oracle\ords

java -jar ords.war
