---
title: "🐘 PostgreSQL Logical Backups – Complete Guide"
datePublished: Sun Sep 14 2025 17:03:29 GMT+0000 (Coordinated Universal Time)
cuid: cmfjy25i8000502lahbn95jdk
slug: postgresql-logical-backups-complete-guide
tags: postgresql, databases, devops, database-administrator

---

When running PostgreSQL in production, taking **backups** is one of the most critical responsibilities of a DBA or DevOps engineer. Without a proper backup and restore strategy, you risk data loss, corruption, and sleepless nights.

PostgreSQL offers two main categories of backups:

1. **Physical Backups** – file-level copies of the database cluster (e.g., `pg_basebackup`).
    
2. **Logical Backups** – SQL-based exports that describe database objects and their data.
    

In this blog, we’ll focus on **Logical Backups** and understand their types, usage, and practical examples.

---

## 🔹 What is a Logical Backup?

A **logical backup** stores the schema (tables, indexes, functions, etc.) and data in a format such as SQL or a compressed archive. Instead of copying files, it **extracts database contents** into a portable format that can be restored later.

Logical backups are ideal when you want:

* To migrate a database from one server to another.
    
* To take backups at the **database level** instead of the entire cluster.
    
* To move between PostgreSQL versions (e.g., from 13 → 17).
    
* To export/import data for development or testing.
    

---

## 🔹 Two Types of Logical Backups in PostgreSQL

### 1\. `pg_dump` – Single Database Backup

`pg_dump` is used to take a backup of a **single database**.

#### Example:

```bash
pg_dump -U postgres paymentdb | gzip > /backups/paymentdb_$(date +%F).sql.gz
```

* Only `paymentdb` schema + data are dumped.
    
* It does **not** include roles, permissions, or other databases.
    

#### Restore:

1. Create the target database:
    
    ```bash
    createdb paymentdb
    ```
    
2. Restore into it:
    
    ```bash
    gunzip -c /backups/paymentdb_2025-09-14.sql.gz | psql -U postgres -d paymentdb
    ```
    

✔️ Use this when:

* You only care about **one database** in a cluster.
    
* Migrating or sharing a single app’s data.
    

❌ Limitation:

* Users/roles and cluster-wide settings must be recreated manually.
    

---

### 2\. `pg_dumpall` – Entire Cluster Backup

`pg_dumpall` backs up **all databases** and **global objects** like roles and tablespaces.

#### Example:

```bash
pg_dumpall -U postgres | gzip > /backups/all_databases_$(date +%F).sql.gz
```

* Includes all databases (`postgres`, `template1`, `paymentdb`, etc.).
    
* Includes `CREATE ROLE`, `CREATE DATABASE`, and permissions.
    

#### Restore:

Simply run:

```bash
gunzip -c /backups/all_databases_$(date +%F).sql.gz | psql -U postgres
```

✔️ Use this when:

* You want a **full cluster backup** including users and permissions.
    
* Migrating entire PostgreSQL instances to a new server.
    

❌ Limitation:

* Not suitable for very large databases (SQL dump can be huge and slow).
    

---

* `pg_dump` → must create DB manually before restore and also user with required premisssions.
    
* `pg_dumpall` → no need, it creates databases and roles inside the dump.
    
* `pg_dumpall` only supports **plain-text SQL output**.
    
* Reason: it’s just a wrapper that runs `pg_dump` for each DB and stitches them together with roles, global objects, etc.
    
* So if you want **custom format** (`-Fc`), you must use `pg_dump` for each database separately.
    

👉 That’s why in production:

* For **single DB** backups → `pg_dump -Fc`.
    
* For **all DBs + roles** → use `pg_dumpall` (plain SQL)
    
* 🔹 What is `-Fc`?
    
    * `-F` = format
        
    * `c` = custom  
        So `-Fc` = **Custom format** dump.  
        (Other formats are `-Fp` = plain SQL, `-Ft` = tar)
        

### 🔹 What is Parallel Restore?

* Normal restore (`psql < dump.sql` or `pg_restore`) runs single-threaded.
    
