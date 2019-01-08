---
title: Configurare l'opzione di configurazione del server scan for startup procs | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- scan for startup procs option
ms.assetid: 6bf9d252-e766-458d-9dcd-23d895f032a2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: ccda9c60880bb6864fc411966ab3e410b5008101
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52640843"
---
# <a name="configure-the-scan-for-startup-procs-server-configuration-option"></a>Configurare l'opzione di configurazione del server scan for startup procs
  In questo argomento si illustra come configurare l'opzione di configurazione del server **scan for startup procs** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'opzione **scan for startup procs** è possibile eseguire un'analisi per l'esecuzione automatica di stored procedure all'avvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se l'opzione è impostata su 1, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguita l'analisi e vengono eseguite tutte le stored procedure a esecuzione automatica definite nel server. Il valore predefinito di **scan for startup procs** è 0 (nessuna analisi).  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione scan for startup procs utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo aver configurato l'opzione scan for startup procs](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Questa opzione è avanzata e la relativa modifica è riservata ad amministratori di database esperti o a tecnici dotati di certificazione per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   È possibile impostare il valore dell'opzione usando **sp_configure**. L'opzione viene tuttavia impostata automaticamente se si usa **sp_procoption**, che consente di contrassegnare o meno impostare le stored procedure eseguite automaticamente. Se si usa **sp_procoption** per contrassegnare la prima stored procedure come procedura automatica, l'opzione viene automaticamente impostata su 1. Se si usa **sp_procoption** per annullare il contrassegno dell'ultima stored procedure come procedura automatica, l'opzione viene automaticamente impostata su 0. Se si usa **sp_procoption** per contrassegnare e annullare il contrassegno di procedure automatiche e se si vuole annullare sempre questo contrassegno prima di eliminarle, non è necessario impostare manualmente questa opzione.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-scan-for-startup-procs-option"></a>Per configurare l'opzione scan for startup procs  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server e scegliere **Proprietà**.  
  
2.  Fare clic sul nodo **Avanzate** .  
  
3.  In **Varie**impostare il valore dell'opzione **Analisi per procedure di avvio** su True o False dall'elenco a discesa.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-configure-the-scan-for-startup-procs-option"></a>Per configurare l'opzione scan for startup procs  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**. Questo esempio illustra come usare [sp_configure](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql) per impostare il valore dell'opzione `scan for startup procs` su `1`.  
  
```tsql  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1 ;  
GO  
RECONFIGURE  
GO  
EXEC sp_configure 'scan for startup procs', 1 ;  
GO  
RECONFIGURE  
GO  
  
```  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione scan for startup procs  
 Per poter rendere effettiva l'impostazione, è necessario riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [sp_procoption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-procoption-transact-sql)  
  
  
