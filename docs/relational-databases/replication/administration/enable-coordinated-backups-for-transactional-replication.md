---
title: Abilitare backup coordinati per la replica transazionale | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- transactional replication, backup and restore
- sp_replicationdboption
- sync with backup [SQL Server replication]
- coordinated backups [SQL Server replication]
- backups [SQL Server replication], transactional replication
ms.assetid: 73a914ba-8b2d-4f4d-ac1b-db9bac676a30
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3e5eeeaa390b4a8607df47ddfd058bc9e1752395
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52524806"
---
# <a name="enable-coordinated-backups-for-transactional-replication"></a>Abilitare backup coordinati per la replica transazionale
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando si attiva la replica transazionale per un database, è possibile specificare che è necessario eseguire il backup di tutte le transazioni prima del recapito al database di distribuzione. È inoltre possibile attivare il backup coordinato nel database di distribuzione. In questo modo, il log delle transazioni per il database di pubblicazione viene troncato solo in seguito al backup delle transazioni propagate al server di distribuzione. Per altre informazioni, vedere [Strategie per il backup e il ripristino della replica snapshot e della replica transazionale](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md).  
  
### <a name="to-enable-coordinated-backups-for-a-database-published-with-transactional-replication"></a>Per attivare i backup coordinati per un database pubblicato con replica transazionale  
  
1.  Nel server di pubblicazione usare la funzione [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) per fare in modo che venga restituita la proprietà **IsSyncWithBackup** del database di pubblicazione. Se la funzione restituisce **1**, i backup coordinati sono già attivati per il database pubblicato.  
  
2.  Se la funzione nel passaggio 1 restituisce **0**, eseguire [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) nel database di pubblicazione nel server di pubblicazione. Specificare un valore di **sync with backup** per **@optname**e **true** per **@value**.  
  
    > [!NOTE]  
    >  Se si modifica l'opzione **sync with backup** in **false**, il punto di troncamento del database di pubblicazione viene aggiornato dopo l'esecuzione dell'agente di lettura log o dopo un intervallo, in caso di esecuzione continua dell'agente di lettura log. L'intervallo massimo è controllato dal parametro dell'agente **-MessageInterval**, la cui impostazione predefinita è pari a 30 secondi.  
  
### <a name="to-enable-coordinated-backups-for-a-distribution-database"></a>Per attivare i backup coordinati per un database di distribuzione  
  
1.  Nel server di distribuzione usare la funzione [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../../t-sql/functions/databasepropertyex-transact-sql.md) per fare in modo che venga restituita la proprietà **IsSyncWithBackup** del database di distribuzione. Se la funzione restituisce **1**, i backup coordinati sono già attivati per il database di distribuzione.  
  
2.  Se la funzione nel passaggio 1 restituisce **0**, eseguire [sp_replicationdboption &#40;Transact-SQL&#41; nel](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) database di pubblicazione nel server di distribuzione. Specificare un valore di **sync with backup** per **@optname** e **true** per **@value**.  
  
### <a name="to-disable-coordinated-backups"></a>Per disabilitare i backup coordinati  
  
1.  Nel database di pubblicazione nel server di pubblicazione o nel database di distribuzione nel server di distribuzione eseguire [sp_replicationdboption &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md). Specificare un valore di **sync with backup** per **@optname** e **false** per **@value**.  
  
  
