---
title: Lezione 5. Opzionale Crittografare il database tramite Transparent Data Encryption | Microsoft Docs
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
ms.openlocfilehash: fb9eaf62514b76e35b73ea87b7820751f670a90f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "70175580"
---
# <a name="lesson-5-optional-encrypt-your-database-using-tde"></a>Lezione 5. (facoltativo) crittografare il database tramite TDE
  Come passaggio facoltativo, è possibile crittografare il database appena creato. Transparent Data Encryption (TDE) esegue la crittografia e la decrittografia I/O in tempo reale dei file di dati e di log. Per questo tipo di crittografia viene utilizzata una chiave di crittografia del database (DEK), archiviata nel record di avvio del database affinché sia disponibile durante le operazioni di recupero. Per ulteriori informazioni, vedere [Transparent Data Encryption &#40;&#41;](security/encryption/transparent-data-encryption.md) Transparent Data Encryption e [spostare un database protetto con crittografia transparent in un altro SQL Server](security/encryption/move-a-tde-protected-database-to-another-sql-server.md).  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   Si ha un account di archiviazione di Azure.  
  
-   È stato creato un contenitore nell'account di archiviazione di Azure.  
  
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
  
 Per informazioni dettagliate sulle istruzioni Transact-SQL utilizzate in questa lezione, vedere [create database &#40;SQL Server Transact-sql&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql), [ALTER database &#40;transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql), [CREATE MASTER KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-master-key-transact-sql), [Create Certificate &#40;transact-SQL ](/sql/t-sql/statements/create-certificate-transact-sql)&#41;e [sys. dm_database_encryption_keys &#40;Transact-SQL ](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql)&#41;.  
  
 **Lezione successiva:**  
  
 [Lezione 6: Eseguire la migrazione di un database da un computer di origine locale a un computer di destinazione in Azure](lesson-5-backup-database-using-file-snapshot-backup.md)  
  
  
