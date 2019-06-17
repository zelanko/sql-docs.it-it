---
title: 'Lezione 4: Creare un database in archiviazione di Microsoft Azure | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: a9ae1501-b614-49d3-b975-6569da8350b2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7361cb5d0e68cfa3f45f46d7f99d68c88c1a556b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090817"
---
# <a name="lesson-4-create-a-database-in-windows-azure-storage"></a>Lezione 4: Creare un database in Archiviazione di Microsoft Azure
  In questa lezione verrà illustrato come creare un database tramite la funzionalità relativa ai file di dati di SQL Server in Windows Azure. Si noti che prima di questa lezione, è necessario aver completato le lezioni 1, 2 e 3. La lezione 3 è un passaggio molto importante perché si archiviano le informazioni sul contenitore del servizio di archiviazione Windows Azure e il nome dei criteri e la chiave SAS associati nell'archivio delle credenziali di SQL Server, operazioni necessarie prima della lezione 4.  
  
 Per ogni contenitore di archiviazione utilizzato da un file di dati o di log, è necessario creare una credenziale di SQL Server il cui nome corrisponda al percorso del contenitore. Quindi, è possibile creare un nuovo database in Archiviazione di Windows Azure  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   Creazione di un account di Archiviazione di Windows Azure.  
  
-   Creazione di un contenitore nell'account di Archiviazione di Windows Azure.  
  
-   Creazione dei criteri in un contenitore con diritti di lettura, scrittura ed elenco. Generazione di una chiave SAS.  
  
-   Creazione di una credenziale di SQL Server nel computer di origine.  
  
 Per creare un database in Windows Azure utilizzando la funzionalità relativa ai file di dati di SQL Server nel Servizio archiviazione Windows Azure, effettuare i passaggi riportati di seguito:  
  
1.  Connettersi a SQL Server Management Studio.  
  
2.  In Esplora oggetti connettersi all'istanza del motore di database installato.  
  
3.  Sulla barra degli strumenti Standard fare clic su Nuova query.  
  
4.  Copiare e incollare l'esempio seguente nella finestra Query e modificare se necessario. Si noti che il campo FILENAME fa riferimento al percorso URI del file di database nel contenitore di archiviazione e deve iniziare con HTTPS.  
  
    ```  
  
    --Create a database that uses a SQL Server credential    
    CREATE DATABASE TestDB1    
    ON   
    (NAME = TestDB1_data,   
       FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Data.mdf')   
     LOG ON   
    (NAME = TestDB1_log,   
        FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontainer/TestDB1Log.ldf')   
    GO  
  
    ```  
  
     Aggiungere alcuni dati al database.  
  
    ```  
  
    USE TestDB1;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
5.  Per visualizzare il nuovo TestDB1 nell'istanza locale di SQL Server, aggiornare i database in Esplora oggetti.  
  
6.  Analogamente, per vedere il nuovo database creato nell'account di archiviazione, connettersi all'account di archiviazione tramite SQL Server Management Studio (SSMS). Per informazioni sulla connessione al Servizio di archiviazione Windows Azure utilizzando SQL Server Management Studio, seguire questi passaggi:  
  
    1.  Innanzitutto, ottenere le informazioni sull'account di archiviazione. Accedere al portale di gestione. Successivamente, fare clic su **Archiviazione** e scegliere l'account di archiviazione. Una volta selezionato un account di archiviazione, fare clic su **Gestisci chiavi di accesso** nella parte inferiore della pagina. Verrà aperta una finestra di dialogo simile:  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-1.gif "SQL 14 CTP2")  
  
    2.  Copiare i valori per **Nome account di archiviazione** e **Chiave di accesso primaria** nella finestra di dialogo **Connessione a Servizio di archiviazione Windows Azure** in SSMS. Successivamente, fare clic su **Connetti**. In questo modo le informazioni sui contenitori di account di archiviazione vengono portate in SSMS come illustrato nella schermata seguente:  
  
         ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2.gif "SQL 14 CTP2")  
  
 Nella schermata seguente viene illustrato il nuovo database creato nell'ambiente locale e in quello di Servizio di archiviazione Windows Azure.  
  
 ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-2b.gif "SQL 14 CTP2")  
  
 **Nota:** Se sono presenti riferimenti attivi ai file di dati in un contenitore, qualsiasi tentativo di eliminare la credenziale associata di SQL Server ha esito negativo. Analogamente, se esiste già un lease in un file di database specifico in un BLOB e si desidera eliminarlo, è necessario innanzitutto arrestare il lease nel BLOB. Per interrompere il lease, è possibile usare [Lease Blob](https://msdn.microsoft.com/library/azure/ee691972.aspx).  
  
 Con questa nuova funzionalità, è possibile configurare SQL Server in modo che qualsiasi istruzione CREATE DATABASE imposta come valore predefinito un database abilitato al cloud. È ovvero possibile impostare i percorsi predefiniti di log e dati nelle proprietà dell'istanza di SQL Server Management Studio e quando si crea un database, tutti i file di database (con estensione mdf e ldf) vengono creati come BLOB di pagine in Archiviazione di Windows Azure.  
  
 Per creare un database in Archiviazione di Windows Azure tramite l'interfaccia utente di SQL Server Management Studio, eseguire questi passaggi:  
  
1.  In Esplora oggetti, connettersi a un'istanza del motore di database di SQL Server ed espanderla.  
  
2.  Fare clic con il pulsante destro del mouse su Database, quindi scegliere Nuovo database.  
  
3.  Nella finestra di dialogo Nuovo database digitare un nome di database.  
  
4.  Modificare i valori predefiniti dei file di dati primario e di log delle transazioni, fare clic sulla cella appropriata nella griglia File di database, quindi immettere il nuovo valore. Specificare inoltre il percorso per la posizione del file. Per il percorso, digitare il percorso URL del contenitore di archiviazione, ad esempio `https://teststorageaccnt.blob.core.windows.net/testcontainer/`. Per FileName, digitare i nomi dei file fisici dei file di database (con estensione mdf e ldf).  
  
     ![SQL 14 CTP2](../tutorials/media/ss-was-tutlesson-4-6-4.gif "SQL 14 CTP2")  
  
     Per ulteriori informazioni, vedere [Aggiungere file di dati o file di log a un database](databases/add-data-or-log-files-to-a-database.md).  
  
5.  Mantenere tutti gli altri valori predefiniti.  
  
6.  Fare clic su OK.  
  
 Per visualizzare il nuovo TestDB1 nell'istanza locale di SQL Server, aggiornare i database in Esplora oggetti. Analogamente, per visualizzare il database appena creato nell'account di archiviazione, connettersi all'account di archiviazione tramite SQL Server Management Studio (SSMS) come illustrato precedentemente in questa lezione.  
  
 **Lezione successiva:**  
  
 [Lezione 5. &#40;Facoltativo&#41; crittografare il database tramite Transparent Data Encryption](../relational-databases/lesson-4-restore-database-to-virtual-machine-from-url.md)  
  
  
