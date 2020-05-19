---
title: Modifica di tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 690b70b7-5be1-4014-af97-54e531997839
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bcfa139cb854954d920a1148f3d5cebb907c61e4
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706561"
---
# <a name="altering-memory-optimized-tables"></a>Modifica di tabelle con ottimizzazione per la memoria
  L'esecuzione di operazioni ALTER nelle tabelle ottimizzate per la memoria non è supportata. Sono incluse le operazioni come la modifica di bucket_count oppure l'aggiunta e la rimozione di un indice o di una colonna. In questo argomento vengono fornite le linee guida su come aggiornare le tabelle ottimizzate per la memoria.  
  
## <a name="updating-the-definition-of-a-memory-optimized-table"></a>Aggiornamento della definizione di una tabella con ottimizzazione per la memoria  
 L'aggiornamento della definizione di una tabella ottimizzata per la memoria richiede la creazione di una nuova tabella con la definizione della tabella aggiornata e la copia dei dati nella nuova tabella, quindi sarà possibile utilizzare la nuova tabella. A meno che la tabella sia di sola lettura, questa operazione richiede l'arresto del carico di lavoro nella tabella per essere certi che non vengano apportate modifiche alla tabella mentre viene eseguita la copia dei dati.  
  
 Nella procedura riportata di seguito vengono illustrati i passaggi necessari per aggiornare una tabella. In questo esempio, l'aggiornamento aggiunge un indice. In questa procedura viene mantenuto il nome della tabella e vengono richieste due operazioni di copia di dati: una volta in una tabella temporanea e una volta nella nuova tabella. La modifica dell'elemento bucket_count di un indice oppure l'aggiunta o la rimozione di una colonna viene eseguita nello stesso modo.  
  
1.  Arrestare il carico di lavoro nella tabella.  
  
2.  Generare lo script per la tabella e aggiungere il nuovo indice allo script.  
  
3.  Generare lo script per gli oggetti associati allo schema (principalmente stored procedure compilate in modo nativo) che fanno riferimento a T e alle relative autorizzazioni.  
  
     Per trovare gli oggetti associati allo schema che fanno riferimento alla tabella utilizzare la query seguente:  
  
    ```sql  
    declare @t nvarchar(255) = N'<table name>'  
  
    select r.referencing_schema_name, r.referencing_entity_name  
    from sys.dm_sql_referencing_entities (@t, 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
    where r.is_caller_dependent = 0 and m.is_schema_bound=1;  
    ```  
  
     È possibile generare uno script delle autorizzazioni di una stored procedure utilizzando la seguente query [!INCLUDE[tsql](../../includes/tsql-md.md)]:  
  
    ```sql  
    declare @sp nvarchar(255) = N'<procedure name>'  
    declare @permissions nvarchar(max) = N''  
  
    select @permissions += dp.state_desc + N' ' + dp.permission_name + N' ON ' +   
       quotename(schema_name(o.schema_id)) + N'.' + quotename(o.name) + N' TO ' +  
       quotename(u.name) + N'; ' + char(13)  
    from sys.database_permissions as dp  
  
    join sys.database_principals as u  
       on u.principal_id = dp.grantee_principal_id  
  
    join sys.objects as o  
       on o.object_id = dp.major_id  
    where dp.class = 1 /* object */  
       and dp.minor_id = 0 and o.object_id=object_id(@sp);  
  
    select @permissions  
    ```  
  
4.  Creare una copia della tabella e copiare i dati dalla tabella originale alla copia della tabella. La copia può essere creata utilizzando il seguente [!INCLUDE[tsql](../../includes/tsql-md.md)] <sup>1</sup>.  
  
    ```sql  
    select * into dbo.T_copy from dbo.T  
    ```  
  
     Se la memoria disponibile è sufficiente, `T_copy` può essere una tabella ottimizzata per la memoria, che rende più veloce la copia dei dati.<sup> 2</sup>  
  
5.  Eliminare gli oggetti associati allo schema che fanno riferimento alla tabella originale.  
  
6.  Eliminare la tabella originale.  
  
7.  Creare la nuova tabella (`T`) con lo script che contiene il nuovo indice.  
  
8.  Copiare i dati da `T_copy` a `T`.  
  
9. Ricreare gli oggetti associati allo schema a cui si fa riferimento e applicare le autorizzazioni.  
  
