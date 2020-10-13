---
title: Configurare un gruppo di disponibilità Always On di SQL Server in Windows e Linux
description: Informazioni su come creare un gruppo di disponibilità Always On di SQL Server con una replica in un server Windows e una replica in un server Linux.
author: VanMSFT
ms.author: vanto
ms.reviewer: vanto
ms.date: 01/31/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ac19c1c8e0dfc2e8a8cf4711400eb3c5cb29b5f2
ms.sourcegitcommit: 610e3ebe21ac6575850a29641a32f275e71557e3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2020
ms.locfileid: "91784835"
---
# <a name="configure-sql-server-always-on-availability-group-on-windows-and-linux-cross-platform"></a>Configurare un gruppo di disponibilità Always On di SQL Server in Windows e Linux (multipiattaforma)

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/applies-to-version/sqlserver2017.md)]

Questo articolo illustra la procedura da seguire per creare un gruppo di disponibilità Always On con una replica in un server Windows e l'altra replica in un server Linux. Questa è una configurazione multipiattaforma perché le repliche si trovano in sistemi operativi diversi. Usare questa configurazione per la migrazione da una piattaforma all'altra o per il ripristino di emergenza. Questa configurazione non supporta la disponibilità elevata perché non è disponibile una soluzione cluster per gestire una configurazione multipiattaforma. 

![Cluster ibrido di tipo None](./media/sql-server-linux-availability-group-overview/image1.png)

Prima di procedere, è necessario avere familiarità con l'installazione e la configurazione per le istanze di SQL Server in Windows e Linux. 

## <a name="scenario"></a>Scenario

In questo scenario, due server si trovano in sistemi operativi diversi. Un'istanza di Windows Server 2016 denominata `WinSQLInstance` ospita la replica primaria e un server Linux denominato `LinuxSQLInstance` ospita quella secondaria.

## <a name="configure-the-ag"></a>Configurare il gruppo di disponibilità 

La procedura per creare il gruppo di disponibilità è identica a quella adottata per creare un gruppo di disponibilità per i carichi di lavoro con scalabilità in lettura. Il tipo di cluster del gruppo di disponibilità è NONE perché non è presente alcun modulo di gestione cluster. 

   >[!NOTE]
   >Per gli script in questo articolo, le parentesi uncinate `<` e `>` identificano i valori che è necessario sostituire per l'ambiente in uso. Non occorre usare le parentesi uncinate negli script. 

