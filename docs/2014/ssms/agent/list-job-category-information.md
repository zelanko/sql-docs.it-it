---
title: Elencare le informazioni sulle categorie di processi | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 0fc668d4-6244-4fef-b90e-62d2c776cd7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dae8f1d98fb1758e9a9802883def1574bda68a78
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "72798213"
---
# <a name="list-job-category-information"></a>Elencare le informazioni sulle categorie di processi
  Come elencare le informazioni sulle categorie [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] di processi [!INCLUDE[tsql](../../includes/tsql-md.md)] in tramite o SQL Server Management Objects.  

  
##  <a name="Security"></a> Sicurezza  
 Per informazioni dettagliate, vedere [Implementazione della sicurezza di SQL Server Agent](implement-sql-server-agent-security.md).  

  
##  <a name="TSQL"></a> Con Transact-SQL  
  
#### <a name="to-list-job-category-information"></a>Per elencare le informazioni sulle categorie di processi  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```sql
    -- returns information about jobs that are administered locally  
    USE msdb ;  
    GO  
  
    EXEC dbo.sp_help_category  
        @type = N'LOCAL' ;  
    GO  
    ```  
  
 Per ulteriori informazioni, vedere [sp_help_category &#40;&#41;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-help-category-transact-sql).  
  
  
##  <a name="SMO"></a>Utilizzo di SQL Server Management Objects  
 **Per elencare le informazioni sulle categorie di processi**  
  
 Usare la classe `JobCategory` tramite il linguaggio di programmazione desiderato, ad esempio Visual Basic, Visual C# o PowerShell. Per ulteriori informazioni, vedere [SQL Server Management Objects &#40;SMO&#41; Programming Guide](../../relational-databases/server-management-objects-smo/sql-server-management-objects-smo-programming-guide.md).  