10. Avviare il carico di lavoro su `T`.  
  
 <sup>1</sup> si noti che `T_copy` in questo esempio è salvato in modo permanente su disco. Se un backup di `T` è disponibile, l'utilità `T_copy` può essere una tabella temporanea o non durevole.  
  
 <sup>2</sup> è necessario disporre di memoria sufficiente per `T_copy` . La memoria non viene liberata immediatamente con `DROP TABLE`. Se `T_copy` è con ottimizzazione per la memoria, deve essere disponibile la memoria sufficiente per due copie aggiuntive di `T`. Se `T_copy` è basata su disco, deve essere disponibile la memoria sufficiente per una sola copia aggiuntiva di `T`, perché Garbage Collector richiede l'aggiornamento dopo l'eliminazione della versione precedente di `T`.  
  
## <a name="changing-schema-powershell"></a>Modifica dello schema (PowerShell)  
 Gli script di PowerShell seguenti preparano e generano le modifiche dello schema creando lo script della tabella e delle autorizzazioni associate.  
  
```powershell
prepare_schema_change.ps1 <serverName> <databaseName> <schemaName> <tableName>
```
  
 Questo script accetta come argomento una tabella e crea lo script dell'oggetto e delle relative autorizzazioni nonché degli oggetti associati allo schema a cui si fa riferimento e delle relative autorizzazioni nella cartella corrente. In totale vengono generati 7 script per aggiornare lo schema della tabella di input:  
  
-   Copiare i dati in una tabella temporanea (heap).  
  
-   Eliminare gli oggetti associati allo schema che fanno riferimento alla tabella.  
  
-   Eliminare la tabella.  
  
-   Ricreare la tabella con il nuovo schema e riapplicare le autorizzazioni.  
  
-   Copiare i dati dalla tabella temporanea nella tabella ricreata.  
  
-   Ricreare gli oggetti associati allo schema che fanno riferimento alla tabella e alle autorizzazioni.  
  
-   Eliminare la tabella temporanea.  
  
 Lo script per il passaggio 4 deve essere aggiornato per riflettere le modifiche apportate allo schema. Se sono state apportate modifiche alle colonne della tabella, gli script per i passaggi 5 (copiare i dati dalla tabella temporanea) e 6 (ricreare le stored procedure) devono essere aggiornati in base alle necessità.  
  
