---
title: Configurare la replica di SQL Server in Linux
description: Questa esercitazione illustra come configurare la replica snapshot SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 9ac898430bbdc3704e43c62be09884ee1925cb75
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130114"
---
# <a name="configure-replication-with-t-sql"></a>Configurare la replica con T-SQL

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)] 

In questa esercitazione si configurerà la replica snapshot SQL Server in Linux con due istanze di SQL Server usando Transact-SQL. Server di pubblicazione e server di distribuzione sarà la stessa istanza, e il sottoscrittore sarà in un'istanza separata.

> [!div class="checklist"]
> * Abilitare gli agenti di replica di SQL Server in Linux
> * Creare un database di esempio
> * Configurare la cartella snapshot per l'accesso degli agenti di SQL Server
> * Configurare il server di distribuzione
> * Configurare il server di pubblicazione
> * Configurare pubblicazioni e articoli
> * Configurare server di sottoscrizione 
> * Eseguire i processi di replica

Tutte le configurazioni di replica possono essere configurate con [stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).

## <a name="prerequisites"></a>Prerequisiti  
Per completare questa esercitazione, è necessario:

- Due istanze di SQL Server con la versione più recente di SQL Server in Linux
- Uno strumento per eseguire T-SQL Query per impostare la replica, ad esempio SQLCMD o SQL Server Management Studio

  Visualizzare [usare SSMS per gestire SQL Server in Linux](./sql-server-linux-manage-ssms.md).

## <a name="detailed-steps"></a>Passaggi dettagliati

