---
title: Gestisci failover gruppo di disponibilità - SQL Server in Linux
description: ''
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
ms.date: 03/01/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: a13f9f3da00889323f3d971ffd801f1fa7d09890
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68027225"
---
# <a name="always-on-availability-group-failover-on-linux"></a>Failover gruppo di disponibilità AlwaysOn in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Nel contesto di un gruppo di disponibilità (AG), il ruolo primario e il ruolo secondario delle repliche di disponibilità sono generalmente intercambiabili in un processo noto come failover. Sono disponibili tre tipi di failover: failover automatico (senza perdita di dati), failover manuale pianificato (senza perdita di dati) e failover manuale forzato (con possibile perdita di dati), in genere chiamato *failover forzato*. Failover manuale automatico e pianificato vengono conservati tutti i dati. Un gruppo di disponibilità di failover a livello di replica di disponibilità. Vale a dire, un gruppo di disponibilità viene eseguito in una delle relative repliche secondarie (la destinazione del failover corrente). 

Per informazioni generali sul failover, vedere [Failover e modalità di failover](../database-engine/availability-groups/windows/failover-and-failover-modes-always-on-availability-groups.md).

## <a name="failover"></a>Failover manuale

Usare gli strumenti di Gestione cluster di failover a un gruppo di disponibilità gestito da un gestore cluster esterno. Ad esempio, se una soluzione Usa Pacemaker per gestire un cluster Linux, usare `pcs` per eseguire i failover manuali in Ubuntu o RHEL. In SLES usare `crm`. 

