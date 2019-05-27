---
title: "Lezione 6: Eseguire la migrazione di un database da un'origine del computer locale a una macchina di destinazione in Microsoft Azure | Microsoft Docs"
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: d9134ade-7b03-4c5c-8ed3-3bc369a61691
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1a5787a3f5aecd746ac9aafd5850e6109ebcd999
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090686"
---
# <a name="lesson-6-migrate-a-database-from-a-source-machine-on-premises-to-a-destination-machine-in-windows-azure"></a>Lezione 6: Eseguire la migrazione di un database da un computer di origine locale a un computer di destinazione in Microsoft Azure
  In questa lezione si presuppone che si disponga già di un'altra istanza di SQL Server che potrebbe trovarsi in un altro computer locale o in una macchina virtuale in Windows Azure. Per informazioni su come creare una macchina virtuale SQL Server in Windows Azure, vedere la pagina relativa al [provisioning di una macchina virtuale SQL Server in Windows Azure](http://www.windowsazure.com/manage/windows/common-tasks/install-sql-server/). Dopo aver eseguito il provisioning di una macchina virtuale SQL Server in Windows Azure, verificare che sia possibile connettersi a un'istanza di SQL Server in questa macchina virtuale tramite SQL Server Management Studio presente in un altro computer.  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   Creazione di un account di Archiviazione di Windows Azure.  
  
-   Creazione di un contenitore nell'account di Archiviazione di Windows Azure.  
  
-   Creazione dei criteri in un contenitore con diritti di lettura, scrittura ed elenco. Generazione di una chiave SAS.  
  
-   Creazione di una credenziale di SQL Server nel computer di origine.  
  
-   Creazione di una macchina virtuale SQL Server di destinazione in Windows Azure. È consigliabile crearla selezionando un'immagine della piattaforma che prevede SQL Server 2014.  
  
 Per eseguire la migrazione di un database dall'istanza locale di SQL Server a un'altra macchina virtuale in Windows Azure, è possibile effettuare i passaggi riportati di seguito:  
  
1.  Nel computer di origine, ovvero un computer locale in questa esercitazione, aprire una finestra di query in SQL Server Management Studio. Scollegare il database per spostarlo in un altro computer attenendosi alle istruzioni seguenti:  
  
    ```  
    -- Detach the database in the source machine   
    USE master  
    EXEC sp_detach_db 'TestDB1', 'true';  
    ```  
  
