L'account **SA** è un account di amministratore di sistema dell'istanza di SQL Server creato durante l'installazione. Dopo aver creato il contenitore SQL Server, la variabile di ambiente `MSSQL_SA_PASSWORD` specificata diventa individuabile eseguendo `echo $MSSQL_SA_PASSWORD` nel contenitore. Per motivi di sicurezza, modificare la password dell'amministratore di sistema:

1. Scegliere una password complessa da usare per l'utente SA.

1. Usare `docker exec` per eseguire l'utilità **sqlcmd** per modificare la password tramite un'istruzione Transact-SQL. Sostituire `<YourStrong!Passw0rd>` e `<YourNewStrong!Passw0rd>` con valori di password:

   ```bash
   sudo docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
      -S localhost -U SA -P '<YourStrong!Passw0rd>' \
      -Q 'ALTER LOGIN SA WITH PASSWORD="<YourNewStrong!Passw0rd>"'
   ```

   ```PowerShell
   docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd `
      -S localhost -U SA -P "<YourStrong!Passw0rd>" `
      -Q "ALTER LOGIN SA WITH PASSWORD='<YourNewStrong!Passw0rd>'"
   ```
