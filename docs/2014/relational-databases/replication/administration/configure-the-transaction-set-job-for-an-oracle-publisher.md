---
title: Configurare il processo del Set di transazioni per un server di pubblicazione Oracle (programmazione Transact-SQL della replica) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- sp_publisherproperty
- Oracle publishing [SQL Server replication], configuring
ms.assetid: beea1a5c-0053-4971-a68f-0da53063fcbb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bfa83609f4040fc9875a63217b0e86d6a3ff99bc
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52815043"
---
# <a name="configure-the-transaction-set-job-for-an-oracle-publisher-replication-transact-sql-programming"></a>Configurazione del processo del set di transazioni per un server di pubblicazione Oracle (programmazione Transact-SQL della replica)
  **Xactset** è un processo del database Oracle creato dalla replica eseguita in un server di pubblicazione Oracle per la creazione di set di transazioni, qualora l'agente di lettura log non è connesso al server di pubblicazione. È possibile abilitare e configurare questo processo a livello di programmazione dal server di distribuzione, utilizzando le stored procedure di replica. Per altre informazioni, vedere [Ottimizzazione delle prestazioni per i server di pubblicazione Oracle](../non-sql/performance-tuning-for-oracle-publishers.md).  
  
### <a name="to-enable-the-transaction-set-job"></a>Per abilitare il processo del set di transazioni  
  
1.  Nel server di pubblicazione Oracle impostare il parametro di inizializzazione **job_queue_processes** su un valore sufficiente per consentire l'esecuzione del processo Xactset. Per ulteriori informazioni su questo parametro, vedere la documentazione del database relativa al server di pubblicazione Oracle.  
  
2.  Nel database di distribuzione eseguire [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Specificare il nome del server di pubblicazione Oracle per **@publisher**, un valore di `xactsetbatching` per **@propertyname**e il valore `enabled` per **@propertyvalue**.  
  
3.  Nel database di distribuzione eseguire [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Specificare il nome del server di pubblicazione Oracle per **@publisher**, un valore di `xactsetjobinterval` per **@propertyname**e l'intervallo del processo, espresso in minuti, per **@propertyvalue**.  
  
4.  Nel database di distribuzione eseguire [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Specificare il nome del server di pubblicazione Oracle per **@publisher**, un valore di `xactsetjob` per **@propertyname**e il valore `enabled` per **@propertyvalue**.  
  
### <a name="to-configure-the-transaction-set-job"></a>Per configurare il processo del set di transazioni  
  
1.  (Facoltativo) Nel database di distribuzione eseguire [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Specificare il nome del server di pubblicazione Oracle per **@publisher**. Vengono restituite le proprietà del processo **Xactset** nel server di pubblicazione.  
  
2.  Nel database di distribuzione eseguire [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Specificare il nome del server di pubblicazione Oracle per **@publisher**, il nome della proprietà del processo Xactset impostato per **@propertyname**e la nuova impostazione per **@propertyvalue**.  
  
3.  (Facoltativo) Ripetere il passaggio 2 per ogni proprietà del processo Xactset impostata. Quando si modifica il `xactsetjobinterval` proprietà, è necessario riavviare il processo nel server di pubblicazione Oracle per il nuovo intervallo per rendere effettive.  
  
### <a name="to-view-properties-of-the-transaction-set-job"></a>Per visualizzare le proprietà del processo del set di transazioni  
  
1.  Nel server di distribuzione eseguire [sp_helpxactsetjob](/sql/relational-databases/system-stored-procedures/sp-helpxactsetjob-transact-sql). Specificare il nome del server di pubblicazione Oracle per **@publisher**.  
  
### <a name="to-disable-the-transaction-set-job"></a>Per disabilitare il processo del set di transazioni  
  
1.  Nel database di distribuzione eseguire [sp_publisherproperty &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publisherproperty-transact-sql). Specificare il nome del server di pubblicazione Oracle per **@publisher**, un valore di `xactsetjob` per **@propertyname**e il valore `disabled` per **@propertyvalue**.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene abilitato il processo `Xactset` e viene impostato un intervallo di tre minuti tra le esecuzioni.  
  
 [!code-sql[HowTo#sp_enable_xactsetjob](../../../snippets/tsql/SQL15/replication/howto/tsql/enablexactsetjob.sql#sp_enable_xactsetjob)]  
  
## <a name="see-also"></a>Vedere anche  
 [Ottimizzazione delle prestazioni per i server di pubblicazione Oracle](../non-sql/performance-tuning-for-oracle-publishers.md)   
 [Concetti di base relativi alle stored procedure del sistema di replica](../concepts/replication-system-stored-procedures-concepts.md)  
  
  
