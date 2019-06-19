---
title: Configurare l'opzione di configurazione del server remote query timeout | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- time limit for remote queries [SQL Server]
- remote query timeout option
ms.assetid: 888c8448-933b-41e3-8aa1-c206bc0cdb78
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: a43aff5afdd0d54663aad31e95f0fd528b3b9096
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66802843"
---
# <a name="configure-the-remote-query-timeout-server-configuration-option"></a>Configurare l'opzione di configurazione del server remote query timeout
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento si illustra come configurare l'opzione di configurazione del server **remote query timeout** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'opzione **remote query timeout** è possibile specificare la durata, in secondi, di un'operazione remota prima del timeout di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Il valore predefinito per questa opzione è 600, che consente un'attesa di 10 minuti. Questo valore è applicabile a una connessione in uscita iniziata dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] come query remota e non influisce sulle query ricevute dal [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Per disabilitare il timeout, impostare il valore su 0. Una query rimarrà in attesa finché non verrà completata.  
  
 Per le query eterogenee, **remote query timeout** specifica il numero di secondi di attesa (inizializzati nell'oggetto comando tramite la proprietà del set di righe DBPROP_COMMANDTIMEOUT) di set di risultati da parte del provider remoto. Trascorso il numero di secondi impostato, si verifica il timeout della query. Questo valore è utilizzato anche per l'impostazione di DBPROP_GENERALTIMEOUT, se la proprietà è supportata dal provider remoto. L'impostazione determina il timeout delle altre operazioni dopo il numero di secondi specificato.  
  
 Per le stored procedure remote, con **remote query timeout** è possibile specificare il numero di secondi successivi all'invio di un'istruzione `EXEC` remota, trascorsi i quali si verifica il timeout della stored procedure remota.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti](#Prerequisites)  
  
     [Security](#Security)  
  
-   **Per configurare l'opzione remote query timeout utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione remote query timeout](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario consentire le connessioni a server remoti prima di impostare questo valore.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-remote-query-timeout-option"></a>Per configurare l'opzione remote query timeout  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Connessioni** .  
  
3.  Nella casella **Timeout query remote**di **Connessioni server remoto** digitare o selezionare un valore compreso tra 0 e 2.147.483.647 per impostare il numero massimo di secondi dopo i quali si verifica il timeout di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-configure-the-remote-query-timeout-option"></a>Per configurare l'opzione remote query timeout  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Questo esempio mostra come usare [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) per impostare il valore dell'opzione `remote query timeout` su `0` per disabilitare il timeout.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote query timeout', 0 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione remote query timeout  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Proprietà e comportamenti dei set di righe](../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
