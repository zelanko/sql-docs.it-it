---
title: Lezione 5. (Facoltativo) Crittografare il database tramite Transparent Data Encryption | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ba793c8f-665a-4c46-b68d-f558a37906b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7e78a787a67c430ec82bea4788fd1c92c4c72c4a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090682"
---
# <a name="lesson-5-optional-encrypt-your-database-using-tde"></a>Lezione 5. (facoltativo) crittografare il database tramite TDE
  Come passaggio facoltativo, è possibile crittografare il database appena creato. Transparent Data Encryption (TDE) esegue la crittografia e la decrittografia I/O in tempo reale dei file di dati e di log. Per questo tipo di crittografia viene utilizzata una chiave di crittografia del database (DEK), archiviata nel record di avvio del database affinché sia disponibile durante le operazioni di recupero. Per altre informazioni, vedere [Transparent Data Encryption &#40;Transparent Data Encryption&#41; ](security/encryption/transparent-data-encryption.md) e [spostare un Database protetto con TDE in un altro Server SQL](security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   Creazione di un account di Archiviazione di Windows Azure.  
  
-   Creazione di un contenitore nell'account di Archiviazione di Windows Azure.  
  
-   Creazione dei criteri in un contenitore con diritti di lettura, scrittura ed elenco. Generazione di una chiave SAS.  
  
-   Creazione di una credenziale di SQL Server nel computer di origine.  
  
-   È stato creato un database seguendo i passaggi descritti nella lezione 4.  
  
 Se si desidera crittografare un database, effettuare i passaggi riportati di seguito:  
  
1.  Nel computer di origine modificare ed eseguire le istruzioni seguenti in una finestra di query:  
  
    ```  
  
    -- Create a master key and a server certificate   
    USE master   
    GO   
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01';   
    GO   
    CREATE CERTIFICATE MySQLCert WITH SUBJECT = 'SQL - Azure Storage Certification'   
    GO   
    -- Create a backup of the server certificate in the master database.   
    -- Store TDS certificates in the source machine locally.   
    BACKUP CERTIFICATE MySQLCert   
    TO FILE = 'C:\certs\MySQLCert.CER'   
    WITH PRIVATE KEY   
    (   
    FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
    ENCRYPTION BY PASSWORD = 'MySQLKey01'   
    );  
  
    ```  
  
2.  Quindi, crittografare il nuovo database nel computer di origine eseguendo la procedura seguente:  
  
    ```  
  
    -- Switch to the new database.   
    -- Create a database encryption key, that is protected by the server certificate in the master database.    
    -- Alter the new database to encrypt the database using TDE.   
    USE TestDB1;   
    GO   
    -- Encrypt your database   
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_256   
    ENCRYPTION BY SERVER CERTIFICATE MySQLCert   
    GO   
  
    ALTER DATABASE TestDB1   
    SET ENCRYPTION ON   
    GO  
  
    ```  
  
 Se si desiderano informazioni sullo stato della crittografia di un database e le relative chiavi di crittografia del database associate, eseguire l'istruzione seguente:  
  
```  
  
SELECT * FROM sys.dm_database_encryption_keys;   
GO  
  
```  
  
 Per istruzioni dettagliate informazioni Transact-SQL che sono state usate in questa lezione, vedere [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql), [ALTER DATABASE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql), [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql), [CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql), e [sys.dm_database_ encryption_keys &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql).  
  
 **Lezione successiva:**  
  
 [Lezione 6: Eseguire la migrazione di un database da un'origine del computer locale a una macchina di destinazione in Microsoft Azure](lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
