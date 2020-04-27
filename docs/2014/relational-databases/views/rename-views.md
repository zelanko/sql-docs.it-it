---
title: Rinominare viste | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- views [SQL Server], renaming
- renaming views
ms.assetid: 5eed0488-81d2-40e8-8fdf-b0a640a591d0
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a0dfa9a95697c4bb1fcb2e4e5d3798f18e305e42
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "68211650"
---
# <a name="rename-views"></a>Rinominare viste
  È possibile rinominare una vista in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!WARNING]  
>  Se si rinomina una vista, è possibile che smettano di funzionare il codice e le applicazioni che dipendono da essa, incluse altre viste, query, stored procedure, funzioni definite dall'utente e applicazioni client. Tali errori inoltre tendono a propagarsi a cascata.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **Per rinominare una vista usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
-   **Completamento:**  [dopo che una vista è stata rinominata](#FollowUp)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Prerequisiti  
 Ottenere un elenco di tutte le dipendenze dalla vista. È necessario modificare qualsiasi oggetto, script o applicazione che fa riferimento alla vista per riflettere il nuovo nome di quest'ultima. Per altre informazioni, vedere [Get Information About a View](get-information-about-a-view.md). Si consiglia di eliminare la vista e di ricrearla con un nuovo nome anziché rinominarla. Se si ricrea la vista, si aggiornano le informazioni sulle dipendenze per gli oggetti a cui viene fatto riferimento nella vista.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Sono richieste l'autorizzazione ALTER per SCHEMA o CONTROL per OBJECT e l'autorizzazione CREATE VIEW per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-rename-a-view"></a>Per rinominare una vista  
  
1.  In **Esplora oggetti**espandere il database contenente la vista da rinominare, quindi espandere la cartella **Vista** .  
  
2.  Fare clic con il pulsante destro del mouse sulla vista da rinominare e scegliere **Rinomina**.  
  
3.  Immettere il nuovo nome della vista.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
 **Per rinominare una vista**  
  
 Nonostante sia possibile usare **sp_rename** per modificare il nome della vista, si consiglia di eliminare quella esistente e di ricrearla con il nuovo nome.  
  
 Per altre informazioni, vedere [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql) e [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql).  
  
##  <a name="follow-up-after-renaming-a-view"></a><a name="FollowUp"></a> Completamento: dopo che una vista è stata rinominata  
 Assicurarsi che tutti gli oggetti, gli script e le applicazioni che fanno riferimento al nome precedente della vista usino ora il nuovo nome.  
  
  