2.  Se è necessario trasferire un database in un computer di destinazione, è necessario innanzitutto prepararlo. Per preparare il computer di destinazione, è necessario innanzitutto creare le credenziale di SQL Server nel computer di destinazione. Se è un database crittografato, è necessario importare il certificato dal computer di origine al computer di destinazione.  
  
    1.  Per creare una credenziale di SQL Server nel computer di destinazione, effettuare i passaggi riportati di seguito:  
  
        1.  Connettersi al computer di destinazione tramite SQL Server Management Studio presente nel computer di origine.  In alternativa, avviare direttamente SQL Server Management Studio nel computer di destinazione.  
  
        2.  Sulla barra degli strumenti Standard fare clic su **Nuova query**.  
  
        3.  Copiare e incollare l'esempio seguente nella finestra Query e modificare se necessario. L'istruzione seguente crea una credenziale di SQL Server per archiviare il certificato di accesso condiviso del contenitore di archiviazione.  
  
            ```sql  
  
            USE master   
            GO   
            CREATE CREDENTIAL [http://teststorageaccnt.blob.core.windows.net/testcontainer]   
            WITH IDENTITY='SHARED ACCESS SIGNATURE',   
            SECRET = 'your SAS key'   
            GO  
  
            ```  
  
        4.  Per visualizzare tutte le credenziali disponibili, è possibile eseguire l'istruzione seguente nella finestra della query:  
  
            ```sql  
            SELECT * from sys.credentials   
            ```  
  
        5.  Una volta connessi a un server di destinazione, aprire la finestra di query ed eseguire:  
  
            ```sql  
  
            -- Create a master key and a server certificate   
            USE master   
            GO   
            CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'MySQLKey01'; -- You may use a different password.   
            GO   
            CREATE CERTIFICATE MySQLCert   
            FROM FILE = 'C:\certs\MySQLCert.CER'   
            WITH PRIVATE KEY   
            (   
            FILE = 'C:\certs\MySQLPrivateKeyFile.PVK',   
            DECRYPTION BY PASSWORD = 'MySQLKey01'   
            );   
            GO  
  
            ```  
  
             Al termine del passaggio, nel computer di destinazione è stato importato il certificato di crittografia di cui è stato eseguito il backup dal computer di origine. Successivamente, è possibile allegare file di dati nel computer di destinazione.  
  
    2.  Quindi si crea un database con i file di dati e di log che puntano ai file esistenti in Archiviazione di Windows Azure utilizzando l'opzione FOR ATTACH. Nella finestra di query, eseguire l'istruzione seguente:  
  
        ```sql  
  
        --Create a database on the destination server   
        CREATE DATABASE TestDB1onDest   
        ON   
        (NAME = TestDB1_data,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf' )   
        LOG ON   
         (NAME = TestDB1_log,   
            FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
        FOR ATTACH   
        GO  
  
        ```  
  
    3.  In Esplora oggetti, fare clic su Database, quindi fare clic con il pulsante destro del mouse su Aggiorna. Sarà possibile vedere nell'elenco il nuovo database creato TestDB1onDest.  
  
    4.  Quindi, nella finestra di query eseguire l'istruzione seguente:  
  
        ```sql  
  
        USE TestDB1onDest   
        SELECT * FROM Table1;   
        GO  
  
        ```  
  
         Vengono elencati tutti i dati immessi nella lezione 4.  
  
 Si noti che il database crittografato è stato trasferito in un'altra istanza di calcolo senza spostamento di dati.  
  
 Per creare un database con file di dati e di log che puntano ai file esistenti in Archiviazione di Windows Azure utilizzando l'interfaccia utente di SQL Server Management Studio, eseguire i passaggi indicati di seguito:  
  
1.  In **Esplora oggetti**connettersi a un'istanza del motore di database di SQL Server e, successivamente, espanderla.  
  
2.  Fare clic con il pulsante destro del mouse su **Database**, quindi scegliere **Nuovo database**. Quindi, fare clic con il pulsante destro del mouse su TestDB1. Fare clic su Attività e quindi su Scollega. Nella finestra di dialogo Scollega, selezionare Interrompi connessioni. Fare clic su **OK**.  
  
3.  Connettersi al computer di destinazione con SQL Server 2014 CTP2 o versione successiva. Per preparare il computer di destinazione, è necessario creare una credenziale di SQL Server nel computer di destinazione che punti allo stesso contenitore in cui è stato inserito TestDB1. Se si intende eseguire il collegamento di nuovo nello stesso computer, non è necessario creare un'altra credenziale.  
  
4.  In **Esplora oggetti**fare clic con il pulsante destro del mouse su **Database** , quindi fare clic su **Collega**.  
  
5.  Nella finestra di dialogo **Collega database** scegliere **Aggiungi**per specificare il database da collegare. Nella finestra di dialogo **Individua file di database** :  
  
     Per percorso di File di dati di Database, digitare: `https://teststorageaccnt.blob.core.windows.net/testcontainer/`.  
  
     Per il nome di File, digitare: `TestDB1Data.mdf`.  
  
6.  Fare clic su **OK**.  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-6-7.gif "SQL 14 CTP2")  
  
 **Lezione successiva:**  
  
 [Lezione 7: Spostare i file di dati in archiviazione di Microsoft Azure](../relational-databases/lesson-6-generate-activity-and-backup-log-using-file-snapshot-backup.md)  
  
  
