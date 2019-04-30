---
title: Configurare le proprietà generali della gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql12.swb.dmf.PolicyManagement.f1
helpviewer_keywords:
- Policy-Based Management, configure properties
ms.assetid: 6d1e0e37-29ea-408a-a055-384984d884be
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 249b338148dc762e091d0be47bc081fe87c72fcd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63162397"
---
# <a name="configure-the-general-properties-of-policy-based-management"></a>Configurare le proprietà generali della gestione basata su criteri
  In questo argomento verrà descritto come configurare le proprietà per la gestione basata su criteri in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per configurare la gestione basata su criteri utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'appartenenza al ruolo predefinito del database PolicyAdministratorRole.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-configure-policy-based-management"></a>Per configurare la gestione basata su criteri  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server in cui configurare le proprietà della gestione basata su criteri.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic con il pulsante destro del mouse su **Gestione criteri** , quindi scegliere **Proprietà**.  
  
     Nella finestra di dialogo **Proprietà Gestione criteri** sono disponibili le opzioni seguenti.  
  
     **Abilitata**  
     Consente di specificare se la gestione basata su criteri è abilitata.  
  
     **HistoryRetentionInDays**  
     Consente di specificare il numero di giorni di conservazione della cronologia di valutazione dei criteri. Se questo valore è pari a 0, ovvero il valore predefinito, la cronologia non verrà rimossa automaticamente.  
  
     **LogOnSuccess**  
     Consente di specificare se vengono registrate le valutazioni di criteri riuscite nella gestione basata su criteri.  
  
    -   Se questo valore corrisponde a false, ovvero il valore predefinito, vengono registrate solo le valutazioni di criteri non riuscite.  
  
    -   Se questo valore corrisponde a true, vengono registrate sia le valutazioni di criteri riuscite che quelle non riuscite.  
  
4.  Al termine, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-configure-policy-based-management"></a>Per configurare la gestione basata su criteri  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    -- enables Policy-Based Management   
    USE msdb;  
    GO  
    EXEC dbo.sp_syspolicy_configure   
         @name = N'Enabled',   
         @value = 1;  
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_syspolicy_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-syspolicy-configure-transact-sql).  
  
  