```powershell
# Prepare for schema changes by scripting out the table, as well as associated permissions
# Usage: prepare_schema_change.ps1 server_name db_name schema_name table_name  
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage prepare_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
$object_heap = "$object$(Get-Random)"  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | Out-Null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$scripter = New-Object ("Microsoft.SqlServer.Management.SMO.Scripter") ($server)  
  
## initialize table variable  
$tableUrn = $server.Databases[$database].Tables[$object, $schema]  
if($tableUrn.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
## initialize scripting object  
$scriptingOptions = New-Object ("Microsoft.SqlServer.Management.SMO.ScriptingOptions")
$scriptingOptions.Permissions = $True  
$scriptingOptions.ScriptDrops = $True  
  
$scripter.Options = $scriptingOptions;  
  
Write-Host "(1) Scripting SELECT INTO $object_heap for table [$object] to 1_copy_to_heap_for_$schema`_$object.sql"  
Echo "SELECT * INTO $schema.$object_heap FROM $schema.$object WITH (SNAPSHOT)" | Out-File "1_copy_to_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(2) Scripting DROP for procs schema-bound to [$object] 2_drop_procs_$schema`_$object.sql"  
## query referencing schema-bound objects  
$dt = $server.Databases[$database].ExecuteWithResults("select r.referencing_schema_name, r.referencing_entity_name  
from sys.dm_sql_referencing_entities ('$schema.$object', 'OBJECT') as r join sys.sql_modules m on r.referencing_id=m.object_id  
where r.is_caller_dependent = 0 and m.is_schema_bound=1;")  
  
## initialize out file  
Echo "" | Out-File "2_drop_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
ForEach ($t In $dt.Tables)  
{    
   ForEach ($r In $t.Rows)  
   {    
      ## script object   
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      $scripter.Script($so) | Out-File -Append "2_drop_procs_$schema`_$object.sql"  
   }  
}  
Write-Host "--done--"  
Write-Host ""  
Write-Host "(3) Scripting DROP table for [$object] to 3_drop_table_$schema`_$object.sql"
$scripter.Script($tableUrn) | Out-File "3_drop_table_$schema`_$object.sql";
Write-Host "--done--"  
Write-Host ""  
  
## now script creates  
$scriptingOptions.ScriptDrops = $False  
  
Write-Host "(4) Scripting CREATE table and permissions for [$object] to !please_edit_4_create_table_$schema`_$object.sql"  
Write-Host "***** rename this script to 4_create_table.sql after completing the updates to the schema"
$scripter.Script($tableUrn) | Out-File "!please_edit_4_create_table_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(5) Scripting INSERT INTO table from heap and UPDATE STATISTICS for [$object] to 5_copy_from_heap_$schema`_$object.sql"  
Write-Host "[update this script if columns are added to or removed from the table]"  
Echo "INSERT INTO [$schema].[$object] SELECT * FROM [$schema].[$object_heap]; UPDATE STATISTICS [$schema].[$object] WITH FULLSCAN, NORECOMPUTE" | Out-File "5_copy_from_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(6) Scripting CREATE PROC and permissions for procedures schema-bound to [$object] to 6_create_procs_$schema`_$object.sql"  
Write-Host "[update the procedure definitions if columns are renamed or removed]"  
## initialize out file  
Echo "" | Out-File "6_create_procs_$schema`_$object.sql"  
## loop through schema-bound objects  
ForEach ($t In $dt.Tables)  
{    
   ForEach ($r In $t.Rows)  
   {    
      ## script the schema-bound object  
      $so =  $server.Databases[$database].StoredProcedures[$r[1], $r[0]]  
      ForEach($s In $scripter.Script($so))  
        {  
            Echo $s | Out-File -Append "6_create_procs_$schema`_$object.sql"  
            Echo "GO" | Out-File -Append "6_create_procs_$schema`_$object.sql"  
        }  
   }  
}  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(7) Scripting DROP $object_heap to 7_drop_heap_$schema`_$object.sql"  
Echo "DROP TABLE $schema.$object_heap" | Out-File "7_drop_heap_$schema`_$object.sql";  
Write-Host "--done--"  
Write-Host ""  
```  
  
 Il seguente script di PowerShell esegue le modifiche dello schema che erano state inserite nello script nell'esempio precedente. Questo script accetta come argomento una tabella ed esegue gli script delle modifiche dello schema generate per la tabella e le stored procedure associate.  
  
 Utilizzo: execute_schema_change. ps1 *server_name * * db_name `schema_name` table_name*  
  
```powershell
# stop execution once an error occurs  
$ErrorActionPreference="Stop"  
  
if($args.Count -le 3)  
{  
   throw "Usage execute_schema_change.ps1 server_name db_name schema_name table_name"  
}  
  
$servername = $args[0]  
$database = $args[1]  
$schema = $args[2]  
$object = $args[3]  
  
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.SMO") | Out-Null  
  
$server =  New-Object ("Microsoft.SqlServer.Management.SMO.Server") ($servername)  
$database = $server.Databases[$database]  
$table = $database.Tables[$object, $schema]  
if($table.Count -eq 0)  
{  
   throw "Table or database not found"  
}  
  
$1 = Get-Item "1_copy_to_heap_$schema`_$object.sql"  
$2 = Get-Item "2_drop_procs_$schema`_$object.sql"  
$3 = Get-Item "3_drop_table_$schema`_$object.sql"  
$4 = Get-Item "4_create_table_$schema`_$object.sql"  
$5 = Get-Item "5_copy_from_heap_$schema`_$object.sql"  
$6 = Get-Item "6_create_procs_$schema`_$object.sql"  
$7 = Get-Item "7_drop_heap_$schema`_$object.sql"  
  
Write-Host "(1) Running SELECT INTO heap for table [$object] from 1_copy_to_heap_for_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $1.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(2) Running DROP for procs schema-bound from [$object] 2_drop_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $2.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(3) Running DROP table for [$object] to 4_drop_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $3.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(4) Running CREATE table and permissions for [$object] from 4_create_table_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $4.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(5) Running INSERT INTO table from heap for [$object] and UPDATE STATISTICS from 5_copy_from_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $5.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(6) Running CREATE PROC and permissions for procedures schema-bound to [$object] from 6_create_procs_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $6.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
  
Write-Host "(7) Running DROP heap from 7_drop_heap_$schema`_$object.sql"  
$database.ExecuteNonQuery("$(Echo $7.OpenText().ReadToEnd())")  
Write-Host "--done--"  
Write-Host ""  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle ottimizzate per la memoria](memory-optimized-tables.md)  
