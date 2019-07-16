---
title: Installare e configurare i database di esempio AdventureWorks - SQL | Microsoft Docs
ms.prod: sql
ms.prod_service: sql
ms.technology: samples
ms.custom: ''
ms.date: 06/19/2018
ms.reviewer: ''
ms.topic: conceptual
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 99cdd6fdf5db075cc8fd46b738f468fd5d9a028d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67894922"
---
# <a name="adventureworks-installation-and-configuration"></a>Configurazione e installazione di AdventureWorks
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

AdventureWorks scaricare collegamenti e le istruzioni di installazione. 

## <a name="prerequisites"></a>Prerequisiti

- [SQL Server](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) oppure [Database SQL di Azure](https://azure.microsoft.com/services/sql-database/). Per la versione completa dell'esempio, usare SQL Server Evaluation o Developer o Enterprise Edition.
- [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md). Per ottenere risultati ottimali usano la versione di giugno 2016 o versione successiva.
 
## <a name="github-links"></a>Collegamenti a Github

- [Tutti i file AdventureWorks per SQL 2014-2016](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks)
- [Tutti i file AdventureWorks per SQL 2012](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2012)
- [Tutti i file AdventureWorks per SQL 2008 e 2008 R2](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks2008r2)

## <a name="oltp-downloads"></a>Download OLTP

Collegamenti diretti alle versioni OLTP di AdventureWorks sono disponibili di seguito:

- [AdventureWorks2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2017.bak)
- [AdventureWorks2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2016.bak)
- [AdventureWorks2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2014.bak)
- [AdventureWorks2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks2012.bak)
- [AdventureWorks2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008r2-oltp.bak)


## <a name="data-warehouse-downloads"></a>Download di Data Warehouse

Collegamenti diretti alle versioni di Data Warehouse di AdventureWorks sono disponibili di seguito:

- [AdventureWorksDW2017.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2017.bak)
- [AdventureWorksDW2016.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2016.bak)
- [AdventureWorksDW2014.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2014.bak)
- [AdventureWorksDW2012.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW2012.bak)
- [AdventureWorksDW2008R2.bak](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks2008r2/adventure-works-2008-dw.bak)

## <a name="creation-scripts"></a>Script di creazione
Il seguente script può essere usato per creare l'intero database AdventureWorks, indipendentemente dalla versione. 

- [Script di AdventureWorks OLTP con estensione Zip](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorks-oltp-install-script.zip)
- [File Zip di script di AdventureWorks DW](https://github.com/Microsoft/sql-server-samples/releases/download/adventureworks/AdventureWorksDW-data-warehouse-install-script.zip)

## <a name="install-to-sql-server"></a>Installare SQL Server

### <a name="restore-backup"></a>Ripristino di backup
Seguire i passaggi seguenti per ripristinare un backup del database usando SQL Server Management Studio. 

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server di destinazione.
2. Fare clic sui **database** nodo e selezionare **Ripristina Database**.
3. Selezionare **periferica** e fare clic sui puntini di sospensione ( **...** )
4. Nella finestra di dialogo **Seleziona dispositivi di backup**, fare clic su **Add**, passare al backup del database nel file System del server e selezionare il backup. Fare clic su **OK**.
5. Se necessario, modificare il percorso di destinazione per i dati e file di log, nelle **file** riquadro. Si noti che è buona norma inserire i dati di file e di log su unità differenti.
6. Fare clic su **OK**. Verrà avviata il ripristino di database. Al termine, sarà necessario il database AdventureWorks installato nell'istanza di SQL Server.

Per altre informazioni sul ripristino di un database di SQL Server, vedere [Ripristina un backup del database tramite SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).


### <a name="attach-a-datafile"></a>Collegare un file di dati
Seguire i passaggi seguenti per collegare il file di dati per il database usando SQL Server Management Studio.

1. Aprire SQL Server Management Studio e connettersi all'istanza di SQL Server di destinazione.
2. Fare clic sui **database** nodo e selezionare **Attach**.
3. Selezionare **Add** e passare ai. Si desidera collegare il file MDF. 
1. Selezionare il file e fare clic su **OK**. 
    1. Il database selezionato deve essere visualizzato nella finestra inferiore. Se il file è elencato come "non trovato", selezionare i puntini di sospensione ( **...** ) accanto al nome del file e aggiornare il percorso al percorso corretto. 
    1. Se hai solo il file di dati (mdf) e non il file di log (ldf), quindi evidenziare il file ldf nella finestra in basso e selezionare **rimuovere**. Si creerà un nuovo file di log. 
1. Selezionare **OK** per collegare il file. Dopo che il file è collegato, hai installato nell'istanza di SQL Server il database AdventureWorks.  

Per altre informazioni sul collegamento di file di database, vedere [collegare un database](../relational-databases/databases/attach-a-database.md). 

## <a name="install-to-azure-sql-database"></a>Installare il database SQL di Azure


Se non si dispone ancora un SQL Server in Azure, passare al [portale di Azure](https://portal.azure.com/) e creare un nuovo Database SQL. In quanto di creare un database, si creerà un server. Prendere nota del server. Visualizzare [in questa esercitazione](https://azure.microsoft.com/documentation/articles/sql-database-get-started/) per creare un database in pochi minuti.

1. Connettersi al portale di Azure.
1. Selezionare **crea una risorsa** nella parte superiore sinistra del riquadro di spostamento. 
1. Selezionare **database** e quindi selezionare **Database SQL**. 
1. Immettere le informazioni richieste.
1. Nel **Seleziona origine** campo, selezionare **Sample (AdventureWorksLT)** per ripristinare un backup del backup più recente AdventureWorksLT.
1. Selezionare **Create** per creare il nuovo Database SQL, ovvero la copia ripristinata del database AdventureWorksLT. 


## <a name="see-also"></a>Vedere anche
[Esercitazioni per SQL Server Management Studio](../ssms/tutorials/tutorial-sql-server-management-studio.md)   
[Esercitazioni per il motore di database di SQL Server](../relational-databases/database-engine-tutorials.md)
