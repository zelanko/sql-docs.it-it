---
title: Feature Pack di Integration Services (SSIS) per Azure | Microsoft Docs
ms.custom: ''
ms.date: 08/17/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.SSIS.AZURE.F1
- SQL14.SSIS.AZURE.F1
ms.assetid: 31de555f-ae62-4f2f-a6a6-77fea1fa8189
author: janinezhang
ms.author: janinez
ms.openlocfilehash: abe8c731a066ed764c2fc55da42bd630e46f3ae8
ms.sourcegitcommit: 8d01698e779a536093dd637e84c52f3ff0066a2c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/19/2019
ms.locfileid: "69610758"
---
# <a name="azure-feature-pack-for-integration-services-ssis"></a>Feature Pack di Integration Services (SSIS) per Azure

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Il Feature Pack di SQL Server Integration Services (SSIS) per Azure è un'estensione che fornisce i componenti elencati in questa pagina per consentire a SSIS di connettersi ai servizi Azure, trasferire i dati tra Azure e le origini dati locali ed elaborare i dati archiviati in Azure.

[![Scaricare il Feature Pack di SSIS per Azure](https://docs.microsoft.com/analysis-services/analysis-services/media/download.png)](https://www.microsoft.com/download/details.aspx?id=54798) **Scarica**

- Per SQL Server 2017 - [Microsoft SQL Server 2017 Integration Services Feature Pack per Azure](https://www.microsoft.com/download/details.aspx?id=54798)
- Per SQL Server 2016 - [Microsoft SQL Server 2016 Integration Services Feature Pack per Azure](https://www.microsoft.com/download/details.aspx?id=49492)
- Per SQL Server 2014 - [Microsoft SQL Server 2014 Integration Services Feature Pack per Azure](https://www.microsoft.com/download/details.aspx?id=47366)
- Per SQL Server 2012 - [Microsoft SQL Server 2012 Integration Services Feature Pack per Azure](https://www.microsoft.com/download/details.aspx?id=47367)

Le pagine di download includono anche informazioni sui prerequisiti. Assicurarsi di installare SQL Server prima di installare il Feature Pack di Azure in un server. In caso contrario i componenti del Feature Pack potrebbero non essere disponibili quando si distribuiscono pacchetti al database del catalogo SSIS (SSISDB) nel server.

## <a name="components-in-the-feature-pack"></a>Componenti del Feature Pack
-   Gestioni connessioni

    -   [Gestione connessioni di Azure Data Lake Analytics](connection-manager/azure-data-lake-analytics-connection-manager.md)

    -   [Gestione connessioni di Azure Data Lake Store](../integration-services/connection-manager/azure-data-lake-store-connection-manager.md)
    
    -   [Gestione connessione Azure HDInsight](../integration-services/connection-manager/azure-hdinsight-connection-manager.md)

    -   [Gestione connessione Azure Resource Manager](../integration-services/connection-manager/azure-resource-manager-connection-manager.md)
    
    -   [Gestione connessione dell'archiviazione di Azure](../integration-services/connection-manager/azure-storage-connection-manager.md)

    -   [Gestione connessione della sottoscrizione di Azure](../integration-services/connection-manager/azure-subscription-connection-manager.md)
    
-   Attività

    -   [Attività di download BLOB di Azure](../integration-services/control-flow/azure-blob-download-task.md)

    -   [Attività di caricamento BLOB di Azure](../integration-services/control-flow/azure-blob-upload-task.md)

    -   [Attività Azure Data Lake Analytics](control-flow/azure-data-lake-analytics-task.md)

    -   [Attività File system di Azure Data Lake Store](../integration-services/control-flow/azure-data-lake-store-file-system-task.md)

    -   [Attività di creazione cluster di Azure HDInsight](../integration-services/control-flow/azure-hdinsight-create-cluster-task.md)

    -   [Attività di eliminazione cluster di Azure HDInsight](../integration-services/control-flow/azure-hdinsight-delete-cluster-task.md)
    
    -   [Attività Hive di Azure HDInsight](../integration-services/control-flow/azure-hdinsight-hive-task.md)

    -   [Attività Pig di Azure HDInsight](../integration-services/control-flow/azure-hdinsight-pig-task.md)

    -   [Attività di caricamento di Azure SQL DW](../integration-services/control-flow/azure-sql-dw-upload-task.md)

    -   [Attività File flessibili](../integration-services/control-flow/flexible-file-task.md)

-   Componenti del flusso di dati

    -   [Origine BLOB di Azure](../integration-services/data-flow/azure-blob-source.md)

    -   [Destinazione BLOB di Azure](../integration-services/data-flow/azure-blob-destination.md)
    
    -   [Origine di Azure Data Lake Store](../integration-services/data-flow/azure-data-lake-store-source.md)
    
    -   [Destinazione di Azure Data Lake Store](../integration-services/data-flow/azure-data-lake-store-destination.md)

    -   [Origine di File flessibili](../integration-services/data-flow/flexible-file-source.md)

    -   [Destinazione di File flessibili](../integration-services/data-flow/flexible-file-destination.md)

-   Blob di Azure, Azure Data Lake Store ed Enumeratore file di Data Lake Store Gen2. Vedere [Contenitore Ciclo Foreach](../integration-services/control-flow/foreach-loop-container.md).

## <a name="use-tls-12"></a>Usare TLS 1.2

La versione di TLS usata dal Feature Pack di Azure dipende dalle impostazioni di sistema di .NET Framework.
Per usare TLS 1.2, aggiungere un valore `REG_DWORD` denominato `SchUseStrongCrypto` con dati `1` nelle due chiavi del Registro di sistema seguenti.

1. `HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\.NETFramework\v4.0.30319`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319`

## <a name="dependency-on-java"></a>Dipendenza da Java

Java è necessario per usare i formati di file ORC/Parquet con i connettori per file flat di Azure Data Lake Store.  
L'architettura (a 32 o a 64 bit) della build di Java deve corrispondere a quella del runtime di SSIS da usare.
Sono state sottoposte a test le build di Java seguenti.

- [OpenJDK 8u192 di Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Oracle Java SE Runtime Environment 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Configurare OpenJDK di Zulu

1. Scaricare ed estrarre il pacchetto di installazione con estensione zip.
2. Dal prompt dei comandi, eseguire `sysdm.cpl`.
3. Nella scheda **Avanzate** selezionare **Variabili di ambiente**.
4. Nella sezione **Variabili di sistema** selezionare **Nuova**.
5. Immettere `JAVA_HOME` in **Nome variabile**.
6. Selezionare **Sfoglia directory**, passare alla cartella estratta e selezionare la sottocartella `jre`.
   Selezionare quindi **OK** e **Valore variabile** verrà popolato automaticamente.
7. Selezionare **OK** per chiudere la finestra di dialogo **Nuova variabile di sistema**.
8. Selezionare **OK** per chiudere la finestra di dialogo **Variabili di ambiente**.
9. Selezionare **OK** per chiudere la finestra di dialogo **Proprietà del sistema**.

### <a name="set-up-zulus-openjdk-on-azure-ssis-integration-runtime"></a>Configurare OpenJDK di Zulu in Azure-SSIS Integration Runtime

Questa operazione deve essere eseguita tramite l'[interfaccia di configurazione personalizzata](https://docs.microsoft.com/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup) per Azure-SSIS Integration Runtime.
Si supponga di usare `zulu8.33.0.1-jdk8.0.192-win_x64.zip`.
Il contenitore BLOB può essere organizzato come indicato di seguito.

~~~
main.cmd
install_openjdk.ps1
zulu8.33.0.1-jdk8.0.192-win_x64.zip
~~~

Come punto di ingresso, `main.cmd` attiva l'esecuzione dello script di PowerShell `install_openjdk.ps1` che a sua volta estrae `zulu8.33.0.1-jdk8.0.192-win_x64.zip` e imposta `JAVA_HOME` di conseguenza.

**main.cmd**

~~~
powershell.exe -file install_openjdk.ps1
~~~

**install_openjdk.ps1**

~~~
Expand-Archive zulu8.33.0.1-jdk8.0.192-win_x64.zip -DestinationPath C:\
[Environment]::SetEnvironmentVariable("JAVA_HOME", "C:\zulu8.33.0.1-jdk8.0.192-win_x64\jre", "Machine")
~~~

### <a name="set-up-oracles-java-se-runtime-environment"></a>Configurare Oracle Java SE Runtime Environment

1. Scaricare ed eseguire il programma di installazione con estensione exe.
2. Seguire le istruzioni del programma di installazione per completare l'installazione.

## <a name="scenario-processing-big-data"></a>Scenario: Elaborazione di Big Data
 Usare il connettore di Azure per completare l'elaborazione di Big Data:

1.  Usare l'attività di caricamento BLOB di Azure per caricare i dati di input nell'archivio BLOB di Azure.

2.  Usare l'attività di creazione cluster di Azure HDInsight per creare un cluster di Azure HDInsight. Questo passaggio è facoltativo se si vuole usare un cluster personale.

3.  Usare l'attività Hive o Pig di Azure HDInsight per richiamare un processo Pig o Hive nel cluster di Azure HDInsight.

4.  Usare l'attività di eliminazione cluster di Azure HDInsight per eliminare il cluster di HDInsight dopo l'uso se è stato creato un cluster di HDInsight su richiesta nel passaggio 2.

5.  Usare l'attività di download BLOB di Azure HDInsight per scaricare i dati di output Pig/Hive dall'archivio BLOB di Azure.

![SSIS-AzureConnector-BigDataScenario](../integration-services/media/ssis-azureconnector-bigdatascenario.png)
 
## <a name="scenario-managing-data-in-the-cloud"></a>Scenario: Gestione di dati nel cloud
 Usare la destinazione BLOB di Azure in un pacchetto SSIS per scrivere i dati di output in un archivio BLOB di Azure oppure usare l'origine BLOB di Azure per leggere i dati da un archivio BLOB di Azure.

![SSIS-AzureConnector-CloudArchive-1](../integration-services/media/ssis-azureconnector-cloudarchive-1.png)
 
 ![SSIS-AzureConnector-CloudArchive-2](../integration-services/media/ssis-azureconnector-cloudarchive-2.png)

 Usare il contenitore Ciclo Foreach con l'enumeratore BLOB di Azure per elaborare i dati in più file BLOB.

![SSIS-AzureConnector-CloudArchive-3](../integration-services/media/ssis-azureconnector-cloudarchive-3.png)
  
