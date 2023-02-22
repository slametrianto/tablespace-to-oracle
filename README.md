# tablespace-to-oracle


=> create tablespace
create tablespace Training
datafile '/u01/app/oracle/oradata/DBbpn/training01.dbf' size 100m 
autoextend on next 50m maxsize unlimited logging online permanent 
extent management local autoallocate blocksize 8k
segment space management auto flashback on;

=> cek tablespace
select * from dba_tablespaces;