1. Abilitare gli agenti di replica di SQL Server in Linux abilitare SQL Server Agent per usare gli agenti di replica. In entrambi i computer host, eseguire i comandi seguenti nel terminale. 

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
  sudo systemctl restart mssql-server
  ```

1. Creare Database di esempio e un tabella nel server di pubblicazione creare un database di esempio e una tabella che verrà utilizzato come gli articoli per una pubblicazione.

  ```sql
  CREATE DATABASE Sales
  GO
  USE [SALES]
  GO 
  CREATE TABLE CUSTOMER([CustomerID] [int] NOT NULL, [SalesAmount] [decimal] NOT NULL)
  GO 
  INSERT INTO CUSTOMER (CustomerID, SalesAmount) VALUES (1,100),(2,200),(3,300)
  ```

  L'altra istanza di SQL Server, nel Sottoscrittore, creare il database per ricevere gli articoli.

  ```sql
  CREATE DATABASE Sales
  GO
  ```

1. Creare la cartella Snapshot per agenti di SQL Server su lettura/scrittura nel server di distribuzione, creare la cartella snapshot e concedere l'accesso all'utente 'mssql' 

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

1. Configurare server di distribuzione In questo esempio, il server di pubblicazione sarà anche il server di distribuzione. Eseguire i comandi seguenti nel server di pubblicazione per configurare l'istanza per la distribuzione oltre.

  ```sql
  DECLARE @distributor AS sysname
  DECLARE @distributorlogin AS sysname
  DECLARE @distributorpassword AS sysname
  -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
  SET @distributor = N'<distributor instance name>'--in this example, it will be the name of the publisher
  SET @distributorlogin = N'<distributor login>'
  SET @distributorpassword = N'<distributor password>'
  -- Specify the distribution database. 
  
  use master
  exec sp_adddistributor @distributor = @distributor -- this should be the hostname

  -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
  exec sp_adddistributiondb @database = N'distribution', @log_file_size = 2, @deletebatchsize_xact = 5000, @deletebatchsize_cmd = 2000, @security_mode = 0, @login = @distributorlogin, @password = @distributorpassword
  GO

  DECLARE @snapshotdirectory AS nvarchar(500)
  SET @snapshotdirectory = N'/var/opt/mssql/data/ReplData/'

  -- Log into distributor and create Distribution Database. In this example, our publisher and distributor is on the same host
  use [distribution] 
  if (not exists (select * from sysobjects where name = 'UIProperties' and type = 'U ')) 
         create table UIProperties(id int) 
  if (exists (select * from ::fn_listextendedproperty('SnapshotFolder', 'user', 'dbo', 'table', 'UIProperties', null, null))) 
         EXEC sp_updateextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties' 
  else 
         EXEC sp_addextendedproperty N'SnapshotFolder', @snapshotdirectory, 'user', dbo, 'table', 'UIProperties'
  GO
  ```

1. Configurare server di pubblicazione eseguire i comandi TSQL seguenti nel server di pubblicazione.

  ```sql
  DECLARE @publisher AS sysname
  DECLARE @distributorlogin AS sysname
  DECLARE @distributorpassword AS sysname
  -- Specify the distributor name. Use 'hostname' command on in terminal to find the hostname
  SET @publisher = N'<instance name>' 
  SET @distributorlogin = N'<distributor login>'
  SET @distributorpassword = N'<distributor password>'
  -- Specify the distribution database. 

  -- Adding the distribution publishers
  exec sp_adddistpublisher @publisher = @publisher, 
  @distribution_db = N'distribution', 
  @security_mode = 0, 
  @login = @distributorlogin, 
  @password = @distributorpassword, 
  @working_directory = N'/var/opt/mssql/data/ReplData', 
  @trusted = N'false', 
  @thirdparty_flag = 0, 
  @publisher_type = N'MSSQLSERVER'
  GO
  ```

1. Configurare i seguenti comandi TSQL di esecuzione del processo di pubblicazione nel server di pubblicazione.

  ```sql
  DECLARE @replicationdb AS sysname
  DECLARE @publisherlogin AS sysname
  DECLARE @publisherpassword AS sysname
  SET @replicationdb = N'Sales'
  SET @publisherlogin = N'<Publisher login>'
  SET @publisherpassword = N'<Publisher Password>'

  use [Sales]
  exec sp_replicationdboption @dbname = N'Sales', @optname = N'publish', @value = N'true'
  
  -- Add the snapshot publication
  exec sp_addpublication 
  @publication = N'SnapshotRepl', 
  @description = N'Snapshot publication of database ''Sales'' from Publisher ''<PUBLISHER HOSTNAME>''.',
  @retention = 0, 
  @allow_push = N'true', 
  @repl_freq = N'snapshot', 
  @status = N'active', 
  @independent_agent = N'true'

  exec sp_addpublication_snapshot @publication = N'SnapshotRepl', 
  @frequency_type = 1, 
  @frequency_interval = 1, 
  @frequency_relative_interval = 1, 
  @frequency_recurrence_factor = 0, 
  @frequency_subday = 8, 
  @frequency_subday_interval = 1, 
  @active_start_time_of_day = 0,
  @active_end_time_of_day = 235959, 
  @active_start_date = 0, 
  @active_end_date = 0, 
  @publisher_security_mode = 0, 
  @publisher_login = @publisherlogin, 
  @publisher_password = @publisherpassword
  ```

1. Creare articoli dalla tabella relativa alle vendite eseguire i comandi TSQL seguenti nel server di pubblicazione.

  ```sql
  use [Sales]
  exec sp_addarticle 
  @publication = N'SnapshotRepl', 
  @article = N'customer', 
  @source_owner = N'dbo', 
  @source_object = N'customer', 
  @type = N'logbased', 
  @description = null, 
  @creation_script = null, 
  @pre_creation_cmd = N'drop', 
  @schema_option = 0x000000000803509D,
  @identityrangemanagementoption = N'manual', 
  @destination_table = N'customer', 
  @destination_owner = N'dbo', 
  @vertical_partition = N'false'
  ```

1. Configura sottoscrizione eseguire i comandi TSQL seguenti nel server di pubblicazione.

  ```sql
  DECLARE @subscriber AS sysname
  DECLARE @subscriber_db AS sysname
  DECLARE @subscriberLogin AS sysname
  DECLARE @subscriberPassword AS sysname
  SET @subscriber = N'<Instance Name>' -- for example, MSSQLSERVER
  SET @subscriber_db = N'Sales'
  SET @subscriberLogin = N'<Subscriber Login>'
  SET @subscriberPassword = N'<Subscriber Password>'

  use [Sales]
  exec sp_addsubscription 
  @publication = N'SnapshotRepl', 
  @subscriber = @subscriber,
  @destination_db = @subscriber_db, 
  @subscription_type = N'Push', 
  @sync_type = N'automatic', 
  @article = N'all', 
  @update_mode = N'read only', 
  @subscriber_type = 0

  exec sp_addpushsubscription_agent 
  @publication = N'SnapshotRepl', 
  @subscriber = @subscriber,
  @subscriber_db = @subscriber_db, 
  @subscriber_security_mode = 0, 
  @subscriber_login =  @subscriberLogin,
  @subscriber_password =  @subscriberPassword,
  @frequency_type = 1,
  @frequency_interval = 0, 
  @frequency_relative_interval = 0, 
  @frequency_recurrence_factor = 0, 
  @frequency_subday = 0, 
  @frequency_subday_interval = 0, 
  @active_start_time_of_day = 0, 
  @active_end_time_of_day = 0, 
  @active_start_date = 0, 
  @active_end_date = 19950101
  GO
  ```

1. Eseguire processi dell'agente di replica

  Eseguire la query seguente per ottenere un elenco di processi:

  ```sql
  SELECT name, date_modified FROM msdb.dbo.sysjobs order by date_modified desc
  ```

  Eseguire il processo di replica Snapshot per generare lo snapshot:

  ```sql
  USE msdb;  
  --generate snapshot of publications, for example
  EXEC dbo.sp_start_job N'PUBLISHER-PUBLICATION-SnapshotRepl-1'
  GO
  ```

  Eseguire il processo di replica Snapshot per generare lo snapshot:

  ```sql
  USE msdb;  
  --distribute the publication to subscriber, for example
  EXEC dbo.sp_start_job N'DISTRIBUTOR-PUBLICATION-SnapshotRepl-SUBSCRIBER'
  GO
  ```

1. Sottoscrittore di connettersi ed eseguire query su dati replicati 

  Nel Sottoscrittore, verificare che la replica sta eseguendo la query seguente:

  ```sql
  SELECT * from [Sales].[dbo].[CUSTOMER]
  ```

In questa esercitazione è stato configurato la replica snapshot SQL Server in Linux con due istanze di SQL Server usando Transact-SQL.

> [!div class="checklist"]
> * Abilitare gli agenti di replica di SQL Server in Linux
> * Creare un database di esempio
> * Configurare la cartella snapshot per l'accesso degli agenti di SQL Server
> * Configurare il server di distribuzione
> * Configurare il server di pubblicazione
> * Configurare pubblicazioni e articoli
> * Configurare server di sottoscrizione 
> * Eseguire i processi di replica

## <a name="see-also"></a>Vedere anche

Per informazioni dettagliate sulla replica, vedere [documentazione di SQL Server replica](../relational-databases/replication/sql-server-replication.md).

## <a name="next-steps"></a>Passaggi successivi

[Concetti: Replica di SQL Server in Linux](sql-server-linux-replication.md)

[Stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).
