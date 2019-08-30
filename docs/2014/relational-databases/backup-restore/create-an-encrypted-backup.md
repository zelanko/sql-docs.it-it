---
title: Creare un backup crittografato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: e29061d3-c2ab-4d98-b9be-8e90a11d17fe
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b2f16425978b1e6ddc560aabd445b6cfe6737b57
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2019
ms.locfileid: "70154750"
---
# <a name="create-an-encrypted-backup"></a>Creare un backup crittografato
  In questo argomento vengono descritti i passaggi necessari per creare un backup crittografato tramite Transact-SQL.  
  
## <a name="backup-to-disk-with-encryption"></a>Backup su disco con crittografia  
 **Prerequisiti:**  
  
-   Accesso a un disco locale o a uno spazio di archiviazione con una quantità di spazio adeguata per creare un backup del database.  
  
-   Chiave master di un database master e certificato o chiave asimmetrica disponibile nell'istanza di SQL Server. Per le autorizzazioni e i requisiti di crittografia, vedere [Crittografia dei backup](backup-encryption.md).  
  
 Utilizzare i passaggi seguenti per creare un backup crittografato di un database in un disco locale. In questo esempio viene utilizzato un database utente denominato MyTestDB.  
  
1.  **Creare una chiave master del database del database master:** Scegliere una password per la crittografia della copia della chiave master che verrà archiviata nel database. Connettersi al motore di database, avviare una nuova finestra Query e copiare e incollare l'esempio seguente, quindi fare clic su **Esegui**.  
  
    ```  
    -- Creates a database master key.   
    -- The key is encrypted using the password "<master key password>"  
    USE master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
2.  **Creare un certificato di backup:** creare un certificato di backup nel database master. Copiare e incollare l'esempio seguente nella finestra Query e quindi fare clic su **Esegui**.  
  
    ```  
    Use Master  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDB Backup Encryption Certificate';  
    GO  
  
    ```  
  
3.  **Eseguire il backup del database:** specificare l'algoritmo di crittografia e il certificato da usare. Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO DISK = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      COMPRESSION,  
      ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
 Per un esempio di crittografia di un backup protetto da Extensible Key Management, vedere [Extensible Key Management tramite l'insieme di credenziali delle chiavi di Azure &#40;SQL Server&#41;](../security/encryption/extensible-key-management-using-azure-key-vault-sql-server.md).  
  
### <a name="backup-to-azure-storage-with-encryption"></a>Backup in archiviazione di Azure con crittografia  
 Se si sta creando un backup in archiviazione di Azure usando l'opzione **SQL Server Backup to URL** , i passaggi di crittografia sono gli stessi, ma è necessario usare l'URL come destinazione e le credenziali SQL per l'autenticazione nell'archiviazione di Azure. Se si vuole configurare [!INCLUDE[ss_smartbackup](../../includes/ss-smartbackup-md.md)] con le opzioni di crittografia, vedere [configurazione di SQL Server backup gestito in Azure](enable-sql-server-managed-backup-to-microsoft-azure.md) e [configurazione SQL Server backup gestito in Azure per i gruppi di disponibilità](../../database-engine/setting-up-sql-server-managed-backup-to-windows-azure-for-availability-groups.md).  
  
 **Prerequisiti**  
  
-   Account di archiviazione di Windows con contenitore. Per altre informazioni, vedere [Lezione 1: Creare oggetti](../../tutorials/lesson-1-create-windows-azure-storage-objects.md)di archiviazione di Azure.  
  
-   Chiave master di un database master e certificato o chiave asimmetrica nell'istanza di SQL Server. Per le autorizzazioni e i requisiti di crittografia, vedere [Crittografia dei backup](backup-encryption.md).  
  
1.  **Creare credenziali di SQL Server:** per creare le credenziali di SQL Server, connettersi al motore di database, aprire una nuova finestra Query, copiare e incollare l'esempio seguente e quindi fare clic su **Esegui**.  
  
    ```  
    CREATE CREDENTIAL mycredential   
    WITH IDENTITY= 'mystorageaccount' - this is the name of the storage account you specified when creating a storage account    
    , SECRET = '<storage account access key>' - this should be either the Primary or Secondary Access Key for the storage account  
    ```  
  
2.  **Creare una chiave master del database:** Scegliere una password per la crittografia della copia della chiave master che verrà archiviata nel database. Connettersi al motore di database, avviare una nuova finestra Query e copiare e incollare l'esempio seguente, quindi fare clic su **Esegui**.  
  
    ```  
    -- Creates a database master key.  
    -- The key is encrypted using the password "<master key password>"  
    USE Master;  
    GO  
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = '<master key password>';  
    GO  
  
    ```  
  
3.  **Creare un certificato di backup:** creare un certificato di backup nel database master. Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**  
  
    ```  
    USE Master;  
    GO  
    CREATE CERTIFICATE MyTestDBBackupEncryptCert  
       WITH SUBJECT = 'MyTestDBBackupEncryptCert ';  
    GO  
  
    ```  
  
4.  **Eseguire il backup del database:** specificare l'algoritmo di crittografia e il certificato da usare. Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    BACKUP DATABASE [MyTestDB]  
    TO URL = N'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Backup\MyTestDB.bak'  
    WITH  
      CREDENTIAL 'mycredential' - this is the name of the credential created in the first step.  
      ,COMPRESSION  
      ,ENCRYPTION   
       (  
       ALGORITHM = AES_256,  
       SERVER CERTIFICATE = MyTestDBBackupEncryptCert  
       ),  
      STATS = 10  
    GO  
  
    ```  
  
  
