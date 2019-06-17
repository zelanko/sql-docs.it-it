---
title: 'Lezione 3: Scrivere un Backup completo del Database al servizio di archiviazione Blob di Azure di Windows | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 454c8296-64e9-46ed-b141-5ebfbc8a4fe2
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 242e32b08ec6346c39e149628e773b33554c95d4
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653685"
---
# <a name="lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>Lezione 3: Scrivere un backup completo del database nel servizio Archiviazione BLOB di Microsoft Azure
  In questa lezione viene illustrato l'utilizzo dell'istruzione tsql per eseguire un backup completo del database nel servizio di archiviazione BLOB di Windows Azure.  
  
## <a name="perform-a-full-database-backup-to-the-windows-azure-blob-storage-service"></a>Eseguire un backup completo del database nel servizio di archiviazione BLOB di Windows Azure  
 Per creare un backup completo del database, attenersi ai passaggi seguenti:  
  
1.  Connettersi a [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
2.  In **Esplora oggetti**connettersi all'istanza di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
3.  Sulla barra del menu Standard fare clic su **Nuova query**.  
  
4.  Copiare e incollare l'esempio seguente nella finestra Query, modificare se necessario, quindi fare clic su **Esegui**.  
  
    ```  
    BACKUP DATABASE[AdventureWorks2012]   
    TO URL = 'https://mystorageaccount.blob.core.windows.net/privatecontainertest/AdventureWorks2012.bak'   
    /* URL includes the endpoint for the BLOB service, followed by the container name, and the name of the backup file*/   
    WITH CREDENTIAL = 'mycredential';  
    /* name of the credential you created in the previous step */   
    GO  
  
    ```  
  
5.  In Esplora oggetti connettersi alla risorsa di archiviazione Azure. Sfogliare per individuare il contenitore e i file di backup appena creati.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 4: Eseguire un ripristino da un Backup completo del Database](../../2014/tutorials/lesson-4-perform-a-restore-from-a-full-database-backup.md).  
  
  
