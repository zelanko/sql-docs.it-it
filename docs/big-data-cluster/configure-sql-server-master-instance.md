---
title: Configurare l'istanza master di SQL Server
titleSuffix: Configure SQL Server master instance of Big Data Cluster
description: Configurare l'istanza master di un cluster Big Data di SQL Server
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: mihaelab
ms.date: 11/04/2019
ms.topic: overview
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: a124b3a82c75f3da5f7abbdec3b519c86ec7c1c5
ms.sourcegitcommit: 4bba3c8e3360bcbe269819d61f8898d0ad52c6e3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/11/2020
ms.locfileid: "79090518"
---
# <a name="configure-master-instance-of-big-data-clusters-2019"></a>Configurare l'istanza master di [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Configurare l'istanza master di [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)].

Non è possibile configurare le impostazioni di configurazione del server per l'istanza master di SQL Server in fase di distribuzione. Questo articolo descrive una soluzione alternativa temporanea per configurare impostazioni quali l'edizione di SQL Server, l'abilitazione o la disabilitazione di SQL Server Agent, l'abilitazione di flag di traccia specifici o l'abilitazione o la disabilitazione del feedback dei clienti.

Per cambiare una qualsiasi di queste impostazioni, eseguire la procedura seguente:

1. Creare un file `mssql-custom.conf` personalizzato che includa le impostazioni interessate. L'esempio seguente abilita SQL Server Agent e la telemetria, imposta un PID per l'edizione Enterprise e abilita il flag di traccia 1204.

   ```
   [sqlagent]
   enabled=true
   
   [telemetry]
   customerfeedback=true
   userRequestedLocalAuditDirectory = /tmp/audit

   [DEFAULT]
   pid = Enterprise

   [traceflag]
   traceflag0 = 1204
   ```

1. Copiare il file `mssql-custom.conf` in `/var/opt/mssql` nel contenitore `mssql-server` nel pod `master-0`. Sostituire `<namespaceName>` con il nome del cluster Big Data.

   ```bash
   kubectl cp mssql-custom.conf master-0:/var/opt/mssql/mssql-custom.conf -c mssql-server -n <namespaceName>
   ```

1. Riavviare l'istanza di SQL Server.  Sostituire `<namespaceName>` con il nome del cluster Big Data.

   ```bash
   kubectl exec -it master-0  -c mssql-server -n <namespaceName> -- /bin/bash
   supervisorctl restart mssql-server
   exit
   ```

> [!IMPORTANT]
> Se l'istanza master di SQL Server si trova in una configurazione di gruppi di disponibilità, copiare il file di `mssql-custom.conf` in tutti i pod `master`. Si noti che ogni riavvio provocherà un failover. È quindi necessario assicurarsi di pianificare l'esecuzione di questa attività in periodi di inattività.

## <a name="known-limitations"></a>Limitazioni note

- La procedura precedente richiede autorizzazioni di amministratore del cluster Kubernetes
- Non è possibile modificare le regole di confronto del server per l'istanza master di SQL Server del cluster Big Data dopo la distribuzione.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni sulla distribuzione di cluster Big Data di SQL Server, vedere [Introduzione ai cluster Big Data](deploy-get-started.md).