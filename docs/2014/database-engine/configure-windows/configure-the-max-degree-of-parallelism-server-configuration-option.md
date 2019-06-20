---
title: Configurare l'opzione di configurazione del server max degree of parallelism | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parallel queries [SQL Server]
- processors [SQL Server], parallel queries
- number of processors for parallel queries
- max degree of parallelism option
ms.assetid: 86b65bf1-a6a1-4670-afc0-cdfad1558032
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 46598cf66c80d07383fb033436bbe1792b1eec64
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786942"
---
# <a name="configure-the-max-degree-of-parallelism-server-configuration-option"></a>Configurare l'opzione di configurazione del server max degree of parallelism
  In questo argomento viene descritto come configurare il `max degree of parallelism` opzione di configurazione del server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Quando un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguita in un computer con più microprocessori o CPU, viene automaticamente rilevato il grado di parallelismo migliore, cioè il numero di processori utilizzati per eseguire una singola istruzione per l'esecuzione di ogni piano parallelo. È possibile utilizzare l'opzione `max degree of parallelism` per limitare il numero di processori da utilizzare per l'esecuzione di piani paralleli. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono valutati i piani di esecuzione parallela per le query, le operazioni DDL (Data Definition Language) sugli indici e il popolamento dei cursori statici e gestiti da keyset.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare il max degree of parallelism opzione, utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo aver configurato l'opzione max degree of parallelism](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Se l'opzione affinity mask non è impostata sul valore predefinito, il numero di processori disponibili per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in sistemi SMP (multiprocessori simmetrici, Symmetric Multiprocessor) potrebbe risultare ridotto.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Questa opzione è avanzata e la relativa modifica è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Per consentire al server di determinare il grado massimo di parallelismo, impostare questa opzione su 0, cioè il valore predefinito. L'impostazione di grado massimo di parallelismo su 0 consente a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di utilizzare tutti i processori disponibili fino a un massimo di 64. Per eliminare la generazione di piani paralleli, impostare `max degree of parallelism` su 1. Impostare il valore su un numero compreso tra 1 e 32.767 per specificare il numero massimo di core del processore che può essere utilizzato per l'esecuzione di una singola query. Se il valore è maggiore di quello dei processori disponibili, viene utilizzato il numero effettivo di processori disponibili. Se il computer dispone di un unico processore, il valore di `max degree of parallelism` verrà ignorato.  
  
-   È possibile sostituire il valore di max degree of parallelism nelle query specificando l'hint per la query MAXDOP nell'istruzione per la query. Per altre informazioni, vedere [Hint per la query &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query).  
  
-   Le operazioni tramite cui viene creato o ricompilato un indice o eliminato un indice cluster possono richiedere un elevato utilizzo di risorse. È possibile sostituire il valore di max degree of parallelism per le operazioni sugli indici specificando l'opzione per gli indici MAXDOP nell'istruzione per l'indice. Il valore MAXDOP viene applicato all'istruzione al momento dell'esecuzione e non viene archiviato nei metadati dell'indice. Per altre informazioni, vedere [Configurazione di operazioni parallele sugli indici](../../relational-databases/indexes/configure-parallel-index-operations.md).  
  
-   Oltre al parallelismo delle query e delle operazioni sugli indici, questa opzione controlla anche il parallelismo dei controlli DBCC CHECKTABLE, DBCC CHECKDB e DBCC CHECKFILEGROUP. È possibile disabilitare i piani di esecuzione parallela per queste istruzioni utilizzando il flag di traccia 2528. Per altre informazioni, vedere [Flag di traccia &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>Per configurare l'opzione max degree of parallelism  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Avanzate** .  
  
3.  Nella casella **Max Degree of Parallelism** selezionare il numero massimo di processori da utilizzare nell'esecuzione di piani paralleli.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-configure-the-max-degree-of-parallelism-option"></a>Per configurare l'opzione max degree of parallelism  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si illustra come utilizzare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per configurare l'opzione `max degree of parallelism` su `8`.  
  
```sql  
USE AdventureWorks2012 ;  
GO   
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
EXEC sp_configure 'max degree of parallelism', 8;  
GO  
RECONFIGURE WITH OVERRIDE;  
GO  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione max degree of parallelism  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Opzione di configurazione del server affinity mask](affinity-mask-server-configuration-option.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [DBCC CHECKTABLE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checktable-transact-sql)   
 [DBCC CHECKDB &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkdb-transact-sql)   
 [DBCC CHECKFILEGROUP &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql)   
 [Configurazione di operazioni parallele sugli indici](../../relational-databases/indexes/configure-parallel-index-operations.md)   
 [Hint di query &#40;Transact-SQL&#41;](/sql/t-sql/queries/hints-transact-sql-query)   
 [Impostare le opzioni di indice](../../relational-databases/indexes/set-index-options.md)  
  
  
