---
title: Gestione di un'istanza del cluster di failover - SQL Server in Linux
description: Questo articolo illustra come usare un'istanza del cluster di failover (FCI) SQL Server in Linux.
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: vanto
manager: jroth
ms.date: 08/28/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: ''
ms.openlocfilehash: cc0059f8e8dc43b2c65e432d7cdd56272218d36c
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833147"
---
# <a name="operate-failover-cluster-instance---sql-server-on-linux"></a>Gestione di un'istanza del cluster di failover - SQL Server in Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Questo articolo illustra come usare un'istanza del cluster di failover (FCI) SQL Server in Linux. Se non è stato creato un failover di SQL Server in Linux, vedere [istanza del cluster di failover configura - SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure.md). 

## <a name="failover"></a>Failover

Il failover per le istanze FCI è simile a un cluster di failover di Windows Server (WSFC). Se il nodo del cluster che ospita l'istanza FCI è sottoposto a qualche tipo di errore, l'istanza FCI deve automaticamente il failover a un altro nodo. A differenza di un cluster WSFC, non è possibile impostare i proprietari preferiti, in modo Pacemaker selezioni il nodo che sarà il nuovo host per l'istanza FCI.

Vi sono casi che è possibile eseguire manualmente l'istanza FCI in un altro nodo. Il processo non è analogo a quello di FCI in un cluster WSFC. Per un cluster WSFC, il failover delle risorse a livello di ruolo. In Pacemaker, si sceglie una risorsa da spostare e presupponendo che tutti i vincoli siano corretti, tutto il resto verrà spostata anche. 

La modalità per eseguire il failover dipende dalla distribuzione di Linux. Seguire le istruzioni per la distribuzione di linux.

- [RHEL o Ubuntu](#-manual-failover-rhel-or-ubuntu)
- [SLES](#-manual-failover-sles)

## <a name = "#-manual-failover-rhel-or-ubuntu"></a> Failover manuale (RHEL o Ubuntu)

Per eseguire un failover manuale, bopomofo Red Hat Enterprise Linux (RHEL) o per i server Ubuntu eseguire i passaggi seguenti.
1.  Eseguire il comando seguente: 

   ```bash
   sudo pcs resource move <FCIResourceName> <NewHostNode> 
   ```

   \<FCIResourceName > è il nome di risorsa Pacemaker per il failover di SQL Server.

   \<NewHostNode > è il nome del nodo del cluster che si vuole ospitare l'istanza FCI. 

   Non si otterrà alcun acknowledgement.

2.  Durante un failover manuale, Pacemaker crea un vincolo di percorso per la risorsa che è stato scelto di spostare manualmente. Per visualizzare questo vincolo, eseguire `sudo pcs constraint`.

3.  Dopo aver completato il failover, rimuovere il vincolo eseguendo `sudo pcs resource clear <FCIResourceName>`. 

\<FCIResourceName > è il nome di risorse Pacemaker per l'istanza FCI. 

## <a name = "#-manual-failover-sles"></a> Failover manuale (SLES)


In Suse Linux Enterprise Server (SLES), usare il `migrate` comando per eseguire il failover manuale di un failover di SQL Server. Ad esempio:

```bash
crm resource migrate <FCIResourceName> <NewHostNode>
```

\<FCIResourceName > è il nome di risorse per l'istanza del cluster di failover. 

\<NewHostNode > è il nome del nuovo host di destinazione. 


<!---

|Distribution |Topic 
|----- |-----
|**Red Hat Enterprise Linux with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-red-hat-7-configure.md)<br/>[Operate](sql-server-linux-shared-disk-cluster-red-hat-7-operate.md)
|**SUSE Linux Enterprise Server with HA add-on** |[Configure](sql-server-linux-shared-disk-cluster-sles-configure.md)

--->

## <a name="next-steps"></a>Passaggi successivi

- [Configurare l'istanza del cluster di failover: SQL Server in Linux](sql-server-linux-shared-disk-cluster-configure.md)

<!--Image references-->
