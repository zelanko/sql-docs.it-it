---
title: 'Lezione 7: spostare i file di dati in archiviazione di Azure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 26aa534a-afe7-4a14-b99f-a9184fc699bd
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e31789b1f2cf5b2206af400c7c7798f7761f1e6c
ms.sourcegitcommit: 37a3e2c022c578fc3a54ebee66d9957ff7476922
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2020
ms.locfileid: "82922076"
---
# <a name="lesson-7-move-your-data-files-to-azure-storage"></a>Lezione 7: Spostare i file di dati in Archiviazione di Azure
  In questa lezione verrà illustrato come spostare i file di dati in archiviazione di Azure (ma non nell'istanza di SQL Server). È possibile seguire questa lezione anche senza aver completato le lezioni 4, 5 e 6.  
  
 Per spostare i file di dati in archiviazione di Azure, è possibile usare l' `ALTER DATABASE` istruzione in quanto consente di modificare il percorso dei file di dati.  
  
 Per questa lezione si presuppone che l'utente abbia già completato i passaggi seguenti:  
  
-   Si ha un account di archiviazione di Azure.  
  
-   È stato creato un contenitore nell'account di archiviazione di Azure.  
  
-   Creazione dei criteri in un contenitore con diritti di lettura, scrittura ed elenco. Generazione di una chiave SAS.  
  
-   Creazione di una credenziale di SQL Server nel computer di origine.  
  
 Usare quindi la procedura seguente per spostare i file di dati in archiviazione di Azure:  
  
1.  Innanzitutto, creare un database di prova nel computer di origine e aggiungere alcuni dati.  
  
    ```sql  
  
    USE master;   
    CREATE DATABASE TestDB1Alter;   
    GO   
    USE TestDB1Alter;   
    GO   
    CREATE TABLE Table1 (Col1 int primary key, Col2 varchar(20));   
    GO   
    INSERT INTO Table1 (Col1, Col2) VALUES (1, 'string1'), (2, 'string2');   
    GO  
  
    ```  
  
2.  Eseguire il codice seguente:  
  
    ```sql  
  
    -- In the following statement, modify the path specified in FILENAME to   
    -- the new location of the file in Azure Storage container.   
    ALTER DATABASE TestDB1Alter    
        MODIFY FILE ( NAME = TestDB1Alter,    
                    FILENAME = 'https://teststorageaccnt.blob.core.windows.net/testcontaineralter/TestDB1AlterData.mdf');   
    GO  
  
    ```  
  
3.  Quando si esegue questa operazione, viene visualizzato il messaggio seguente: "il file" TestDB1Alter "è stato modificato nel catalogo di sistema. Il nuovo percorso verrà utilizzato al successivo avvio del database ".  
  
4.  Quindi, impostare il database come offline.  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET OFFLINE;   
    GO  
  
    ```  
  
5.  A questo punto, è necessario copiare i file di dati in archiviazione di Azure usando uno dei metodi seguenti: [strumento AzCopy](https://docs.microsoft.com/archive/blogs/windowsazurestorage/azcopy-uploadingdownloading-files-for-windows-azure-blobs), [pagina put](https://msdn.microsoft.com/library/azure/ee691975.aspx), informazioni di [riferimento sulla libreria client di archiviazione](https://msdn.microsoft.com/library/azure/dn261237.aspx)o uno strumento di esplorazione di archiviazione di terze parti.  
  
     **Importante:** Quando si usa questa nuova funzionalità avanzata, assicurarsi sempre di creare un BLOB di pagine e non un BLOB in blocchi.  
  
6.  Quindi, impostare il database come online.  
  
    ```sql  
  
    ALTER DATABASE TestDB1Alter SET ONLINE;   
    GO  
  
    ```  
  
 **Lezione successiva:**  
  
 [Lezione 8. Ripristinare un database in archiviazione di Azure](lesson-7-restore-a-database-to-a-point-in-time.md)  
  
  