> [!IMPORTANT]
> In condizioni normali, non eseguire il failover con gli strumenti di gestione di Transact-SQL o SQL Server, ad esempio SQL Server Management Studio o PowerShell. Quando `CLUSTER_TYPE = EXTERNAL`, il jedinou platnou hodnotu Pro `FAILOVER_MODE` è `EXTERNAL`. Con queste impostazioni, tutte le azioni di failover manuale o automatica vengono eseguite dal gestore del cluster esterno. Per istruzioni su come forzare il failover con potenziale perdita di dati, vedere [forzare il failover](#forceFailover).

### <a name="a-namemanualfailovermanual-failover-steps"></a><a name="manualFailover">Passaggi del failover manuale

Per eseguire il failover, la replica secondaria che diventerà la replica primaria deve essere sincrona. Se una replica secondaria è asincrona, [modificare la modalità di disponibilità](../database-engine/availability-groups/windows/change-the-availability-mode-of-an-availability-replica-sql-server.md).

Eseguire il failover manuale in due passaggi.

   Prima di tutto [effettuare manualmente il failover lo spostamento di risorse del gruppo di disponibilità](#manualMove) dal nodo del cluster che è proprietario delle risorse in un nuovo nodo.

   Il cluster di failover della risorsa del gruppo di disponibilità e aggiunge un vincolo di posizione. Questo vincolo consente di configurare la risorsa per l'esecuzione nel nuovo nodo. Per eseguire il failover in futuro, rimuovere il vincolo.

   Secondo, [rimuovere il vincolo di percorso](#removeLocConstraint).

#### <a name="a-namemanualmovestep-1-manually-fail-over-by-moving-availability-group-resource"></a><a name="manualMove">Passaggio 1. Effettuare manualmente il failover lo spostamento di risorsa del gruppo di disponibilità

Per eseguire manualmente il failover una risorsa del gruppo di disponibilità denominata *ag_cluster* al nodo del cluster denominata *nodeName2*, eseguire il comando appropriato per la distribuzione:

- **Esempio RHEL/Ubuntu**

   ```bash
   sudo pcs resource move ag_cluster-master nodeName2 --master
   ```

- **Esempio SLES**

   ```bash
   crm resource migrate ag_cluster nodeName2
   ```

>[!IMPORTANT]
>Dopo il failover manuale su una risorsa, è necessario rimuovere un vincolo di posizione aggiunto automaticamente.

#### <a name="a-nameremovelocconstraint-step-2-remove-the-location-constraint"></a><a name="removeLocConstraint"> Passaggio 2. Rimuovere il vincolo di posizione

Durante un failover manuale, il `pcs` comandi `move` oppure `crm` comando `migrate` aggiunge un vincolo di posizione per la risorsa da inserire nel nuovo nodo di destinazione. Per visualizzare il nuovo vincolo, eseguire il comando seguente dopo aver spostato manualmente la risorsa:

- **Esempio RHEL/Ubuntu**

   ```bash
   sudo pcs constraint list --full
   ```

- **Esempio SLES**

   ```bash
   crm config show
   ```

Un esempio del vincolo che viene creato a causa di un failover manuale. 
 `Enabled on: Node1 (score:INFINITY) (role: Master) (id:cli-prefer-ag_cluster-master)`

- **Esempio RHEL/Ubuntu**

   Nel comando seguente `cli-prefer-ag_cluster-master` è l'ID del vincolo che deve essere rimosso. `sudo pcs constraint list --full` restituisce questo ID. 
   
   ```bash
   sudo pcs constraint remove cli-prefer-ag_cluster-master  
   ```
   
- **Esempio SLES**

   Nel comando seguente `cli-prefer-ms-ag_cluster` è l'ID del vincolo. `crm config show` restituisce questo ID. 
   
   ```bash
   crm configure
   delete cli-prefer-ms-ag_cluster 
   commit
   ```

>[!NOTE]
>Il failover automatico non comporta l'aggiunta di un vincolo di posizione, quindi non è necessaria alcuna operazione di pulizia. 

Per ulteriori informazioni:
- [Red Hat - Managing Cluster Resources](https://access.redhat.com/documentation/Red_Hat_Enterprise_Linux/6/html/Configuring_the_Red_Hat_High_Availability_Add-On_with_Pacemaker/ch-manageresource-HAAR.html) (Red Hat - Gestione di risorse cluster)
- [Pacemaker - spostare manualmente le risorse](https://clusterlabs.org/pacemaker/doc/en-US/Pacemaker/1.1/html/Clusters_from_Scratch/_manually_moving_resources_around_the_cluster.html)
 [Guida all'amministrazione di SLES - risorse](https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha/book_sleha.html#sec.ha.troubleshooting.resource) 
 
## <a name="forceFailover"></a> Forzare il failover 

Un failover forzato è deve essere utilizzato esclusivamente per il ripristino di emergenza. In questo caso, è possibile eseguire il failover con gli strumenti di gestione di cluster perché il Data Center primario è inattivo. Se si forza il failover in una replica secondaria non sincronizzata, è possibile che vengano persi alcuni dati. Forzare il failover solo se è necessario ripristinare il servizio al gruppo di disponibilità immediatamente e sono disposti a rischiare la perdita di dati.

Se è possibile usare gli strumenti di gestione di cluster per l'interazione con il cluster, ad esempio, se il cluster è non risponde a causa di un evento di emergenza nel data center primario, potrebbe essere necessario forzare il failover per ignorare la gestione di cluster external. Questa procedura non è consigliabile per le normali operazioni, perché si rischia di perdita di dati. Usarlo quando gli strumenti di gestione di cluster non riescono a eseguire l'azione di failover. A livello funzionale, questa procedura è simile a [esegue un failover manuale forzato](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md) in un gruppo di disponibilità in Windows.
 
Questo processo per il failover forzato è specifico di SQL Server in Linux.

1. Verificare che la risorsa del gruppo di disponibilità non è gestita dal cluster più. 

      - Impostare la risorsa in modalità non gestita nel nodo del cluster di destinazione. Questo comando segnala l'agente delle risorse alla gestione e monitoraggio delle risorse significative. Ad esempio: 
      
      ```bash
      sudo pcs resource unmanage <resourceName>
      ```

      - Se il tentativo di impostare la modalità di risorse per la modalità non gestita non riesce, eliminare la risorsa. Ad esempio:

      ```bash
      sudo pcs resource delete <resourceName>
      ```

      >[!NOTE]
      >Quando si elimina una risorsa, verranno inoltre eliminati tutti i vincoli associati. 

1. Nell'istanza di SQL Server che ospita la replica secondaria, impostare la variabile di contesto di sessione `external_cluster`.

   ```Transact-SQL
   EXEC sp_set_session_context @key = N'external_cluster', @value = N'yes';
   ```

1. Eseguire il failover del gruppo di disponibilità con Transact-SQL. Nell'esempio seguente, sostituire `<MyAg>` con il nome del gruppo di disponibilità. Connettersi all'istanza di SQL Server che ospita la replica secondaria di destinazione ed eseguire il comando seguente:

   ```Transact-SQL
   ALTER AVAILABILITY GROUP <MyAg> FORCE_FAILOVER_ALLOW_DATA_LOSS;
   ```

1.  Dopo un failover forzato, portare il gruppo di disponibilità in uno stato integro prima di riavviare il monitoraggio delle risorse cluster e la gestione o ricreare la risorsa del gruppo di disponibilità. Rivedere le [attività essenziali dopo un Failover forzato](../database-engine/availability-groups/windows/perform-a-forced-manual-failover-of-an-availability-group-sql-server.md#FollowUp).

1.  Riavviare Gestione e monitoraggio delle risorse cluster:

   Per riavviare la gestione e monitoraggio delle risorse cluster, eseguire il comando seguente:

   ```bash
   sudo pcs resource manage <resourceName>
   sudo pcs resource cleanup <resourceName>
   ```

   Se si elimina la risorsa cluster, è necessario ricrearla. Per ricreare la risorsa cluster, seguire le istruzioni in [creare una risorsa del gruppo di disponibilità](sql-server-linux-availability-group-cluster-rhel.md#create-availability-group-resource).

>[!Important]
>Non usare i passaggi precedenti per le esercitazioni sul ripristino di emergenza perché è il rischio di perdita di dati. Invece di modificare la replica asincrona diventa sincrona e le istruzioni relative [failover manuale normale](#manualFailover).

## <a name="database-level-monitoring-and-failover-trigger"></a>Database trigger a livello di monitoraggio e failover

Per `CLUSTER_TYPE=EXTERNAL`, la semantica di trigger di failover è diversa rispetto al cluster WSFC. Quando il gruppo di disponibilità si trova in un'istanza di SQL Server in un cluster WSFC, la transizione di `ONLINE` sullo stato per il database fa sì che l'integrità del gruppo di disponibilità segnalare un errore. In risposta, la gestione di cluster attiva un'azione di failover. In Linux, l'istanza di SQL Server non può comunicare con il cluster. Il monitoraggio per l'integrità del database viene eseguita *esterno a interno*. Se utente scelto per il monitoraggio di failover a livello di database e failover (impostando l'opzione `DB_FAILOVER=ON` durante la creazione del gruppo di disponibilità), il cluster viene verificato se lo stato del database `ONLINE` ogni volta che esegue un'azione di monitoraggio. Il cluster esegue una query lo stato in `sys.databases`. Per qualsiasi stato diverso da quello `ONLINE`, attiverà un failover automaticamente (se vengono soddisfatte le condizioni di failover automatico). Il tempo effettivo del failover dipende dalla frequenza dell'azione di monitoraggio, nonché lo stato del database in corso l'aggiornamento in sys. Databases.

Il failover automatico richiede almeno una replica sincrona.

## <a name="next-steps"></a>Passaggi successivi

[Configurare Cluster di Red Hat Enterprise Linux per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-rhel.md)

[Configurare Cluster di SUSE Linux Enterprise Server per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-sles.md)

[Configurare Cluster di Ubuntu per le risorse Cluster il gruppo di disponibilità di SQL Server](sql-server-linux-availability-group-cluster-ubuntu.md)
