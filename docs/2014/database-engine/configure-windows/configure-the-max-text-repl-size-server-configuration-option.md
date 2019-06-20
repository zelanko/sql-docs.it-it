---
title: Configurare l'opzione di configurazione del server max text repl size | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- max text repl size option
ms.assetid: 3056cf64-621d-4996-9162-3913f6bc6d5b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e55268f499069fb6714aa07944997e1e92e7fc23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62811575"
---
# <a name="configure-the-max-text-repl-size-server-configuration-option"></a>Configurare l'opzione di configurazione del server max text repl size
  In questo argomento si illustra come configurare l'opzione di configurazione del server **max text repl size** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Il **testo repl dimensione massima** opzione specifica la dimensione massima (in byte) della `text`, `ntext`, `varchar(max)`, `nvarchar(max)`, `varbinary(max)`, `xml`, e `image` dati che possono essere aggiunto a una colonna replicata o una colonna acquisita in un'unica istruzione INSERT, UPDATE, WRITETEXT o UPDATETEXT. Il valore predefinito è 65536 byte. Il valore -1 indica che non esiste alcun limite di dimensioni, tranne il limite imposto dal tipo di dati.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione max text repl size tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione max text repl size](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Questa opzione si applica alla replica transazionale e a Change Data Capture. Se un server è configurato sia per la replica transazionale che per Change Data Capture, il valore specificato si applica a entrambe le funzionalità. Questa opzione viene ignorata dalla replica snapshot e da quella di tipo merge.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-max-text-repl-size-option"></a>Per configurare l'opzione max text repl size  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Avanzate** .  
  
3.  Nel gruppo **Varie**impostare il valore desiderato per l'opzione **Dimensioni massime replica testo** .  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-configure-the-max-text-repl-size-option"></a>Per configurare l'opzione max text repl size  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si illustra come utilizzare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per configurare l'opzione `max text repl size` su `-1`.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;   
RECONFIGURE ;   
GO  
EXEC sp_configure 'max text repl size', -1 ;   
GO  
RECONFIGURE;   
GO  
  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione max text repl size  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Replica di SQL Server](../../relational-databases/replication/sql-server-replication.md)   
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)   
 [UPDATETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/updatetext-transact-sql)   
 [WRITETEXT &#40;Transact-SQL&#41;](/sql/t-sql/queries/writetext-transact-sql)  
  
  
