---
description: Attività di caricamento di Azure SQL DW
title: Attività di caricamento di Azure SQL DW | Microsoft Docs
ms.custom: ''
ms.date: 12/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPDWUPTASK.F1
- sql14.dts.designer.afpdwuptask.f1
ms.assetid: eef82c89-228a-4dc7-9bd0-ea00f57692f5
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: a374a5eaa64eb69d96ddfe609fb8561a1dc983b6
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725983"
---
# <a name="azure-sql-dw-upload-task"></a>Attività di caricamento di Azure SQL DW

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



L' **'attività di caricamento di Azure SQL DW** consente a un pacchetto SSIS di copiare dati tabulari in Azure SQL Data Warehouse (DW) dal file system o da Archiviazione BLOB di Azure.
L'attività usa PolyBase per migliorare le prestazioni, come descritto nell'articolo [Azure SQL Data Warehouse Loading Patterns and Strategies](/archive/blogs/sqlcat/azure-sql-data-warehouse-loading-patterns-and-strategies)(Modelli e strategie di caricamento di Azure SQL Data Warehouse).
Il formato di file dei dati di origine attualmente supportato è testo delimitato in codifica UTF8.
Quando si copia dal file system, i dati vengono prima caricati in Archiviazione BLOB di Azure per lo staging e poi in Azure SQL DW. Per questo motivo, è quindi necessario un account di Archiviazione BLOB di Azure.

**Attività di caricamento BLOB di Azure** è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Per aggiungere un' **attività di caricamento di Azure SQL DW**, trascinare l'attività da Casella degli strumenti SSIS nei canvas di progettazione, fare doppio clic o fare clic con il pulsante destro del mouse e selezionare **Modifica** per visualizzare la finestra di dialogo dell'editor dell'attività.

Nella pagina **Generale** configurare le proprietà seguenti.

**SourceType** specifica il tipo di archivio dati di origine. Selezionare uno dei tipi seguenti:

* **FileSystem:** i dati di origine si trovano nel file system locale.
* **BlobStorage:** i dati di origine si trovano in Archiviazione BLOB di Azure.

Di seguito sono elencate le proprietà per ogni tipo di origine.

### <a name="filesystem"></a>FileSystem

Campo|Descrizione
-----|-----------
LocalDirectory|Specifica la directory locale che contiene i file di dati da caricare.
Recursively (Ricorsivo)|Specifica se eseguire una ricerca ricorsiva delle sottodirectory.
FileName|Specifica un filtro per nome per selezionare i file con un determinato modello di nome. ad esempio Foglio*.xsl\* includerà file come Foglio001.xls e FoglioABC.xlsx.
RowDelimiter|Specifica il carattere che contrassegna la fine di ogni riga.
ColumnDelimiter|Specifica uno o più caratteri che contrassegnano la fine di ogni colonna. ad esempio &#124; (barra verticale), \t (TAB), ' (virgoletta singola), " (virgoletta doppia) e 0x5c (barra rovesciata).
IsFirstRowHeader|Specifica se la prima riga in ogni file di dati contiene nomi di colonna anziché dati effettivi.
AzureStorageConnection|Specifica una gestione connessione di Archiviazione di Azure.
BlobContainer|Specifica il nome di un contenitore BLOB in cui i dati locali verranno caricati e inoltrati ad Azure DW tramite PolyBase. Se il contenitore non esiste, ne verrà creato uno nuovo.
BlobDirectory|Specifica la directory BLOB, vale a dire una struttura gerarchica virtuale, in cui i dati locali verranno caricati e inoltrati ad Azure DW tramite PolyBase.
RetainFiles|Specifica se mantenere i file caricati in Archiviazione di Azure.
CompressionType|Specifica il formato di compressione da usare durante il caricamento dei file in Archiviazione di Azure. L'origine locale non è interessata.
CompressionLevel|Specifica il livello di compressione da usare per il formato di compressione.
AzureDwConnection|Specifica una gestione connessione ADO.NET per Azure SQL DW.
TableName|Specifica il nome della tabella di destinazione. Scegliere un nome di tabella esistente o crearne uno nuovo scegliendo **\<New Table ...>** .
TableDistribution|Specifica il metodo di distribuzione per la nuova tabella. Si applica se per **TableName**viene specificato un nuovo nome tabella.
HashColumnName|Specifica la colonna usata per la distribuzione di tabelle hash. Si applica se **HASH** è specificato per **TableDistribution**.

### <a name="blobstorage"></a>BlobStorage

Campo|Descrizione
-----|-----------
AzureStorageConnection|Specifica una gestione connessione di Archiviazione di Azure.
BlobContainer|Specifica il nome del contenitore BLOB in cui risiedono i dati di origine.
BlobDirectory|Specifica la directory BLOB (struttura gerarchica virtuale) in cui risiedono i dati di origine.
RowDelimiter|Specifica il carattere che contrassegna la fine di ogni riga.
ColumnDelimiter|Specifica uno o più caratteri che contrassegnano la fine di ogni colonna. ad esempio &#124; (barra verticale), \t (TAB), ' (virgoletta singola), " (virgoletta doppia) e 0x5c (barra rovesciata).
CompressionType|Specifica il formato di compressione usato per i dati di origine.
AzureDwConnection|Specifica una gestione connessione ADO.NET per Azure SQL DW.
TableName|Specifica il nome della tabella di destinazione. Scegliere un nome di tabella esistente o crearne uno nuovo scegliendo **\<New Table ...>** .
TableDistribution|Specifica il metodo di distribuzione per la nuova tabella. Si applica se per **TableName**viene specificato un nuovo nome tabella.
HashColumnName|Specifica la colonna usata per la distribuzione di tabelle hash. Si applica se **HASH** è specificato per **TableDistribution**.

Verrà visualizzata una pagina **Mapping** diversa a seconda che i dati siano copiati in una tabella nuova o in una esistente.
Nel primo caso, configurare le colonne di origine da mappare e i relativi nomi nella tabella di destinazione da creare.
Nel secondo caso, configurare le relazioni di mapping tra colonne di origine e di destinazione.

Nella pagina **Colonne** configurare le proprietà del tipo di dati per ogni colonna di origine.

La pagina **T-SQL** visualizza il linguaggio T-SQL usato per caricare i dati da Archiviazione BLOB di Azure in Azure SQL DW.
T-SQL viene generato automaticamente dalle configurazioni in altre pagine e verrà eseguito come parte dell'esecuzione dell'attività.
È possibile scegliere di modificare manualmente il linguaggio T-SQL generato per soddisfare esigenze specifiche. Fare quindi clic sul pulsante **Modifica** .
È possibile ripristinare quello generato automaticamente selezionando poi il pulsante **Reimposta** .