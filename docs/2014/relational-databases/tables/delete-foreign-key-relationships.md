---
title: Eliminare relazioni di chiave esterna | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- foreign keys [SQL Server], deleting
- removing foreign keys
- deleting foreign keys
ms.assetid: 9c9e9ae4-9e03-4137-acb6-b18928a0c4ca
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 919a0c9eb96021ccd7495579cda9756bcdde3194
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62761441"
---
# <a name="delete-foreign-key-relationships"></a>Eliminazione di relazioni di chiave esterna
  È possibile eliminare un vincolo di chiave esterna in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. L'eliminazione di un vincolo di chiave esterna comporta la rimozione del requisito di attivazione dell'integrità referenziale.  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per eliminare un vincolo di chiave esterna utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessario disporre dell'autorizzazione ALTER per la tabella.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-delete-a-foreign-key-constraint"></a>Per eliminare un vincolo di chiave esterna  
  
1.  In **Esplora oggetti**espandere la tabella contenente il vincolo, quindi espandere **Chiavi**.  
  
2.  Fare clic con il pulsante destro del mouse sul vincolo e selezionare **Elimina**.  
  
3.  Nella finestra di dialogo **Elimina oggetto** fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-delete-a-foreign-key-constraint"></a>Per eliminare un vincolo di chiave esterna  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    ALTER TABLE dbo.DocExe   
    DROP CONSTRAINT FK_Column_B;   
    GO  
    ```  
  
 Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
  
