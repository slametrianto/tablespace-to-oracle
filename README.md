# tablespace-to-oracle


=> create tablespace
create tablespace Training
datafile '/u01/app/oracle/oradata/DBbpn/training01.dbf' size 100m 
autoextend on next 50m maxsize unlimited logging online permanent 
extent management local autoallocate blocksize 8k
segment space management auto flashback on;

=> cek tablespace
select * from dba_tablespaces;


=>cek datafile tablespace
Select name from v$datafile;


=> create tablespace ASM(automatic storage management)
alter tablespace BERKAS  add datafile '+DATA' size 10M;

=> cek tbs
SELECT DFQ.TABLESPACE_NAME "Tablespace Name"
      ,DFQ.TOTALSPACE "Total Size MB"
      , (DFQ.TOTALSPACE - DSQ.TOTALUSEDSPACE) "Free Space MB"
      ,ROUND (100 * ( (DFQ.TOTALSPACE - DSQ.TOTALUSEDSPACE) / DFQ.TOTALSPACE)) || '%' "Free Space %"
FROM   (SELECT   TABLESPACE_NAME, ROUND (SUM (BYTES) / 1048576) TOTALSPACE
        FROM     DBA_DATA_FILES
        GROUP BY TABLESPACE_NAME) DFQ
      ,(SELECT   TABLESPACE_NAME, ROUND (SUM (BYTES) / (1024 * 1024)) TOTALUSEDSPACE
        FROM     DBA_SEGMENTS
        GROUP BY TABLESPACE_NAME) DSQ
WHERE  DFQ.TABLESPACE_NAME = DSQ.TABLESPACE_NAME(+);

