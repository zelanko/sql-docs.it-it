---
title: Feature Pack di Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL11.SSIS.AZURE.F1
- SQL12.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: chugugrace
ms.author: chugu
ms.openlocfilehash: abcad704ed02655c03a970d3fe4b80556b96cf69
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439398"
---
# <a name="azure-feature-pack"></a>Azure Feature Pack
Il Feature Pack di SQL Server Integration Services (SSIS) per Azure è un'estensione che fornisce i componenti elencati in questa pagina per consentire a SSIS di connettersi ai servizi Azure, trasferire i dati tra Azure e le origini dati locali ed elaborare i dati archiviati in Azure.

## <a name="components-in-the-feature-pack"></a>Componenti del Feature Pack
  
-   Gestioni connessioni  
  
    -   [Gestione connessione dell'archiviazione di Azure](connection-manager/azure-storage-connection-manager.md)  
  
    -   [Gestione connessione della sottoscrizione di Azure](connection-manager/azure-subscription-connection-manager.md)  
    
    -   [Gestione connessioni di Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-connection-manager.md)
    
    -   [Gestione connessione Azure Resource Manager](../../2014/integration-services/azure-resource-manager-connection-manager.md)
    
    -   [Gestione connessione Azure HDInsight](../../2014/integration-services/azure-hdinsight-connection-manager.md)
  
-   Attività  
  
    -   [Attività di caricamento BLOB di Azure](control-flow/azure-blob-upload-task.md)  
  
    -   [Attività di download BLOB di Azure](control-flow/azure-blob-download-task.md)  
  
    -   [Attività Hive di Azure HDInsight](control-flow/azure-hdinsight-hive-task.md)  
  
    -   [Attività Pig di Azure HDInsight](https://msdn.microsoft.com/library/mt146781(v=sql.120).aspx)
  
    -   [Attività di creazione cluster di Azure HDInsight](control-flow/azure-hdinsight-create-cluster-task.md)  
  
    -   [Attività di eliminazione cluster di Azure HDInsight](control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Attività di caricamento di Azure SQL DW](../../2014/integration-services/azure-sql-dw-upload-task.md)    
    
    -   [Attività File system di Azure Data Lake Store](control-flow/file-system-task.md)    
  
-   Componenti del flusso di dati  
  
    -   [Origine BLOB di Azure](https://msdn.microsoft.com/library/mt146775(v=sql.120).aspx)  
  
    -   [Destinazione BLOB di Azure](data-flow/azure-blob-destination.md)  
    
    -   [Origine di Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-source.md)
    
    -   [Destinazione di Azure Data Lake Store](../../2014/integration-services/azure-data-lake-store-destination.md)
  
-   Enumeratore BLOB di Azure & enumeratore del file ADLS. Vedere [contenitore ciclo foreach](control-flow/foreach-loop-container.md).  
  
 
## <a name="download-the-feature-pack"></a>Scaricare il Feature Pack  
Scaricare il Feature Pack di SQL Server Integration Services (SSIS) per Azure.  
  
-   [Microsoft SQL Server 2014 Integration Services Feature Pack per Azure](https://www.microsoft.com/download/details.aspx?id=47366)  

## <a name="prerequisites"></a>Prerequisiti  
Prima di installare questo Feature Pack, è necessario installare i prerequisiti seguenti.  
  
-   SQL Server Integration Services  
-   .Net Framework 4.5  
  
## <a name="scenarios"></a>Scenari  
  
### <a name="big-data-processing"></a>Elaborazione di Big Data  
 Usare il connettore di Azure per completare l'elaborazione di Big Data:  
  
1.  Usare l'attività di caricamento BLOB di Azure per caricare i dati di input nell'archivio BLOB di Azure.  
  
2.  Usare l'attività di creazione cluster di Azure HDInsight per creare un cluster di Azure HDInsight. Questo passaggio è facoltativo se si vuole usare un cluster personale.  
  
3.  Usare l'attività Hive o Pig di Azure HDInsight per richiamare un processo Pig o Hive nel cluster di Azure HDInsight.  
  
4.  Usare l'attività di eliminazione cluster di Azure HDInsight per eliminare il cluster di HDInsight dopo l'uso se è stato creato un cluster di HDInsight su richiesta nel passaggio 2.  
  
5.  Usare l'attività di download BLOB di Azure HDInsight per scaricare i dati di output Pig/Hive dall'archivio BLOB di Azure.  
  
 ![SSIS-AzureConnector-BigDataScenario](media/ssis-azureconnector-bigdatascenario.png "SSIS-AzureConnector-BigDataScenario")  
  
### <a name="cloud-data-archiving"></a>Archiviazione dei dati cloud  
 Usare la destinazione BLOB di Azure in un pacchetto SSIS per scrivere i dati di output in un archivio BLOB di Azure oppure usare l'origine BLOB di Azure per leggere i dati da un archivio BLOB di Azure.  
  
 ![SSIS-AzureConnector-CloudArchive-1](media/ssis-azureconnector-cloudarchive-1.png "SSIS-AzureConnector-CloudArchive-1")  
  
 ![SSIS-AzureConnector-CloudArchive-2](media/ssis-azureconnector-cloudarchive-2.png "SSIS-AzureConnector-CloudArchive-2")  
  
 Inoltre, usare il contenitore Ciclo Foreach con l'enumeratore BLOB di Azure per elaborare i dati in più file BLOB.  
  
 ![SSIS-AzureConnector-CloudArchive-3](media/ssis-azureconnector-cloudarchive-3.png "SSIS-AzureConnector-CloudArchive-3")  
  
  
