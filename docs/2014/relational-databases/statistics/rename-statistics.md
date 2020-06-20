---
title: Rinominare statistiche | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- renaming statistics
- statistics [SQL Server], renaming
ms.assetid: a3bed7b7-3dc5-4b33-b1c6-67c27f573764
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 1528dcec50a662524531065d597b004fe7f59e5f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85060095"
---
# <a name="rename-statistics"></a>Rinominare statistiche
  È possibile rinominare un oggetto statistiche in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Rinominare un oggetto statistiche tramite:**  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
 Per impostazione predefinita, la creazione di un indice comporta la creazione di una statistica per le colonne chiave di tale indice. La ridenominazione automatica dell'indice comporta pertanto la ridenominazione dell'oggetto statistiche e viceversa.  
  
 La modifica di una parte del nome di un oggetto potrebbe compromettere il funzionamento di script e stored procedure. Anziché rinominare l'oggetto statistiche, è consigliabile eliminarlo e ricrearlo con il nuovo nome.  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È richiesta l'autorizzazione ALTER per la tabella o la vista.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
  
#### <a name="to-rename-a-statistics-object"></a>Per rinominare un oggetto statistiche  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_rename N'AK_Employee_LoginID', N'AK_Emp_Login', N'STATISTICS';   
    GO  
    ```  
  
 Per altre informazioni, vedere [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql).  
  
  
