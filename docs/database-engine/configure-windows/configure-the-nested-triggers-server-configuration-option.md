---
title: Configurare l'opzione di configurazione del server nested triggers | Microsoft Docs
ms.custom: ''
ms.date: 03/02/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- nested triggers option
ms.assetid: 29d7372b-d406-4a5b-80c6-a2d231d25211
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2ac59b4fb2923aacd377bb974e49dd8edebf5587
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68012500"
---
# <a name="configure-the-nested-triggers-server-configuration-option"></a>Configurare l'opzione di configurazione del server nested triggers
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  In questo argomento si illustra come configurare l'opzione di configurazione del server **nested triggers** in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Con l'opzione **nested triggers** è possibile verificare se è possibile effettuare una sovrapposizione tramite un trigger AFTER, cioè eseguire un'azione con cui viene avviato un altro trigger, mediante il quale a sua volta ne viene avviato un altro e così via. Se l'opzione **nested triggers** è impostata su 0, i trigger AFTER non supportano la propagazione. Se l'opzione **nested triggers** è impostata su 1 (valore predefinito), i trigger AFTER supportano 32 livelli di propagazione. I trigger INSTEAD OF possono essere annidati indipendentemente dall'impostazione di questa opzione.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per configurare l'opzione nested triggers tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [Dopo la configurazione dell'opzione nested triggers](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Le autorizzazioni di esecuzione per **sp_configure** senza alcun parametro o solo con il primo parametro vengono assegnate per impostazione predefinita a tutti gli utenti. Per eseguire **sp_configure** con entrambi i parametri per la modifica di un'opzione di configurazione o per l'esecuzione dell'istruzione RECONFIGURE, a un utente deve essere concessa l'autorizzazione a livello di server ALTER SETTINGS. L'autorizzazione ALTER SETTINGS è assegnata implicitamente ai ruoli predefiniti del server **sysadmin** e **serveradmin** .  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-the-nested-triggers-option"></a>Per configurare l'opzione nested triggers  
  
1.  In **Esplora oggetti**fare clic con il pulsante destro del mouse su un server, quindi scegliere **Proprietà**.  
  
2.  Nella pagina **Avanzate** impostare l'opzione **Consenti attivazione trigger da altri trigger** su **True** (impostazione predefinita) o **False**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-configure-the-nested-triggers-option"></a>Per configurare l'opzione nested triggers  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Questo esempio illustra come usare [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) per impostare il valore dell'opzione `nested triggers` su `0`.  
  
```wmimof  
USE AdventureWorks2012 ;  
GO  
EXEC sp_configure 'show advanced options', 1;  
GO  
RECONFIGURE ;  
GO  
EXEC sp_configure 'nested triggers', 0 ;  
GO  
RECONFIGURE;  
GO  
  
```  
  
 Per altre informazioni, vedere [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)sia installato il servizio WMI.  
  
##  <a name="FollowUp"></a> Completamento: Dopo la configurazione dell'opzione nested triggers  
 L'impostazione diventa effettiva immediatamente senza dover riavviare il server.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di trigger annidati](../../relational-databases/triggers/create-nested-triggers.md)   
 [RECONFIGURE &#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