1. Installare SQL Server 2017 in Windows Server 2016, abilitare Gruppi di disponibilità Always On da Gestione configurazione SQL Server e impostare l'autenticazione in modalità mista. 

   >[!TIP]
   >Se si convalida questa soluzione in Azure, posizionare entrambi i server nello stesso set di disponibilità per assicurarsi che siano separati nel data center. 

   **Abilitare i gruppi di disponibilità**

   Per istruzioni, vedere [Abilitare e disabilitare la funzionalità Gruppi di disponibilità Always On (SQL Server)](../database-engine/availability-groups/windows/enable-and-disable-always-on-availability-groups-sql-server.md).

   ![Abilitare i gruppi di disponibilità](./media/sql-server-linux-availability-group-cross-platform/1-sqlserver-configuration-manager.png)

   Gestione configurazione SQL Server rileva che il computer non è un nodo in un cluster di failover. 

   Dopo aver abilitato Gruppi di disponibilità, riavviare SQL Server.

   **Impostare l'autenticazione in modalità mista**

   Per istruzioni, vedere [Modifica della modalità di autenticazione del server](../database-engine/configure-windows/change-server-authentication-mode.md#change-authentication-mode-with-ssms).

1. Installare SQL Server 2017 in Linux. Per istruzioni, vedere [Installare SQL Server](sql-server-linux-setup.md). Abilitare `hadr` tramite mssql-conf.

   Per abilitare `hadr` tramite mssql-conf da un prompt della shell, eseguire il comando seguente:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set hadr.hadrenabled 1
   ```

   Dopo aver abilitato `hadr`, riavviare l'istanza di SQL Server.  

   La figura seguente mostra il passaggio completo.

   ![Abilitare i gruppi di disponibilità Linux](./media/sql-server-linux-availability-group-cross-platform/2-sqlserver-linux-set-hadr.png)

1. Configurare il file hosts in entrambi i server o registrare i nomi dei server con DNS.

1. Aprire le porte del firewall per TPC 1433 e 5022 in Windows e Linux.

1. Nella replica primaria creare un account di accesso al database con la relativa password.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   ```

1. Nella replica primaria creare una chiave master e un certificato e quindi eseguire il backup del certificato con una chiave privata.

   ```sql
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE CERTIFICATE dbm_certificate WITH SUBJECT = 'dbm';
   BACKUP CERTIFICATE dbm_certificate
   TO FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.cer'
   WITH PRIVATE KEY (
           FILE = 'C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\MSSQL\DATA\dbm_certificate.pvk',
           ENCRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
       );
   GO
   ```

1. Copiare il certificato e la chiave privata nel server Linux (replica secondaria) in `/var/opt/mssql/data`. Per copiare i file nel server Linux è possibile usare `pscp`. 

1. Impostare il gruppo e la proprietà della chiave privata e del certificato su `mssql:mssql`.

   Lo script seguente imposta il gruppo e la proprietà dei file. 

   ```bash
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.pvk
   sudo chown mssql:mssql /var/opt/mssql/data/dbm_certificate.cer
   ```

   Nel diagramma seguente la proprietà e il gruppo sono impostati correttamente per il certificato e la chiave.

   ![Abilitare i gruppi di disponibilità Linux](./media/sql-server-linux-availability-group-cross-platform/3-cert-key-owner-group.png)


1. Nella replica secondaria creare un account di accesso al database con la relativa password e creare una chiave master.

   ```sql
   CREATE LOGIN dbm_login WITH PASSWORD = '<C0m9L3xP@55w0rd!>';
   CREATE USER dbm_user FOR LOGIN dbm_login;
   GO
   CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<M@st3rKeyP@55w0rD!>'
   GO
   ```

1. Nella replica secondaria ripristinare il certificato copiato in `/var/opt/mssql/data`. 

   ```sql
   CREATE CERTIFICATE dbm_certificate   
       AUTHORIZATION dbm_user
       FROM FILE = '/var/opt/mssql/data/dbm_certificate.cer'
       WITH PRIVATE KEY (
       FILE = '/var/opt/mssql/data/dbm_certificate.pvk',
       DECRYPTION BY PASSWORD = '<C0m9L3xP@55w0rd!>'
   )
   GO
   ```

1. Nella replica primaria creare un endpoint.

   ```sql
   CREATE ENDPOINT [Hadr_endpoint]
       AS TCP (LISTENER_IP = (0.0.0.0), LISTENER_PORT = 5022)
       FOR DATA_MIRRORING (
           ROLE = ALL,
           AUTHENTICATION = CERTIFICATE dbm_certificate,
           ENCRYPTION = REQUIRED ALGORITHM AES
           );
   ALTER ENDPOINT [Hadr_endpoint] STATE = STARTED;
   GRANT CONNECT ON ENDPOINT::[Hadr_endpoint] TO [dbm_login]
   GO
   ```

   >[!IMPORTANT]
   >Il firewall deve essere aperto per la porta TCP del listener. Nello script precedente la porta è 5022. Usare qualsiasi porta TCP disponibile. 

1. Nella replica secondaria creare l'endpoint. Ripetere lo script precedente nella replica secondaria per creare l'endpoint. 

1. Nella replica primaria creare il gruppo di disponibilità con `CLUSTER_TYPE = NONE`. Lo script di esempio usa `SEEDING_MODE = AUTOMATIC` per creare il gruppo di disponibilità. 

   >[!NOTE]
   >Quando l'istanza di SQL Server in Windows usa percorsi diversi per i file di dati e di log, viene eseguito il failover automatico del seeding nell'istanza di SQL Server in Linux perché questi percorsi non esistono nella replica secondaria. Per usare lo script seguente per un gruppo di disponibilità multipiattaforma, il database richiede lo stesso percorso per i file di dati e di log in Windows Server. In alternativa, è possibile aggiornare lo script con l'impostazione `SEEDING_MODE = MANUAL` e quindi eseguire il backup e il ripristino del database con `NORECOVERY` per il seeding del database. 
   >
   >Questo comportamento si applica alle immagini di Azure Marketplace. 
   >
   >Per altre informazioni sul seeding automatico, vedere [Seeding automatico - Layout dei dischi](../database-engine/availability-groups/windows/automatic-seeding-secondary-replicas.md#disklayout). 

   Prima di eseguire lo script, aggiornare i valori per i gruppi di disponibilità.

      * Sostituire `<WinSQLInstance>` con il nome del server dell'istanza di SQL Server della replica primaria.

      * Sostituire `<LinuxSQLInstance>` con il nome del server dell'istanza di SQL Server della replica secondaria. 

   Per creare il gruppo di disponibilità, aggiornare i valori ed eseguire lo script nella replica primaria.  

   ```sql
   CREATE AVAILABILITY GROUP [ag1]
       WITH (CLUSTER_TYPE = NONE)
       FOR REPLICA ON
           N'<WinSQLInstance>' 
        WITH (
           ENDPOINT_URL = N'tcp://<WinSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
            SEEDING_MODE = AUTOMATIC,
            FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
            ),
           N'<LinuxSQLInstance>' 
       WITH (
            ENDPOINT_URL = N'tcp://<LinuxSQLInstance>:5022',
           AVAILABILITY_MODE = ASYNCHRONOUS_COMMIT,
           SEEDING_MODE = AUTOMATIC,
           FAILOVER_MODE = MANUAL,
           SECONDARY_ROLE (ALLOW_CONNECTIONS = ALL)
           )
   GO
   ```
   
   Per altre informazioni, vedere [CREATE AVAILABILITY GROUP (Transact-SQL)](../t-sql/statements/create-availability-group-transact-sql.md).

1. Nella replica secondaria aggiungere il gruppo di disponibilità.

   ```sql
   ALTER AVAILABILITY GROUP [ag1] JOIN WITH (CLUSTER_TYPE = NONE)
   ALTER AVAILABILITY GROUP [ag1] GRANT CREATE ANY DATABASE
   GO
   ```

1. Creare un database per il gruppo di disponibilità. Nella procedura di esempio viene usato un database denominato `<TestDB>`. Se si usa il seeding automatico, impostare lo stesso percorso per i file di dati e di log. 

   Prima di eseguire lo script, aggiornare i valori per il database.

      * Sostituire `<TestDB>` con il nome del database.

      * Sostituire `<F:\Path>` con il percorso dei file di database e di log. Usare lo stesso percorso per i file di database e di log. 

      È anche possibile usare i percorsi predefiniti. 

    Per creare il database, eseguire lo script. 

   ```sql
   CREATE DATABASE [<TestDB>]
      CONTAINMENT = NONE
     ON  PRIMARY ( NAME = N'<TestDB>', FILENAME = N'<F:\Path>\<TestDB>.mdf')
     LOG ON ( NAME = N'<TestDB>_log', FILENAME = N'<F:\Path>\<TestDB>_log.ldf')
   GO
   ```

1. Eseguire un backup completo del database. 

1. Se non si usa il seeding automatico, ripristinare il database nel server della replica secondaria (Linux). [Eseguire la migrazione di un database di SQL Server da Windows a Linux tramite backup e ripristino](sql-server-linux-migrate-restore-database.md). Ripristinare il database `WITH NORECOVERY` nella replica secondaria. 

1. Aggiungere il database al gruppo di disponibilità. Aggiornare lo script di esempio. Sostituire `<TestDB>` con il nome del database. Nella replica primaria eseguire la query SQL per aggiungere il database al gruppo di disponibilità.

   ```sql
   ALTER AG [ag1] ADD DATABASE <TestDB>
   GO
   ```

1. Verificare che il database venga popolato nella replica secondaria. 

## <a name="fail-over-the-primary-replica"></a>Eseguire il failover della replica primaria

[!INCLUDE[Force failover](../includes/ss-force-failover-read-scale-out.md)]

In questo articolo è stata illustrata la procedura per creare un gruppo di disponibilità multipiattaforma per supportare i carichi di lavoro di migrazione o di scalabilità in lettura. La procedura può essere usata per il ripristino di emergenza manuale. È stato inoltre illustrato come eseguire il failover del gruppo di disponibilità. Un gruppo di disponibilità multipiattaforma usa il tipo di cluster `NONE` e non supporta la disponibilità elevata perché non sono disponibili strumenti per la gestione di cluster su più piattaforme. 

## <a name="next-steps"></a>Passaggi successivi

[Panoramica di Gruppi di disponibilità AlwaysOn](../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)

[Nozioni fondamentali sulla disponibilità di SQL Server per le distribuzioni Linux](sql-server-linux-ha-basics.md)
