
## <a name="add-a-database-to-the-availability-group"></a>Aggiungere un database al gruppo di disponibilità

Verificare che il database che si aggiunge al gruppo di disponibilità sia in modalità di ripristino completa e disponga di un backup del log valido. Se si tratta di un database di prova o di un database appena creato, eseguire un backup del database. Per creare un database denominato `db1` ed eseguirne il backup, eseguire lo script Transact-SQL seguente sull'istanza primaria di SQL Server:

```sql
CREATE DATABASE [db1];
ALTER DATABASE [db1] SET RECOVERY FULL;
BACKUP DATABASE [db1]
   TO DISK = N'c:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\Backup\db1.bak';
```

Per aggiungere un database denominato `db1` a un gruppo di disponibilità denominato `ag1`, eseguire lo script Transact-SQL seguente nella replica di SQL Server primaria:

```sql
ALTER AVAILABILITY GROUP [ag1] ADD DATABASE [db1];
```

### <a name="verify-that-the-database-is-created-on-the-secondary-servers"></a>Verificare che il database sia creato nei server secondari

Per verificare che il database `db1` sia stato creato e sia sincronizzato, eseguire la query seguente in ogni replica secondaria di SQL Server:

```sql
SELECT * FROM sys.databases WHERE name = 'db1';
GO
SELECT DB_NAME(database_id) AS 'database', synchronization_state_desc FROM sys.dm_hadr_database_replica_states;
```
