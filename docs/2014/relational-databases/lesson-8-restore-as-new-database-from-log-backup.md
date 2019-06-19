---
title: 'Lezione 9: Ripristinare un database da archiviazione di Microsoft Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ebba12c7-3d13-4c9d-8540-ad410a08356d
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 41fbe4cefb6a759befd8b96ded8487ff54b0a1c6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090652"
---
# <a name="lesson-9-restore-a-database-from-windows-azure-storage"></a>Lezione 9: ripristinare un database da Archiviazione di Windows Azure
  In questa lezione verrà illustrato come ripristinare un file di backup del database da Archiviazione di Windows Azure in un database, localmente o in una macchina virtuale di Windows Azure. È possibile seguire questa lezione anche senza aver completato le lezioni 4, 5, 6, 7 e 8.  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   È stato creato un database nel computer di origine.  
  
-   È stato creato un backup del database (con estensione bak) in archiviazione di Azure usando il [Backup e ripristino di SQL Server con il servizio di archiviazione BLOB di Windows Azure](backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) funzionalità. Si noti che è necessario creare un'altra credenziale di SQL Server durante questo passaggio. La credenziale usano le chiavi di account di archiviazione.  
  
-   Creazione di un account di Archiviazione di Windows Azure.  
  
-   Creazione di un contenitore nell'account di Archiviazione di Windows Azure.  
  
-   Creazione dei criteri in un contenitore con diritti di lettura, scrittura ed elenco. Generazione di una chiave SAS.  
  
-   La credenziale di SQL Server viene creata nel computer per la funzionalità Integrazione del servizio di archiviazione Windows Azure. Si noti che la credenziale richiede una chiave della la firma di accesso condiviso.  
  
 Per ripristinare un database da Archiviazione di Windows Azure, è possibile effettuare i passaggi riportati di seguito:  
  
1.  Avviare SQL Server Management Studio. Connettersi all'istanza predefinita.  
  
2.  Fare clic su **nuova Query** sulla barra degli strumenti Standard.  
  
3.  Copiare e incollare il seguente script completo nella finestra Query. Modificare lo script in base alle esigenze.  
  
     **Nota:** Eseguire il `RESTORE` istruzione per ripristinare il backup del database (con estensione bak) in archiviazione di Azure a un'istanza di database in un altro computer.  
  
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
    -- Create a credential to be used by SQL Server Backup and Restore with Windows Azure -----Blob Storage Service.   
    USE master;   
    GO   
    CREATE CREDENTIAL BackupCredential    
    WITH IDENTITY= 'teststorageaccnt',   
    SECRET = 'BO1nH/lWRdnc8TGPlQIXmGLWVCoEa48suYSGiAlC73+S0TX5VXo5/LCm8qiyGCYafDg4ZsueDIV3GQ5RXHaRGw=='    
    GO   
    -- Display the newly created credential   
    SELECT * from sys.credentials   
    -- Create a backup in Windows Azure Storage.   
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
  
 **Fine dell'esercitazione: File di dati di SQL Server nel servizio di archiviazione di Microsoft Azure**  
  
  
