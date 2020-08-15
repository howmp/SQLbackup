# SQLbackup

- SQL backup command line tool (written in go)

- BUILD 
  - `go build .`
  - `mv m sqlbackup`

- Usage
  - `sqlbackup user/pass@tnsaddr [-d]`
    - `-d ` drop table before create

  - write SQL dump for all table in database user

- caution
  - indexes are ignored
  
- eg. `sqlbackup $OCISTRING -d >test.sql`

```sql
DROP TABLE "TESTBLOB";

  CREATE TABLE "ADMIN"."TESTBLOB" 
   (    "BL1" BLOB, 
        "ID" NUMBER
   )  DEFAULT COLLATION "USING_NLS_COMP" SEGMENT CREATION IMMEDIATE 
  PCTFREE 10 PCTUSED 40 INITRANS 1 MAXTRANS 255 
 NOCOMPRESS NOLOGGING
  STORAGE(INITIAL 65536 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0 FREELISTS 1 FREELIST GROUPS 1
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)
  TABLESPACE "DATA" 
 LOB ("BL1") STORE AS SECUREFILE (
  TABLESPACE "DATA" ENABLE STORAGE IN ROW CHUNK 8192
  NOCACHE NOLOGGING  NOCOMPRESS  KEEP_DUPLICATES 
  STORAGE(INITIAL 106496 NEXT 1048576 MINEXTENTS 1 MAXEXTENTS 2147483645
  PCTINCREASE 0
  BUFFER_POOL DEFAULT FLASH_CACHE DEFAULT CELL_FLASH_CACHE DEFAULT)) ;

SET DEFINE OFF;
Insert Into TESTBLOB ("BL1","ID") VALUES (HEXTORAW('01020304'),2);
Insert Into TESTBLOB ("BL1","ID") VALUES (HEXTORAW('01020304'),1);
```
