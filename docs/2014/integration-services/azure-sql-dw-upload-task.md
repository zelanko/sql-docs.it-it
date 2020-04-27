---
title: Attività di caricamento di Azure SQL DW | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPDWUPTASK.F1
- SQL11.DTS.DESIGNER.AFPDWUPTASK.F1
ms.assetid: 112cf764-f85a-4c1a-b732-d299d717c0d4
author: yualan
ms.author: janinez
manager: craigg
ms.openlocfilehash: d3c310ee1d60648ac4b1eb299a0fd291adb86aea
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66061287"
---
# <a name="azure-sql-dw-upload-task"></a>Attività di caricamento di Azure SQL DW
L' **attività di caricamento di Azure SQL DW** consente a un pacchetto SSIS di caricare i dati locali in una tabella in Azure SQL Data Warehouse (DW). Il formato di file dei dati di origine attualmente supportato è testo delimitato in codifica UTF8. Il processo di caricamento segue l'approccio di polibase efficiente. In particolare, i dati vengono prima caricati in Archiviazione BLOB di Azure e poi in Azure SQL DW. Per usare questa attività, è quindi necessario un account di Archiviazione BLOB di Azure.

Per aggiungere un' **attività di caricamento di Azure SQL DW**, trascinare l'attività da Casella degli strumenti SSIS nei canvas di progettazione, fare doppio clic o fare clic con il pulsante destro del mouse e selezionare **Modifica** per visualizzare la finestra di dialogo dell'editor dell'attività.

Nella pagina **Generale** configurare le proprietà seguenti.

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
TableName|Specifica il nome della tabella di destinazione. Scegliere un nome di tabella esistente o crearne uno nuovo scegliendo ** \<nuova tabella... >**.
TableDistribution|Specifica il metodo di distribuzione per la nuova tabella. Si applica se per **TableName**viene specificato un nuovo nome tabella.
HashColumnName|Specifica la colonna usata per la distribuzione di tabelle hash. Si applica se **HASH** è specificato per **TableDistribution**.

Verrà visualizzata una pagina **Mapping** diversa a seconda che i dati siano caricati in una tabella nuova o in una esistente. Nel primo caso, configurare le colonne di origine da mappare e i relativi nomi nella tabella di destinazione da creare. Nel secondo caso, configurare le relazioni di mapping tra colonne di origine e di destinazione.

Nella pagina **Colonne** configurare le proprietà del tipo di dati per ogni colonna di origine.

La pagina **T-SQL** visualizza il linguaggio T-SQL usato per caricare i dati da Archiviazione BLOB di Azure in Azure SQL DW. T-SQL viene generato automaticamente dalle configurazioni in altre pagine e verrà eseguito come parte dell'esecuzione dell'attività. È possibile scegliere di modificare manualmente il linguaggio T-SQL generato per soddisfare esigenze specifiche. Fare quindi clic sul pulsante **Modifica** . È possibile ripristinare quello generato automaticamente selezionando poi il pulsante **Reimposta** .
