---
title: Lezione 8. Ripristinare un database in archiviazione di Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 9e0841c3473baf73033f298cfd3c8402ffc3aa19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743350"
---
# <a name="lesson-8-restore-a-database-to-windows-azure-storage"></a>Lezione 8. ripristinare un database in Archiviazione di Windows Azure
  In questa lezione, verrà illustrato come creare un file di backup in locale e quindi ripristinarlo in Archiviazione di Windows Azure. Si noti che è possibile impostare il database localmente o in una macchina virtuale in Windows Azure. È possibile seguire questa lezione anche senza aver completato le lezioni 4, 5, 6 e 7.  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   Creazione di un account di Archiviazione di Windows Azure.  
  
-   Creazione di un contenitore nell'account di Archiviazione di Windows Azure.  
  
-   Creazione dei criteri in un contenitore con diritti di lettura, scrittura ed elenco. Generazione di una chiave SAS.  
  
-   La credenziale di SQL Server viene creata nel computer di origine in base alla firma di accesso condiviso (SAS, Shared Access Signature).  
  
-   È stato creato un database nel computer di origine.  
  
 Per ripristinare un database in Archiviazione di Windows Azure, è possibile effettuare i passaggi riportati di seguito:  
  
1.  Nel computer di origine, avviare SQL Server Management Studio.  
  
2.  Quando si è connessi al database appena creato, aprire la finestra Query. Eseguire l'istruzione seguente:  
  
    ```sql  
  
    USE TestDB3Restore;   
    GO   
    BACKUP DATABASE TestDB3Restore   
    TO DISK = 'C:\BACKUP\TestDB3Restore.Bak'   
       WITH FORMAT,   
       NAME = 'Full Backup of TestDB3Restore'   
    GO  
  
    ```  
  
3.  Quindi, copiare ed eseguire le istruzioni seguenti nella finestra Query.  
  
    ```sql  
  
    USE master;   
    GO   
    RESTORE DATABASE TestDB3Restore    
    FROM DISK = 'C:\BACKUP\TestDB3Restore.bak'    
    WITH REPLACE,   
    MOVE 'TestDB3Restore' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore.mdf',     
    MOVE 'TestDB3Restore_log' TO 'https://teststorageaccnt.blob.core.windows.net/testcontainrestore/TestDB3Restore_log.ldf';   
    GO  
  
    ```  
  
     Al termine del passaggio, i file di dati (estensione mdf e ldf) vengono elencati nel portale di gestione.  
  
 Per ripristinare un database con file di dati e di log che puntano ad Archiviazione di Windows Azure utilizzando l'interfaccia utente di SQL Server Management Studio, eseguire i passaggi indicati di seguito:  
  
1.  Nelle **Esplora oggetti**, fare clic sul nome del server per espanderne l'albero.  
  
2.  Espandere **database**e selezionare il database.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Ripristina**.  
  
4.  Nel **generali** nella pagina il **ripristinare** sezione di origine, fare clic su **origine** dispositivo.  
  
5.  Fare clic sul pulsante per la **origine** dispositivo casella di testo che consente di aprire il **Seleziona dispositivi di Backup** nella finestra di dialogo.  
  
6.  Nella casella di testo supporti di Backup, selezionare **File**, fare clic sui **Add** pulsante per individuare il file di backup (bak). Fare clic su **OK**.  
  
7.  Fare clic su **file** nella prima pagina.  
  
8.  Nel **Ripristina file di Database** come sezione **Ripristina come** digitare quanto segue:  
  
     Per file di dati, digitare: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`. File di log, digitare: `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. Fare clic su **OK**.  
  
 Una volta eseguito il ripristino, accedere al portale di gestione. È possibile visualizzare i file con estensione mdf e ldf nel contenitore come segue:  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **Lezione successiva:**  
  
 [Lezione 9: Ripristinare un database da Archiviazione di Windows Azure](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