* With **custom format**, you can tell `pg_restore` to use multiple jobs:
    

```bash
pg_dump -Fc mydb > mydb.dump
pg_restore -U postgres -d mydb -j 4 mydb.dump
```

* `-j 4` → runs 4 parallel worker jobs.
    
* This splits the restore across schemas, tables, and indexes simultaneously.
    
* Very useful for **large DBs (GB–TB range)** because index creation and data load happen faster.
    

## 🎯 Formats in `pg_dump`

When you run `pg_dump`, you can specify format using the `-F` flag:

| Option | Format | File extension | Features | Restore tool | Recommended for |
| --- | --- | --- | --- | --- | --- |
| `-Fp` | **Plain SQL** (default) | `.sql` | Human-readable SQL script with `CREATE` and `INSERT` statements. Easy to inspect & edit, but **slow restore** for big DBs. | `psql` | Small DBs, debugging, portability |
| `-Fc` | **Custom format** | `.dump` | Compressed, compact, allows **parallel restore** (`pg_restore -j`), selective restore (only certain tables/schemas). | `pg_restore` | Production backups, large DBs, faster restore |
| `-Fd` | **Directory format** | Directory with multiple files | Each table dumped separately → **parallel restore & parallel dump**. Can restore only parts. Not a single file → harder to move around. | `pg_restore` | Very large DBs, when parallel dump/restore speed is critical |
| `-Ft` | **Tar archive** | `.tar` | Standard tar file. Can be compressed by external tools. Supports `pg_restore`. Doesn’t support parallel restore. | `pg_restore` | When you want one portable archive file but still need `pg_restore` features |

---

## ✅ Recommended Practice

* For **everyday production backups** → `-Fc` (Custom format) is recommended:
    
    * It’s compressed
        
    * Easy to store & move
        
    * Works with `pg_restore` (fast, parallel, selective restore)
        
* For **very large databases (hundreds of GBs → TBs)** → `-Fd` (Directory format) with multiple jobs (`-j`) is best.
    
* Use `-Fp` (plain SQL) only when:
    
    * DB is small
        
    * You need human-readable SQL
        
    * Or migrating to another DB system
        
* `-Ft` (tar) is rarely used in practice — only if you specifically want a tarball for archiving.
    

---

👉 So, **best recommendation**:

* `pg_dump -U postgres -Fc mydb > mydb.dump` (for most cases)
    
* Or `pg_dump -U postgres -Fd backupdir -j 4 mydb` (for very large DBs with parallelism)
    

✅ So summary:

* **pg\_dumpall** = only plain text (no `-Fc`).
    
* **pg\_dump -Fc** = custom format, supports **parallel restore** with `pg_restore -j`.
    
* **Plain SQL format (default, no** `-F` option)
    
    * Output is just SQL commands.
        
    * Usually named with `.sql`
        
    * Example:
        
        ```bash
        pg_dump -U postgres -C myappdb > myappdb.sql
        createdb -U postgres myappdb
        psql -U postgres -d myappdb -f myappdb.sql
        ```
        
    
    **Custom format (**`-Fc`)
    
    * Output is a compressed, binary archive.
        
    * Usually named with `.dump` (or `.backup`).
        
    * Needs `pg_restore` for restore.
        
    * Example:
        
        ```bash
        pg_dump -U postgres -Fc myappdb > myappdb.dump
        pg_restore -U postgres -d myappdb myappdb.dump
        ```
        
* **Directory format (**`-Fd`)
    
    * Output is a directory containing one file per table.
        
    * Restore with `pg_restore`.
        
* **Tar format (**`-Ft`)
    
    * Output is a tar archive.
        
    * Restore with `pg_restore`.
        

📌 So:

* If you use **default SQL dump** → `.sql` makes sense.
    
* If you use **custom format (-Fc)** → `.dump` (or `.backup`) is the convention.
    
* Use `.sql` if you want portability, readability, or to quickly replay commands.
    
* Use `.dump` if you want faster backup/restore and advanced options (`pg_restore --jobs=N` for parallel restore).