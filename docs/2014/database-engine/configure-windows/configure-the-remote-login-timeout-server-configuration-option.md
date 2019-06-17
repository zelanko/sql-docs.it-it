---
title: Configurare l'opzione di configurazione del server remote login timeout | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- remote login timeout option
ms.assetid: 077adebe-0e3f-42a5-a75e-5e6d04847e2b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3f2a3a0515674e5a6a5a9e4cb4788ddcf4a37da8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62786950"
---
# <a name="configure-the-remote-login-timeout-server-configuration-option"></a>Configurare l'opzione di configurazione del server remote login timeout
  In questo argomento si illustra come configurare l'opzione di configurazione del server **remote login timeout** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'opzione **remote login timeout** è possibile specificare il numero di secondi che devono trascorrere prima di considerare non riuscito il tentativo di accesso remoto a un server. Se, ad esempio, si tenta l'accesso a un server remoto non funzionante, con **remote login timeout** viene definito un limite oltre il quale i tentativi di accesso verranno sospesi evitando quindi il protrarsi di tentativi inutili per un periodo di tempo indefinito. Il valore predefinito per questa opzione è 10 secondi. Il valore 0 determina un tempo di attesa infinito.  
  
> [!NOTE]  
>  Il valore predefinito per questa opzione è 20 secondi in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione remote login timeout tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione remote login timeout](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   L'opzione **remote login timeout** influisce sulle connessioni ai provider OLE DB stabilite per l'esecuzione di query eterogenee.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-remote-login-timeout-option"></a>Per configurare l'opzione remote login timeout  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Avanzate** .  
  
3.  In **Rete**selezionare un valore per la casella **Remote Login Timeout** .  
  
     Utilizzare l'opzione **remote login timeout** per specificare il numero di secondi che devono trascorrere prima di considerare non riuscito il tentativo di accesso remoto.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-configure-the-remote-login-timeout-option"></a>Per configurare l'opzione remote login timeout  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si illustra come utilizzare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per impostare il valore dell'opzione `remote login timeout` su `35` secondi.  
  
```sql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'remote login timeout', 35 ;  
GO  
RECONFIGURE ;  
GO  
  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione remote login timeout  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
  
