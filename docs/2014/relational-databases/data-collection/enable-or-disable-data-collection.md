---
title: Abilitare o disabilitare la raccolta dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- data collector [SQL Server], disabling
- data collector [SQL Server], enabling
ms.assetid: 0137971b-fb48-4a3e-822a-3df2b9bb09d7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 61a5e8c1e3dad99318f14a49f1386757a4ebabe3
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536763"
---
# <a name="enable-or-disable-data-collection"></a>Abilitazione o disabilitazione della raccolta dati
  In questo argomento viene descritto come abilitare o disabilitare una raccolta dati in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per abilitare o disabilitare la raccolta dati utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Per eseguire questa procedura, è necessaria l'appartenenza al ruolo predefinito del database **dc_admin** o **dc_operator** (con autorizzazione EXECUTE).  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-enable-the-data-collector"></a>Per abilitare l'agente di raccolta dati  
  
1.  In Esplora oggetti espandere il nodo **Gestione** .  
  
2.  Fare clic con il pulsante destro del mouse su **Raccolta dati**, quindi scegliere **Abilita raccolta dati**.  
  
#### <a name="to-disable-the-data-collector"></a>Per disabilitare l'agente di raccolta dati  
  
1.  In Esplora oggetti espandere il nodo **Gestione** .  
  
2.  Fare clic con il pulsante destro del mouse su **Raccolta dati**, quindi scegliere **Disabilita raccolta dati**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-enable-the-data-collector"></a>Per abilitare l'agente di raccolta dati  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Questo esempio usa [sp_syscollector_enable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql) per abilitare l'agente di raccolta dati.  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_enable_collector ;  
```  
  
#### <a name="to-disable-the-data-collector"></a>Per disabilitare l'agente di raccolta dati  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Questo esempio usa [sp_syscollector_disable_collector](/sql/relational-databases/system-stored-procedures/sp-syscollector-disable-collector-transact-sql) per disabilitare l'agente di raccolta dati.  
  
```sql  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati](data-collection.md)   
 [Stored procedure di sistema &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/system-stored-procedures-transact-sql)  
  
  
