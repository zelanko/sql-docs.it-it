---
title: Eliminazione degli oggetti di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- deleting database objects
ms.assetid: dbb94fdf-c85b-477b-8e84-f830d259bade
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: a23d307cc33e5b8e59111819b245bc9df1df67df
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63063119"
---
# <a name="deleting-database-objects"></a>Eliminazione degli oggetti di database
  Per rimuovere completamente tutte le tracce di questa esercitazione, è sufficiente eliminare il database. In questo argomento verranno comunque illustrate le procedure per annullare ogni azione eseguita nell'ambito dell'esercitazione.  
  
### <a name="removing-permissions-and-objects"></a>Rimozione di autorizzazioni e oggetti  
  
1.  Prima di eliminare gli oggetti, verificare di trovarsi nel database corretto:  
  
    ```  
    USE TestData;  
    GO  
    ```  
  
2.  Utilizzare l'istruzione `REVOKE` per rimuovere l'autorizzazione di esecuzione per `Mary` sulla stored procedure:  
  
    ```  
    REVOKE EXECUTE ON pr_Names FROM Mary;  
    GO  
  
    ```  
  
3.  Utilizzare l'istruzione `DROP` per rimuovere l'autorizzazione di accesso per `Mary` al database `TestData` :  
  
    ```  
    DROP USER Mary;  
    GO  
  
    ```  
  
4.  Utilizzare l'istruzione `DROP` per rimuovere l'autorizzazione di accesso per `Mary` all'istanza di [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)]:  
  
    ```  
    DROP LOGIN [<computer_name>\Mary];  
    GO  
  
    ```  
  
5.  Utilizzare l'istruzione `DROP` per rimuovere la stored procedure `pr_Names`:  
  
    ```  
    DROP PROC pr_Names;  
    GO  
  
    ```  
  
6.  Utilizzare l'istruzione `DROP` per rimuovere la vista `vw_Names`:  
  
    ```  
    DROP View vw_Names;  
    GO  
  
    ```  
  
7.  Utilizzare l'istruzione `DELETE` per rimuovere tutte le righe della tabella `Products` :  
  
    ```  
    DELETE FROM Products;  
    GO  
  
    ```  
  
8.  Utilizzare l'istruzione `DROP` per rimuovere la tabella `Products` :  
  
    ```  
    DROP Table Products;  
    GO  
  
    ```  
  
9. Non è possibile rimuovere il database `TestData` se è in uso. Passare pertanto a un altro database e quindi utilizzare l'istruzione `DROP` per rimuovere il database `TestData` :  
  
    ```  
    USE MASTER;  
    GO  
    DROP DATABASE TestData;  
    GO  
  
    ```  
  
 In questo modo si conclude l'esercitazione per la scrittura di istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] . Tenere presente che questa esercitazione rappresenta una breve panoramica in cui non vengono descritte tutte le opzioni delle istruzioni utilizzate. La progettazione e la creazione di una struttura di database efficiente e la configurazione dell'accesso sicuro ai dati richiede un database più complesso di quello illustrato in questa esercitazione.  
  
## <a name="return-to-sql-server-tools-portal"></a>Torna al portale degli strumenti di SQL Server  
 [Esercitazione: Scrittura di istruzioni Transact-SQL](tutorial-writing-transact-sql-statements.md)  
  
## <a name="see-also"></a>Vedere anche  
 [REVOKE &#40;Transact-SQL&#41;](/sql/t-sql/statements/revoke-transact-sql)   
 [DROP USER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-user-transact-sql)   
 [DROP LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-login-transact-sql)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-procedure-transact-sql)   
 [DROP VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-view-transact-sql)   
 [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql)   
 [DROP TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-table-transact-sql)   
 [DROP DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-database-audit-specification-transact-sql)  
  
  
