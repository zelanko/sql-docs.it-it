---
description: Creazione di un ambiente multiserver
title: Creazione di un ambiente multiserver
ms.custom: seo-lt-2019
ms.date: 01/30/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, multiserver environments
- master servers [SQL Server], about master servers
- target servers [SQL Server], about target servers
- multiserver environments [SQL Server]
ms.assetid: edc2b60d-15da-40a1-8ba3-f1d473366ee6
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 356fb010386f3675a3f62073dacc4cd28cf09e9c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92038284"
---
# <a name="create-a-multiserver-environment"></a>Creazione di un ambiente multiserver
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di database SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

L'amministrazione multiserver richiede l'impostazione di un server master (MSX) e di uno o più server di destinazione (TSX). I processi che verranno eseguiti in tutti i server di destinazione vengono innanzitutto definiti nel server master e quindi scaricati nei server di destinazione.  
  
Per impostazione predefinita, per le connessioni tra server master e server di destinazione sono abilitate la crittografia Transport Layer Security (TLS) completa (denominata in precedenza SSL, Secure Sockets Layer) e la convalida del certificato. Per altre informazioni, vedere [Impostazione delle opzioni di crittografia nei server di destinazione](../../ssms/agent/set-encryption-options-on-target-servers.md).  
  
Se si dispone di un numero elevato di server di destinazione, evitare di definire il server master in un server di produzione con requisiti di prestazioni significativi da altre funzionalità di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , perché il traffico del server di destinazione può rallentare le prestazioni nel server di produzione. Se si inoltrano anche gli eventi a un server master dedicato, è possibile centralizzare l'intera amministrazione in un singolo server. Per altre informazioni, vedere [Gestire eventi](../../ssms/agent/manage-events.md).  
  
> [!NOTE]  
> Per usare l'elaborazione dei processi multiserver, l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve essere membro del ruolo **TargetServersRole** del database **msdb** nel server master. Tramite Configurazione guidata server master l'account del servizio viene automaticamente aggiunto a questo ruolo all'interno del processo di integrazione.  
  
## <a name="considerations-for-multiserver-environments"></a>Considerazioni relative agli ambienti multiserver  
  
Al momento della creazione di un ambiente multiserver, è opportuno considerare i problemi seguenti:  
  
-   Usare la versione più recente come server master. Sono supportate la versione corrente e le due precedenti.

-   Ogni server di destinazione fa riferimento a un solo server master. Per integrare un server di destinazione in un server master diverso, è necessario escluderlo dal server master corrente.  
  
-   Per modificare il nome di un server di destinazione, è necessario escludere il server, modificarne il nome e quindi reintegrarlo dopo la modifica.  
  
-   Per annullare una configurazione multiserver, è necessario escludere tutti i server di destinazione dal server master.  
  
-   SQL Server Integration Services supporta solo server di destinazione la cui versione è uguale o superiore alla versione del server master.  
  
## <a name="related-tasks"></a>Attività correlate  
Negli argomenti seguenti vengono illustrate le attività comuni necessarie per la creazione di un ambiente multiserver.  
  
|Descrizione|Argomento|  
|---------------|---------|  
|Viene illustrato come creare un server master.|[Configurare un server master](../../ssms/agent/make-a-master-server.md)|  
|Viene illustrato come creare un server di destinazione.|[Configurare un server di destinazione](../../ssms/agent/make-a-target-server.md)|  
|Viene illustrato come integrare un server di destinazione in un server master.|[Integrare un server di destinazione in un server master](../../ssms/agent/enlist-a-target-server-to-a-master-server.md)|  
|Viene illustrato come escludere un server di destinazione da un server master.|[Escludere un server di destinazione da un server master](../../ssms/agent/defect-a-target-server-from-a-master-server.md)|  
|Viene illustrato come escludere più server di destinazione da un server master.|[Escludere più server di destinazione da un server master](../../ssms/agent/defect-multiple-target-servers-from-a-master-server.md)|  
|Viene illustrato come verificare lo stato di un server di destinazione.|[sp_help_targetserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)<br /><br />[sp_help_targetservergroup (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)|  
  
## <a name="see-also"></a>Vedere anche  
[Risolvere i problemi relativi a processi multiserver che usano proxy](../../ssms/agent/troubleshoot-multiserver-jobs-that-use-proxies.md)  
