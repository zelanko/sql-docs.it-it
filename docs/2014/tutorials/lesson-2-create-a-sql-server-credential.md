---
title: 'Lezione 2: creare una credenziale di SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
ms.assetid: 64f8805c-1ddc-4c96-a47c-22917d12e1ab
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: baa337d33173f292145d92b60d6192af2a716c5e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "70154333"
---
# <a name="lesson-2-create-a-sql-server-credential"></a>Lezione 2: Creare le credenziali di SQL Server
  **Credenziale:** una credenziale di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è un oggetto usato per archiviare le informazioni di autenticazione necessarie per la connessione a una risorsa all'esterno di SQL Server.  Qui, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] i processi di backup e ripristino usano le credenziali per eseguire l'autenticazione nel servizio di archiviazione BLOB di Azure. Nelle credenziali vengono archiviati il nome dell'account di archiviazione e i relativi valori della **chiave di accesso** . Una volta create, le credenziali devono essere specificate nell'opzione WITH CREDENTIAL durante l'esecuzione delle istruzioni BACKUP/RESTORE. Per altre informazioni su come visualizzare, copiare o rigenerare le **access keys**dell'account di archiviazione, vedere la pagina relativa alle [chiavi di accesso dell'account di archiviazione](https://msdn.microsoft.com/library/windowsazure/hh531566.aspx).  
  
 Per informazioni generali sulle credenziali, vedere [credenziali](../relational-databases/security/authentication-access/credentials-database-engine.md).  
  
 Per informazioni su altri esempi in cui vengono usate le credenziali, vedere [creare un Proxy SQL Server Agent](../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
> [!IMPORTANT]  
>  I requisiti per la creazione di una credenziale SQL Server descritta di seguito sono specifici per i processi di backup SQL Server ([SQL Server backup su URL](../relational-databases/backup-restore/sql-server-backup-to-url.md)e [SQL Server backup gestito in Azure](../relational-databases/backup-restore/sql-server-managed-backup-to-microsoft-azure.md)). Per accedere alla risorsa di archiviazione di Azure, SQL Server usa le informazioni sul nome dell'account di archiviazione e sulla chiave di accesso.  Per altre informazioni sulla creazione delle credenziali per l'archiviazione dei file di database nella risorsa di archiviazione di Azure, vedere [Lesson 3: Create a SQL Server Credential](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="create-a-sql-server-credential"></a>Creare le credenziali di SQL Server  
 Per creare le credenziali di SQL Server, attenersi ai passaggi seguenti:  
  
1.  Connettersi a SQL Server Management Studio.  
  
2.  In Esplora oggetti connettersi all'istanza del motore di database con il database AdventureWorks2012 installato; in alternativa, utilizzare il proprio database da utilizzare per questa esercitazione.  
  
3.  Sulla barra degli strumenti **Standard** fare clic su **Nuova query**.  
  
4.  Copiare e incollare l'esempio seguente nella finestra Query e modificare se necessario.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account (See Lesson 1)   
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account (See Lesson 1)  
  
    ```  
  
     ![Mapping dell'account di archiviazione alle credenziali SQL](../../2014/tutorials/media/backuptocloud-storage-credential-mapping.gif "Mapping dell'account di archiviazione alle credenziali SQL")  
  
5.  Verificare l'istruzione T-SQL e fare clic su **Esegui**.  
  
 Per altre informazioni sul servizio di archiviazione BLOB di Azure per i concetti e i requisiti di backup, vedere [SQL Server backup e ripristino con il servizio di archiviazione BLOB di Azure](../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md).  
  
### <a name="next-lesson"></a>Lezione successiva  
 [Lezione 3: scrivere un backup completo del database nel servizio di archiviazione BLOB di Azure](../../2014/tutorials/lesson-3-write-a-full-database-backup-to-the-windows-azure-blob-storage-service.md).  
  
  
