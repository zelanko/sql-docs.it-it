---
title: Configurare l'opzione di configurazione del server min memory per query | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- memory [SQL Server], queries
- minimum query memory
- queries [SQL Server], memory
- min memory per query option
ms.assetid: ecd3fb79-b4a6-432f-9ef5-530e0d42d5a6
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: dfee7265529419aecf2b05831503ed134b93f525
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62787040"
---
# <a name="configure-the-min-memory-per-query-server-configuration-option"></a>Configurare l'opzione di configurazione del server min memory per query
  In questo argomento viene descritto come configurare `min memory per query` l'opzione di configurazione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del server [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)]tramite o. L' `min memory per query` opzione specifica la quantità minima di memoria (in kilobyte) che verrà allocata per l'esecuzione di una query. Se `min memory per query` , ad esempio, è impostato su 2.048 KB, per la query verrà garantita almeno la quantità di memoria totale. Il valore predefinito è 1024 KB. Il valore minimo è 512 KB mentre quello massimo è 2.147.483.647 KB (2 GB).  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione min memory per query utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [dopo la configurazione dell'opzione min memory per query](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   La quantità di memoria minima per query ha la precedenza sull' [opzione index create memory](configure-the-index-create-memory-server-configuration-option.md). Se si modificano entrambe le opzioni e index create memory è minore di min memory per query, verrà visualizzato un messaggio di avviso, ma il valore risulterà impostato. Durante l'esecuzione delle query verrà visualizzato un altro avviso simile.  
  
###  <a name="Recommendations"></a> Raccomandazioni  
  
-   Questa opzione è avanzata e la relativa modifica è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Con Query Processor di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si tenta di determinare la quantità ottimale di memoria da allocare per una query. L'opzione min memory per query consente all'amministratore di specificare la quantità di memoria minima assegnata a ogni query. In genere la quantità di memoria aumenta se le query comportano operazioni di hashing o di ordinamento per quantità di dati elevate. L'aumento del valore dell'opzione min memory per query può migliorare le prestazioni per alcune query di dimensioni ridotte o medie, ma può provocare una maggiore contesa per le risorse di memoria. L'opzione min memory per query include la memoria allocata per l'ordinamento.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>Per configurare l'opzione min memory per query  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Memoria** .  
  
3.  Nella casella **Memoria minima per le query** immettere la quantità minima di memoria, in kilobyte, che verrà allocata per l'esecuzione di una query.  
  
##  <a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-configure-the-min-memory-per-query-option"></a>Per configurare l'opzione min memory per query  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si illustra come usare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per impostare il valore dell'opzione `min memory per query` su `3500` KB.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'min memory per query', 3500 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
##  <a name="FollowUp"></a>Completamento: dopo la configurazione dell'opzione min memory per query  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [Configurare l'opzione di configurazione del server index create memory](configure-the-index-create-memory-server-configuration-option.md)  
  
  
