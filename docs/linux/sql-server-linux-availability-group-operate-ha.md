---
title: Funzionamento del gruppo di disponibilità SQL Server in Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: 24a9d3d9ee0fd65b08e30f40a0597eadf47c6b76
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67916045"
---
# <a name="operate-always-on-availability-groups-on-linux"></a>Operare sempre i gruppi di disponibilità in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

## <a name="upgrade-availability-group"></a>Aggiornare il gruppo di disponibilità

Prima di aggiornare un gruppo di disponibilità, esaminare i modelli e procedure consigliate alla [aggiornano le istanze di replica di disponibilità gruppo](../database-engine/availability-groups/windows/upgrading-always-on-availability-group-replica-instances.md).

Le sezioni seguenti illustrano come eseguire un aggiornamento in sequenza con istanze di SQL Server in Linux con gruppi di disponibilità. 

### <a name="upgrade-steps-on-linux"></a>Passaggi di aggiornamento in Linux

Quando le repliche del gruppo disponibilità sono nelle istanze di SQL Server in Linux, il tipo di cluster del gruppo di disponibilità è `EXTERNAL` o `NONE`. Un gruppo di disponibilità gestito da un gestore di cluster diversi da Windows Server Failover Cluster (WSFC) `EXTERNAL`. Pacemaker con Corosync è riportato un esempio di una gestione di cluster external. Dispone di un gruppo di disponibilità con Gestione cluster di nessun tipo di cluster `NONE` i passaggi di aggiornamento indicati in questo documento sono specifici per i gruppi di disponibilità di tipo cluster `EXTERNAL` o `NONE`.

L'ordine in cui si esegue l'aggiornamento di istanze dipende se il proprio ruolo secondario e o meno ospitano le repliche sincrone o asincrone. Aggiornare le istanze di SQL Server che ospitano le repliche secondarie asincrone prima di tutto. Aggiornare quindi le istanze che ospitano le repliche secondarie sincrone. 

   >[!NOTE]
   >Se un gruppo di disponibilità ha solo asincrona repliche, per evitare perdite di dati modifica una replica sincrona e attendere che sia sincronizzato. Eseguire quindi l'aggiornamento di questa replica.
   
Prima di iniziare, eseguire il backup di ogni database.

1. Arrestare la risorsa nel nodo che ospita la replica secondaria di destinazione per l'aggiornamento.
   
   Prima di eseguire il comando di aggiornamento, arrestare la risorsa in modo che il cluster verrà non monitorarlo ed eseguirne il inutilmente. L'esempio seguente aggiunge un vincolo di percorso sul nodo che verrà generato per la risorsa deve essere arrestato. Update `ag_cluster-master` con il nome della risorsa e `nodeName1` con il nodo che ospita la replica di destinazione per l'aggiornamento.

   ```bash
   pcs constraint location ag_cluster-master avoids nodeName1
   ```

1. Aggiornamento di SQL Server nella replica secondaria.

   L'esempio seguente viene aggiornata `mssql-server` e `mssql-server-ha` pacchetti.

   ```bash
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
1. Rimuovere il vincolo di percorso.

   Prima di eseguire il comando di aggiornamento, arrestare la risorsa in modo che il cluster verrà non monitorarlo ed eseguirne il inutilmente. L'esempio seguente aggiunge un vincolo di percorso sul nodo che verrà generato per la risorsa deve essere arrestato. Update `ag_cluster-master` con il nome della risorsa e `nodeName1` con il nodo che ospita la replica di destinazione per l'aggiornamento.

   ```bash
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```
   Come procedura consigliata, assicurarsi che la risorsa viene avviata (tramite `pcs status` comando) e la replica secondaria connessa e sincronizzato lo stato dopo l'aggiornamento.

1. Dopo avere aggiornate tutte le repliche secondarie, eseguire il failover manuale in una delle repliche secondarie sincrone.

   Per i gruppi di disponibilità con `EXTERNAL` tipo di cluster, usare gli strumenti di gestione di cluster per eseguire il failover, gruppi di disponibilità con `NONE` tipo di cluster deve utilizzare Transact-SQL per eseguire il failover. 
   Nell'esempio seguente un gruppo di disponibilità con gli strumenti di Gestione cluster di failover. Sostituire `<targetReplicaName>` con il nome della replica secondaria sincrona che diventerà il database primario:

   ```bash
   sudo pcs resource move ag_cluster-master <targetReplicaName> --master  
   ``` 
   
   >[!IMPORTANT]
   >I passaggi seguenti si applicano solo ai gruppi di disponibilità che non è una gestione del cluster.

   Se il tipo di cluster di gruppo di disponibilità è `NONE`manualmente il failover. Completare i passaggi seguenti nell'ordine indicato:

      a. Il comando seguente imposta la replica primaria a secondaria. Sostituire `AG1` con il nome del gruppo di disponibilità. Eseguire il comando Transact-SQL nell'istanza di SQL Server che ospita la replica primaria.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] SET (ROLE = SECONDARY);
      ```

      b. Il comando seguente imposta una replica secondaria sincrona al sito primario. Eseguire il comando Transact-SQL seguente nell'istanza di destinazione di SQL Server - l'istanza che ospita la replica secondaria sincrona.

      ```transact-sql
      ALTER AVAILABILITY GROUP [ag1] FAILOVER;
      ```

1. Dopo il failover, aggiornare SQL Server nella replica primaria precedente ripetendo la procedura precedente.

   L'esempio seguente viene aggiornata `mssql-server` e `mssql-server-ha` pacchetti.

   ```bash
   # add constraint for the resource to stop on the upgraded node
   # replace 'nodename2' with the name of the cluster node targeted for upgrade
   pcs constraint location ag_cluster-master avoids nodeName2
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```
   
   ```bash
   # upgrade mssql-server and mssql-server-ha packages
   sudo yum update mssql-server
   sudo yum update mssql-server-ha
   ```

   ```bash
   # remove the constraint; make sure the resource is started and replica is connected and synchronized
   pcs constraint remove location-ag_cluster-master-rhel1--INFINITY
   ```

1. Per un gruppi di disponibilità con una gestione di cluster external - in cui il tipo di cluster è EXTERNAL, eliminare il vincolo di percorso che è stato causato dal failover manuale. 

   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```

1. Riprendi spostamento dati per la replica secondaria appena aggiornata - la replica primaria precedente. Questo passaggio è obbligatorio quando un'istanza di versione superiore di SQL Server sta trasferendo i blocchi di log a un'istanza di versione inferiore in un gruppo di disponibilità. Eseguire il comando seguente nella nuova replica secondaria (la replica primaria precedente).

   ```transact-sql
   ALTER DATABASE database_name SET HADR RESUME;
   ```

Dopo l'aggiornamento di tutti i server, è possibile eseguire il failback. Se necessario il failover alla replica primaria originale - back. 

## <a name="drop-an-availability-group"></a>Eliminare un gruppo di disponibilità

Per eliminare un gruppo di disponibilità, eseguire [DROP AVAILABILITY GROUP](../t-sql/statements/drop-availability-group-transact-sql.md). Se il tipo di cluster `EXTERNAL` o `NONE` eseguire il comando in ogni istanza di SQL Server che ospita una replica. Ad esempio, per eliminare un gruppo di disponibilità denominato `group_name` eseguire il comando seguente:

   ```transact-sql
   DROP AVAILABILITY GROUP group_name
   ```
 

## <a name="next-steps"></a>Passaggi successivi

[Configurare Cluster di Red Hat Enterprise Linux per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurare Cluster di SUSE Linux Enterprise Server per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurare Cluster di Ubuntu per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
