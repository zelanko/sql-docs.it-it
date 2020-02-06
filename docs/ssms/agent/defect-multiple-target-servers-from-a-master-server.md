---
title: Escludere più server di destinazione da un server master
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, target servers
- target servers [SQL Server], defecting
- SQL Server Agent jobs, master servers
- master servers [SQL Server], defecting target servers
- defecting target servers
- multiple target server defections
ms.assetid: 61a3713b-403a-4806-bfc4-66db72ca1156
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: dcce797597d2f0ed4700ad17d716d31c49a4cffa
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75254721"
---
# <a name="defect-multiple-target-servers-from-a-master-server"></a>Escludere più server di destinazione da un server master

[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

In questo argomento viene illustrata la procedura per l'esclusione di più server di destinazione da una configurazione di amministrazione multiserver in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Eseguire questa procedura dal server master.  
  
## <a name="SSMSProcedure"></a>Utilizzo di SQL Server Management Studio  
  
#### <a name="to-defect-multiple-target-servers-from-a-master-server"></a>Per escludere più server di destinazione da un server master  
  
1.  In **Esplora oggetti**espandere un server configurato come server master.  
  
2.  Fare clic con il pulsante destro del mouse su **SQL Server Agent**, scegliere **Amministrazione multiserver**e fare clic su **Gestione server di destinazione**.  
  
3.  Fare clic su **Invia istruzioni**e quindi selezionare **Escludi** nell'elenco **Tipo istruzione**.  
  
4.  In **Destinatari**eseguire una delle operazioni seguenti:  
  
    -   Fare clic su **Tutti i server di destinazione** per escludere tutti i server di destinazione di questo server master. Questa opzione consente di disinstallare completamente l'attuale configurazione di amministrazione multiserver.  
  
    -   Fare clic su **Solo i server di destinazione seguenti**e quindi sulla casella **Seleziona** corrispondente per escludere solo alcuni server di destinazione di questo server master.  
  
## <a name="see-also"></a>Vedere anche  
[Creazione di un ambiente multiserver](../../ssms/agent/create-a-multiserver-environment.md)  
[Amministrazione automatizzata in un'organizzazione](../../ssms/agent/automated-administration-across-an-enterprise.md)  
[Escludere un server di destinazione da un server master](../../ssms/agent/defect-a-target-server-from-a-master-server.md)  
  
