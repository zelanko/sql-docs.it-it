---
title: 'Lezione 4: Eseguire un ripristino da un Backup completo del Database | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 580f76e6-9802-4abc-9043-db6de592c733
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 077fb708f09db0182bc5f1510f0264b139beab13
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017092"
---
# <a name="lesson-4-perform-a-restore-from-a-full-database-backup"></a>Lezione 4: Eseguire un ripristino da un Backup completo del Database
  In questa lezione viene illustrato l'utilizzo di un'istruzione tsql per eseguire un ripristino da un backup completo del database creato nella lezione precedente.  
  
## <a name="perform-a-restore-of-a-database-backup"></a>Eseguire un ripristino di un backup del database  
 Per ripristinare un backup completo del database, attenersi ai passaggi seguenti:  
  
1.  Connettersi a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  In **Esplora oggetti**connettersi all'istanza di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
3.  Sulla barra del menu Standard fare clic su **Nuova query**.  
  
4.  Copiare e incollare l'esempio seguente nella finestra Query e modificare se necessario.  
  
    ```  
    RESTORE DATABASE AdventureWorks2012   
    FROM URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    WITH CREDENTIAL = 'mycredential';  
    , STATS = 5 - use this to see monitor the progress  
    GO  
  
    ```  
  
5.  Verificare l'istruzione T-SQL e fare clic su **Esegui**.  
  
### <a name="return-to-tutorials-portal"></a>Ritornare al portale delle esercitazioni  
 [Esercitazione: SQL Server Backup and Restore in Windows Azure Blob Storage Service](../relational-databases/tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md).  
  
  
