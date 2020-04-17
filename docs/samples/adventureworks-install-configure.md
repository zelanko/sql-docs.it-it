---
title: Installare e configurare il database di esempio AdventureWorksInstall and configure AdventureWorks sample database
description: Seguire queste istruzioni per scaricare e installare i database di esempio AdventureWorks con SQL Server Management StudioSQL Server Management Studio o nel database SQL di Azure.Follow these instructions to download and install AdventureWorks sample databases with SQL Server Management StudioSQL Server Management Studio or in Azure SQL Database.
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.custom: seo-lt-2019
ms.openlocfilehash: 7fa3d199450750a444f2b67ae3e4583549d449b9
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484570"
---
# <a name="adventureworks-installation-and-configuration"></a>Installazione e configurazione di AdventureWorks
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Collegamenti di download e istruzioni di installazione di AdventureWorks. 

## <a name="prerequisites"></a>Prerequisiti

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) o [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/). Per la versione completa dell'esempio, usare SQL Server Evaluation/Developer/Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Per ottenere i migliori risultati, utilizzare la versione di giugno 2016 o successiva.
 
## <a name="oltp-downloads"></a>Download OLTP

I collegamenti diretti alle versioni OLTP di AdventureWorks sono disponibili di seguito:

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>Download del data warehouse

I collegamenti diretti alle versioni di AdventureWorks del data warehouse sono disponibili di seguito:

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-dw.bak)

## <a name="creation-scripts"></a>Script di creazione
Gli script seguenti possono essere utilizzati per creare l'intero database AdventureWorks, indipendentemente dalla versione. 

- [AdventureWorks OLTP Script zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [AdventureWorks DW Script zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="github-links"></a>Collegamenti GitHub

- [Tutti i file AdventureWorks per SQL 2014 - 2016](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [Tutti i file AdventureWorks per SQL 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [Tutti i file AdventureWorks per SQL 2008 e 2008R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="install-to-sql-server"></a>Installare in SQL Server

### <a name="restore-backup"></a>Ripristina backup
Seguire i passaggi seguenti per ripristinare un backup del database tramite SQL Server Management Studio. 

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server di destinazione.
2. Fare clic con il pulsante destro del mouse sul nodo **Database** e scegliere **Ripristina database**.
3. Selezionare **Dispositivo** e fare clic sui puntini di sospensione (**...**)
4. Nella finestra di dialogo **Selezione periferiche di backup**fare clic su **Aggiungi**, passare al backup del database nel file system del server e selezionare il backup. Fare clic su **OK**.
5. Se necessario, modificare il percorso di destinazione per i file di dati e di log nel riquadro **File.** Si noti che è consigliabile inserire i file di dati e di log in unità diverse.
6. Fare clic su **OK**. Verrà avviato il ripristino del database. Al termine, il database AdventureWorks verrà installato nell'istanza di SQL Server.

Per ulteriori informazioni sul ripristino di un database di SQL Server, vedere Ripristinare un backup del [database tramite SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).


### <a name="attach-a-datafile"></a>Allegare un file di dati
Seguire i passaggi seguenti per collegare il file di dati per il database usando SQL Server Management StudioSQL Server Management Studio.Follow the below steps to attach the datafile for your database using SQL Server Management StudioSQL Server Management Studio.

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server di destinazione.
2. Fare clic con il pulsante destro del mouse sul nodo **Database** e scegliere **Collega**.
3. Selezionare **Aggiungi** e passare al file . MDF che si desidera allegare. 
1. Selezionare il file e fare clic su **OK**. 
    1. Il database selezionato dovrebbe essere visualizzato nella finestra inferiore. Se il file è elencato come "non trovato", selezionare i puntini di sospensione (**...**) accanto al nome del file e aggiornare il percorso al percorso corretto. 
    1. Se si dispone solo del file di dati (con estensione mdf) e non del file di registro (con estensione ldf), evidenziare il file ldf nella finestra inferiore e selezionare **Rimuovi**. Verrà creato un nuovo file di registro. 
1. Selezionare **OK** per allegare il file. Dopo aver collegato il file, il database AdventureWorks sarà installato nell'istanza di SQL Server.  

Per ulteriori informazioni sul collegamento di file di database, vedere [Collegare un database](../relational-databases/databases/attach-a-database.md). 

## <a name="install-to-azure-sql-database"></a>Installare nel database SQL di AzureInstall to Azure SQL Database


Se non si dispone ancora di UN SQL Server in Azure, passare al portale di [Azure](https://portal.azure.com/) e creare un nuovo database SQL. Durante la creazione di un database, si creerà un server. Prendere nota del server. Vedere [questa esercitazione](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) per creare un database in pochi minuti.

1. Connettersi al portale di Azure.Connect to your Azure portal.
1. Selezionare **Crea una risorsa** nella parte superiore sinistra del riquadro di spostamento. 
1. Selezionare **Database** e quindi **Database SQL**. 
1. Inserire le informazioni richieste.
1. Nel campo **Seleziona origine** selezionare **Esempio (AdventureWorksLT)** per ripristinare un backup dell'ultimo backup AdventureWorksLT.
1. Selezionare **Crea** per creare il nuovo database SQL, ovvero la copia ripristinata del database AdventureWorksLT. 


## <a name="see-also"></a>Vedere anche
[Esercitazioni per SQL Server Management StudioTutorials for SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[Esercitazioni per il motore di database di SQL ServerTutorials for SQL Server database engine](../relational-databases/database-engine-tutorials.md)
