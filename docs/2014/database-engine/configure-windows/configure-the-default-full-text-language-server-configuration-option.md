---
title: Configurare l'opzione di configurazione del server default full-text language | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- languages [full-text search]
- default full-text language option
ms.assetid: 0fa8785b-0830-4a52-aff5-fcf8268b72fc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d98194f5dead58b738c39503445923d9df49be06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62787067"
---
# <a name="configure-the-default-full-text-language-server-configuration-option"></a>Configurare l'opzione di configurazione del server default full-text language
  In questo argomento viene descritto come configurare `default full-text language` l'opzione di configurazione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del server [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] in [!INCLUDE[tsql](../../includes/tsql-md.md)]tramite o. L' `default full-text language` opzione consente di specificare un valore di lingua predefinito per gli indici full-text. L'analisi linguistica viene eseguita su tutti i dati abilitati per l'indicizzazione full-text e dipende dalla lingua dei dati. Il valore predefinito per questa opzione corrisponde alla lingua impostata per il server. Per una versione localizzata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , il programma `default full-text language` di installazione di imposta l'opzione sulla lingua del server, se esiste una corrispondenza appropriata. Per le versioni non localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], l'opzione `default full-text language` è impostata sull'inglese.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione default full-text language tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione default full-text language](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Il valore dell' `default full-text language` opzione viene utilizzato in un indice full-text quando per una colonna non viene specificata alcuna lingua tramite l'opzione Language **LANGUAGE_TERM** nell'istruzione CREATE FULLTEXT INDEX o ALTER FULLTEXT index. Se l'opzione default full-text language non è supportata o il pacchetto di analisi linguistica non è disponibile, l'operazione CREATE o ALTER non verrà eseguita e in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà restituito un messaggio di errore in cui viene indicato che la lingua specificata non è valida.  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Questa opzione è avanzata e la relativa modifica è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   L' `default full-text language` opzione richiede un valore LCID. Per un elenco di LCID supportati e delle lingue corrispondenti, vedere [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql). Potrebbero essere disponibili altre lingue, ad esempio da fornitori di software indipendenti. Se non viene rilevato alcun sottolinguaggio specifico, il motore di ricerca full-text passerà automaticamente alla lingua principale.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>Per configurare l'opzione default full-text language  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Avanzate** .  
  
3.  In Varie usare l'opzione **Lingua predefinita full-text** per specificare il valore relativo alla lingua predefinita per le colonne con indicizzazione full-text.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-configure-the-default-full-text-language-option"></a>Per configurare l'opzione default full-text language  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Questo esempio illustra come usare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per impostare il valore dell'opzione `default full-text` sull'olandese (`1043`).  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'default full-text language', 1043 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione default full-text language  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [sys.fulltext_languages &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-index-transact-sql)   
 [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-index-transact-sql)  
  
  
