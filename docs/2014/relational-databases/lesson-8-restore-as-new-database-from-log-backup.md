---
title: 'Lezione 9: Ripristinare un database da archiviazione di Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 37d8344323add8b9b6f520d59862cdd978823e4f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049766"
---
# <a name="lesson-9-restore-a-database-from-azure-storage"></a>Lezione 9: Ripristinare un database da Archiviazione di Azure
  In questa lezione si apprenderà come ripristinare un file di backup del database da archiviazione di Azure in un database, che si trova in locale o in una macchina virtuale in Azure. È possibile seguire questa lezione anche senza aver completato le lezioni 4, 5, 6, 7 e 8.  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   È stato creato un database nel computer di origine.  
  
-   È stata creata una copia di backup del database (con estensione bak) in archiviazione di Azure usando la funzionalità di [backup e ripristino SQL Server con il servizio di archiviazione BLOB di Azure](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) . Si noti che è necessario creare un'altra credenziale di SQL Server durante questo passaggio. La credenziale usano le chiavi di account di archiviazione.  
  
-   Si ha un account di archiviazione di Azure.  
  
-   È stato creato un contenitore nell'account di archiviazione di Azure.  
  
-   Creazione dei criteri in un contenitore con diritti di lettura, scrittura ed elenco. Generazione di una chiave SAS.  
  
-   È stata creata una credenziale SQL Server nel computer per la funzionalità di integrazione di archiviazione di Azure. Si noti che la credenziale richiede una chiave della la firma di accesso condiviso.  
  
 Per ripristinare un database da archiviazione di Azure, è possibile seguire questa procedura:  
  
1.  Avviare SQL Server Management Studio. Connettersi all'istanza predefinita.  
  
2.  Fare clic su **nuova query** sulla barra degli strumenti standard.  
  
3.  Copiare e incollare il seguente script completo nella finestra Query. Modificare lo script in base alle esigenze.  
  
     **Nota:** Eseguire l' `RESTORE` istruzione per ripristinare il backup del database (con estensione bak) in archiviazione di Azure in un'istanza del database in un altro computer.  
  
    ```sql  
  
    USE master   
    GO   
    -- Create a new database to be backed up.   
    CREATE DATABASE TestDbRestoreFrom;   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO   
    USE TestDbRestoreFrom;   
    GO   
    SELECT * from dbo.Table1;   
    GO   
    -- Create a credential to be used by SQL Server Backup and Restore with Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Azure Storage.   
    BACKUP DATABASE TestDBRestoreFrom    
    TO URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
          WITH CREDENTIAL = 'BackupCredential'    
         ,COMPRESSION   
         ,STATS = 5;   
    GO    
    -- Create a Shared Access Signature credential   
    CREATE CREDENTIAL [https://teststorageaccnt.blob.core.windows.net/testrestorefrom]   
    WITH IDENTITY='SHARED ACCESS SIGNATURE',   
    SECRET = 'sv=2012-02-12&sr=c&si=policy_resfrom&sig=EhVpzLUXjG4ThAMLmVhrnoiCt8IfmD3BsuYiMawGzxc%3D'   
    GO   
    USE master;   
    GO   
    RESTORE DATABASE TestDBRestoreFrom    
    FROM URL = 'https://teststorageaccnt.blob.core.windows.net/testrestorefrom/TestDBRestoreFrom.bak'    
    WITH    
    CREDENTIAL = 'BackupCredential',    
    REPLACE,   
    MOVE 'TestDBRestoreFrom' TO 'C:\Backup\TestDBRestoreFrom.mdf',     
    MOVE 'TestDBRestoreFrom_log' TO 'C:\Backup\TestDBRestoreFrom_log.ldf';   
    GO  
  
    ```  
  
 **Fine dell'esercitazione: SQL Server i file di dati nel servizio di archiviazione di Azure**  
  
  
