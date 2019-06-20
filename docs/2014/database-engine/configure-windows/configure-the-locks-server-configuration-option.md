---
title: Configurare l'opzione di configurazione del server locks | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- locks option [SQL Server]
ms.assetid: b0cf0f86-7652-4574-a9fb-908e10d03973
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 22f47a80a73efc8d462ef8f26f2e6b0fb5b3f3c7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62787212"
---
# <a name="configure-the-locks-server-configuration-option"></a>Configurare l'opzione di configurazione del server locks
  In questo argomento si illustra come configurare l'opzione di configurazione del server **locks** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'opzione **locks** è possibile impostare il numero massimo di blocchi disponibili e pertanto limitare la quantità di memoria utilizzata per i blocchi stessi dal [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . L'impostazione predefinita è 0, che consente al [!INCLUDE[ssDE](../../includes/ssde-md.md)] di allocare e deallocare le strutture di blocco in modo dinamico, in base alle variazioni dei requisiti di sistema.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione locks utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione locks](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Questa opzione è avanzata e la relativa modifica è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Quando si avvia il server con l'opzione **locks** impostata su 0, viene acquisita dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] una quantità di memoria sufficiente per un pool iniziale di 2.500 strutture di blocco tramite Gestione blocchi. Quando il pool di blocchi è esaurito, viene acquisita memoria aggiuntiva per il pool.  
  
     In genere, se per il pool di blocchi è necessaria una quantità di memoria superiore a quella disponibile nel pool di memoria del [!INCLUDE[ssDE](../../includes/ssde-md.md)] ed è disponibile ulteriore memoria del computer, ovvero non è stata raggiunta la soglia **max server memory** , tale memoria viene allocata dinamicamente dal [!INCLUDE[ssDE](../../includes/ssde-md.md)] per soddisfare la richiesta di blocchi. Se tuttavia questa modalità di allocazione di memoria determina il paging a livello del sistema operativo, ad esempio se un'altra applicazione eseguita sul computer in cui si trova l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sta utilizzando la memoria disponibile, lo spazio aggiuntivo per i blocchi non viene allocato. Il pool di blocchi dinamico può acquisire fino al 40% della memoria disponibile per il [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Se il pool di blocchi raggiunge il 60% della memoria acquisita da un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)]oppure se nel computer non è disponibile ulteriore memoria, eventuali richieste aggiuntive di blocchi generano un errore.  
  
     La configurazione consigliata prevede che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzi i blocchi dinamicamente. È tuttavia possibile impostare l'opzione **locks** e impedire l'allocazione dinamica di risorse di blocco da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se l'opzione **locks** è impostata su un valore diverso da 0, il [!INCLUDE[ssDE](../../includes/ssde-md.md)] è in grado di allocare solo il numero di blocchi corrispondente al valore specificato in **locks**. Aumentare tale valore se in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene visualizzato un messaggio indicante che è stato superato il numero di blocchi disponibili. Poiché ogni blocco richiede memoria (96 byte), l'aumento del valore può richiedere anche l'aumento della quantità di memoria destinata al server.  
  
-   L'opzione **locks** influisce inoltre sul momento in cui si verifica l'escalation dei blocchi. Se l'opzione **locks** è impostata su 0, l'escalation dei blocchi si verifica quando la memoria utilizzata dalle strutture di blocco correnti raggiunge il 40% del pool di memoria del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Se l'opzione **locks** è impostata su un valore diverso da 0, l'escalation dei blocchi si verifica quando il numero dei blocchi raggiunge il 40% del valore specificato per l'opzione **locks**.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-locks-option"></a>Per configurare l'opzione locks  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Avanzate** .  
  
3.  Nell'area **Parallelismo**digitare il valore desiderato per l'opzione **locks** .  
  
     L'opzione **locks** consente di impostare il numero massimo di blocchi disponibili e pertanto limitare la quantità di memoria utilizzata per i blocchi stessi da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-configure-the-locks-option"></a>Per configurare l'opzione locks  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Questo esempio mostra come usare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per impostare il valore dell'opzione `locks` su `20000`per poter stabilire il numero di blocchi disponibili a tutti gli utenti.  
  
```sql  
Use AdventureWorks2012 ;  
GO  
sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE;  
GO  
sp_configure 'locks', 20000;  
GO  
RECONFIGURE;  
GO  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione locks  
 Per poter rendere effettiva l'impostazione, è necessario riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
