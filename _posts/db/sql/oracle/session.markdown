---
layout: post
title:  "Oracle会话"
date:   2016-10-11 13:21:30
categories: oracle
---

### 会话相关表
```
SELECT * FROM V$SESSION;
SELECT * FROM V$PROCESS;
SELECT * FROM V$SESS_IO;
```

### 查看当前会话
```
SELECT S.USERNAME,
       S.PROGRAM,
       DECODE(S.COMMAND,
              0, 'NO COMMAND',
              1, 'CREATE TABLE',
              2, 'INSERT',
              3, 'SELECT',
              6, 'UPDATE',
              7, 'DELETE',
              9, 'CREATE INDEX',
              15, 'ALTER TABLE',
              21, 'CREATE VIEW',
              23, 'VALIDATE INDEX',
              35, 'ALTER DATABASE',
              39, 'CREATE TABLESPACE',
              41, 'DROP TABLESPACE',
              40, 'ALTER TABLESPACE',
              53, 'DROP USER',
              62, 'ANALYZE TABLE',
              63, 'ANALYZE INDEX',
              S.COMMAND || ': OTHER') COMMAND
FROM V$SESSION S,
     V$PROCESS P,
     V$TRANSACTION T,
     V$ROLLSTAT R,
     V$ROLLNAME N
WHERE S.PADDR = P.ADDR
  AND S.TADDR = T.ADDR (+)
  AND T.XIDUSN = R.USN (+)
  AND R.USN = N.USN (+)
ORDER BY 1
;
```

### 查看DML会话
```
SELECT S.USERNAME,
       S.PROGRAM,
       DECODE(S.COMMAND,
              2, 'INSERT',
              3, 'SELECT',
              6, 'UPDATE',
              7, 'DELETE') COMMAND,
       L.SQL_TEXT
FROM V$SESSION S,
     V$PROCESS P,
     V$TRANSACTION T,
     V$ROLLSTAT R,
     V$ROLLNAME N,
     V$SQLAREA L
WHERE S.PADDR = P.ADDR
  AND S.TADDR = T.ADDR (+)
  AND T.XIDUSN = R.USN (+)
  AND R.USN = N.USN (+)
  AND S.SQL_ID = L.SQL_ID (+)
  AND S.COMMAND IN (2, 3, 6, 7)
```


### 参考
+ Oracle Database Reference