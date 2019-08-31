---
title: Lezione 8. Ripristinare un database in archiviazione di Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9f99670-e1de-441e-972c-69faffcac17a
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 5b30a9f60f52b8b19875f5fb3c15242ce2c632fd
ms.sourcegitcommit: 3b1f873f02af8f4e89facc7b25f8993f535061c9
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/30/2019
ms.locfileid: "70175422"
---
# <a name="lesson-8-restore-a-database-to-azure-storage"></a>Lezione 8. Ripristinare un database in Archiviazione di Azure
  In questa lezione verrà illustrato come creare un file di backup in locale e quindi ripristinarlo in archiviazione di Azure. Si noti che è possibile fare in modo che il database sia in locale o in una macchina virtuale in Azure. È possibile seguire questa lezione anche senza aver completato le lezioni 4, 5, 6 e 7.  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   Si ha un account di archiviazione di Azure.  
  
-   È stato creato un contenitore nell'account di archiviazione di Azure.  
  
-   Creazione dei criteri in un contenitore con diritti di lettura, scrittura ed elenco. Generazione di una chiave SAS.  
  
-   La credenziale di SQL Server viene creata nel computer di origine in base alla firma di accesso condiviso (SAS, Shared Access Signature).  
  
-   È stato creato un database nel computer di origine.  
  
 Per ripristinare un database in archiviazione di Azure, è possibile seguire questa procedura:  
  
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
  
 Per ripristinare un database con file di dati e di log che puntano ad archiviazione di Azure usando SQL Server Management Studio interfaccia utente, seguire questa procedura:  
  
1.  In **Esplora oggetti**fare clic sul nome del server per espandere l'albero del server.  
  
2.  Espandere **database**, quindi selezionare il database.  
  
3.  Fare clic con il pulsante destro del mouse sul database, scegliere **Attività**e quindi fare clic su **Ripristina**.  
  
4.  Nella sezione origine **ripristino** della pagina **generale** fare clic su dispositivo di **origine** .  
  
5.  Fare clic sul pulsante Sfoglia per la casella di testo dispositivo di **origine** , che consente di aprire la finestra di dialogo **Seleziona dispositivi di backup** .  
  
6.  Nella casella di testo supporti di backup selezionare **file**, quindi fare clic sul pulsante **Aggiungi** per individuare il file di backup (con estensione bak). Fare clic su **OK**.  
  
7.  Fare clic su **file** nella prima pagina.  
  
8.  Nella sezione **Ripristina file di database** come digitare quanto segue nel campo **Ripristina come** :  
  
     Per file di dati, digitare `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS.mdf`:. Per file di log, digitare `https://teststorageaccnt.blob.core.windows.net/testrestoressms/TestRESSMS_log.ldf`:.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-8.gif "SQL 14 CTP2")  
  
9. Fare clic su **OK**.  
  
 Una volta eseguito il ripristino, accedere al portale di gestione. È possibile visualizzare i file con estensione mdf e ldf nel contenitore come segue:  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-8-9.gif "SQL 14 CTP2")  
  
 **Lezione successiva:**  
  
 [Lezione 9: Ripristinare un database da archiviazione di Azure](../relational-databases/lesson-8-restore-as-new-database-from-log-backup.md)  
  
  
