# dba
# 📘 Top 20 Important Oracle 21c Commands

This README contains **20 essential Oracle Database 21c commands** commonly used by DBAs and developers. 
They cover database checks, PDB operations, users, tablespaces, and new 21c features such as blockchain and immutable tables.

> Note:
> - Some commands require SYSDBA privileges
> - Replace sample names (users, PDBs, paths) with your environment values

---

## 🟢 1) Check database name and role
SELECT name, open_mode, database_role FROM v$database;

## 🟢 2) Check instance status
SELECT instance_name, status FROM v$instance;

## 🟢 3) List all PDBs
SHOW PDBS;

## 🟢 4) Open all pluggable databases
ALTER PLUGGABLE DATABASE ALL OPEN;

## 🟢 5) Save state of PDBs on startup
ALTER PLUGGABLE DATABASE ALL SAVE STATE;

## 🟢 6) Create a new pluggable database (PDB)
CREATE PLUGGABLE DATABASE pdb_test ADMIN USER pdbadmin IDENTIFIED BY password;

## 🟢 7) Switch to a PDB
ALTER SESSION SET CONTAINER = pdb_test;

## 🟢 8) Create user
CREATE USER john IDENTIFIED BY john123;

## 🟢 9) Grant basic privileges
GRANT CONNECT, RESOURCE TO john;

## 🟢 10) Grant DBA role (use carefully)
GRANT DBA TO john;

## 🟢 11) Unlock a user account
ALTER USER john ACCOUNT UNLOCK;

## 🟢 12) Change user password
ALTER USER john IDENTIFIED BY newpass;

## 🟢 13) Create a tablespace
CREATE TABLESPACE data01 
DATAFILE '/u01/app/oracle/oradata/data01.dbf' 
SIZE 500M AUTOEXTEND ON;

## 🟢 14) Add a datafile to tablespace
ALTER TABLESPACE data01 ADD DATAFILE '/u01/app/oracle/oradata/data02.dbf' SIZE 500M;

## 🟢 15) Check tablespace usage
SELECT tablespace_name, used_space, tablespace_size 
FROM dba_tablespace_usage_metrics;

## 🟢 16) Create a table
CREATE TABLE emp (
  emp_id NUMBER PRIMARY KEY,
  emp_name VARCHAR2(50),
  salary NUMBER
);

## 🟢 17) Create Blockchain Table (Oracle 21c feature)
CREATE BLOCKCHAIN TABLE secure_emp (
  emp_id NUMBER,
  emp_name VARCHAR2(50)
) NO DROP UNTIL 30 DAYS IDLE;

## 🟢 18) Create Immutable Table (Oracle 21c feature)
CREATE IMMUTABLE TABLE audit_log(
  id NUMBER,
  message VARCHAR2(200)
) 
NO DROP UNTIL 30 DAYS IDLE 
NO DELETE UNTIL 30 DAYS AFTER INSERT;

## 🟢 19) View active sessions
SELECT username, machine, program 
FROM v$session 
WHERE username IS NOT NULL;

## 🟢 20) Kill a session
ALTER SYSTEM KILL SESSION 'sid,serial#' IMMEDIATE;

### Find SID and SERIAL#
SELECT sid, serial# FROM v$session WHERE username='JOHN';

---

# ⭐ Bonus Useful Commands

## 🔹 Check Database Size
SELECT SUM(bytes)/1024/1024/1024 AS size_gb FROM dba_data_files;

## 🔹 Backup Controlfile to Trace
ALTER DATABASE BACKUP CONTROLFILE TO TRACE;

## 🔹 Listener Status (OS Command)
lsnrctl status

---

## ✅ What to learn next?

- RMAN backup commands
- Data Guard basics
- Performance tuning queries
- ASM commands
- AWR & ADDM usage
- PDB cloning and unplug/plug
- Oracle 21c new features

👉 Ask: **“Give RMAN commands”** or **“Only DBA commands”**
