---
title: Configurare la replica di SQL Server in Linux
description: Questo articolo descrive come configurare la replica di SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/20/2018
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.technology: linux
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d7e3f4d81b5b40db2be1e45fbf28d27411492f83
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67895933"
---
# <a name="configure-sql-server-replication-on-linux"></a>Configurare la replica di SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] introduce la replica di SQL Server per le istanze di SQL Server in Linux.

Per informazioni dettagliate sulla replica, vedere [documentazione di SQL Server replica](../relational-databases/replication/sql-server-replication.md).

Configurare la replica in Linux con SQL Server Management Studio (SSMS) o le procedure di Transact-SQL archiviate.

* Per usare SQL Server Management Studio, seguire le istruzioni riportate in questo articolo.

  Usare SSMS in un sistema operativo Windows per connettersi alle istanze di SQL Server. Per e istruzioni, vedere [usare SSMS per gestire SQL Server in Linux](./sql-server-linux-manage-ssms.md).
  
* Per un esempio con le stored procedure, seguire le [replica di configurare SQL Server in Linux](sql-server-linux-replication-tutorial-tsql.md) esercitazione.

## <a name="prerequisites"></a>Prerequisiti

Prima di configurare i server di pubblicazione, i server di distribuzione e sottoscrittori, è necessario completare alcuni passaggi di configurazione per l'istanza di SQL Server.

1. Abilitare SQL Server Agent per usare gli agenti di replica. In tutti i server Linux, eseguire i comandi seguenti nel terminale.

  ```bash
  sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true
  sudo systemctl restart mssql-server
  ```

1. Configurare l'istanza di SQL Server per la replica. Per configurare l'istanza di SQL Server per la replica, eseguire `sys.sp_MSrepl_createdatatypemappings` in tutte le istanze che partecipano alla replica.

  ```sql
  USE msdb
  GO
  exec sys.sp_MSrepl_createdatatypemappings;
  GO
  ```

1. Creare una cartella snapshot. Gli agenti di SQL Server richiedono una cartella di snapshot di lettura/scrittura in. Creare la cartella snapshot nel server di distribuzione.

  Per creare la cartella snapshot e concedere l'accesso a `mssql` utente, eseguire il comando seguente:

  ```bash
  sudo mkdir /var/opt/mssql/data/ReplData/
  sudo chown mssql /var/opt/mssql/data/ReplData/
  sudo chgrp mssql /var/opt/mssql/data/ReplData/
  ```

## <a name="configure-and-monitor-replication-with-sql-server-management-studio-ssms"></a>Configurare e monitorare la replica con SQL Server Management Studio (SSMS)

### <a name="configure-the-distributor"></a>Configurare il server di distribuzione
  
Per configurare il server di distribuzione: 

1. In SQL Server Management Studio connettersi all'istanza di SQL Server in Esplora oggetti.

1. Fare doppio clic su **replica**, fare clic su **configurare la distribuzione...** .

1. Seguire le istruzioni nel **configurazione guidata distribuzione**.

### <a name="create-publication-and-articles"></a>Creare pubblicazioni e articoli

Per creare una pubblicazione e degli articoli:

1. In Esplora oggetti fare clic su **replica** > **pubblicazioni locali**> **nuova pubblicazione...** .

1. Seguire le istruzioni **Creazione guidata nuova pubblicazione** per configurare il tipo di replica e gli articoli che appartengono alla pubblicazione.

### <a name="configure-the-subscription"></a>Configurare la sottoscrizione

Per configurare la sottoscrizione in Esplora oggetti, fare clic su **replica** > **sottoscrizioni locali**> **nuove sottoscrizioni...** .

### <a name="monitor-replication-jobs"></a>Monitorare i processi di replica

Usare Monitoraggio replica per monitorare i processi di replica.

In Esplora oggetti fare doppio clic su **replica**, fare clic su **Avvia monitoraggio replica**.

## <a name="next-steps"></a>Passaggi successivi

[Concetti: Replica di SQL Server in Linux](sql-server-linux-replication.md)

[Stored procedure di replica](../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md).
