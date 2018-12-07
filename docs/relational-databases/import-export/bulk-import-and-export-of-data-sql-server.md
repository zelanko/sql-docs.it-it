---
title: Informazioni sull'importazione ed esportazione bulk di dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- exporting data
- bulk importing [SQL Server], about bulk importing
- data [SQL Server], bulk export and import
- transferring data
- importing data, (See also bulk importing [SQL Server])
- copying data [SQL Server]
- bulk exporting [SQL Server]
- importing data, bulk import
- copying data [SQL Server], bulk export and import
- exporting data,(See also bulk exporting [SQL Server])
- bulk exporting [SQL Server], about bulk exporting
- bulk importing [SQL Server]
- importing data
ms.assetid: 19049021-c048-44a2-b38d-186d9f9e4a65
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a1a8a8beb6f39db8aa7f3b72189870e26762dca
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52533545"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>Informazioni sull'importazione ed esportazione bulk di dati (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'esportazione in blocco dei dati (*dati in blocco*) da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'importazione in blocco dei dati in una tabella o in una vista non partizionata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  
-   Per*esportazione bulk* si intende la copia di dati da una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un file di dati.

-   L'*importazione in blocco* indica il caricamento di dati da un file di dati a una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ad esempio, è possibile esportare dati da un'applicazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel in un file di dati e quindi eseguire l'importazione bulk di tali dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
 
##  <a name="MethodsForBuliIE"></a> Metodi di importazione ed esportazione bulk di dati  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'esportazione bulk dei dati da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'importazione bulk dei dati in una tabella o in una vista non partizionata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sono disponibili le modalità di base seguenti.  
 
  
|Metodo|Descrizione|Importazione dei dati|Esportazione dei dati|  
|------------|-----------------|------------------|------------------|  
|[utilità bcp](../../relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|Utilità della riga di comando (Bcp.exe) che esegue l'esportazione e l'importazione bulk dei dati e genera file di formato.|Sì|Sì|  
|[BULK INSERT - istruzione](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che importa i dati direttamente da un file di dati in una tabella di database o in una vista non partizionata.|Sì|no|  
|[INSERT ... Istruzione SELECT * FROM OPENROWSET(BULK...)](../../relational-databases/import-export/import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che usa il provider di set di righe con lettura bulk OPENROWSET per eseguire l'importazione bulk dei dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificando la funzione OPENROWSET(BULK...) per selezionare i dati in un'istruzione INSERT.|Sì|no| 
|[Importazione/Esportazione guidata SQL Server](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)|La procedura guidata crea pacchetti semplici che importano ed esportano dati tra numerosi formati di dati comuni, inclusi database, fogli di calcolo e file di testo.|Sì|Sì|  
  
> [!IMPORTANT]
> I file con valori delimitati da virgole (CSV) non sono supportati nelle operazioni di importazione bulk di SQL Server. In alcuni casi, tuttavia, è possibile usare un file CSV come file di dati per un'importazione bulk di dati in SQL Server. Si noti che il carattere di terminazione del campo di un file CSV non può essere una virgola. Per altre informazioni, vedere [Preparazione dei dati per l'importazione o l'esportazione bulk (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md).

> [!NOTE]
> Per l'importazione e l'esportazione di file delimitati, il database SQL di Azure e Azure SQL DW supportano solo l'utilità bcp.
  
##  <a name="FFs"></a> File di formato  
 [utilità bcp](../../tools/bcp-utility.md), [BULK INSERT](../../t-sql/statements/bulk-insert-transact-sql.md) e [INSERT ... SELECT * FROM OPENROWSET(BULK...)](../../t-sql/functions/openrowset-transact-sql.md) supportano l'uso di un *file di formato* specializzato che archivia le informazioni sul formato di ogni campo in un file di dati. Un file di formato può inoltre contenere informazioni sulla tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrispondente. Il file di formato può essere utilizzato per specificare tutte le informazioni sul formato necessarie per l'esportazione e l'importazione bulk dei dati da e verso un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 I file di formato costituiscono un modo flessibile per interpretare i dati così come presenti nel file di dati durante l'importazione, nonché per formattare i dati nel file di dati durante l'esportazione. Grazie a questa flessibilità, non è necessario scrivere codice specifico per interpretare i dati o riformattarli in base ai requisiti specifici di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dell'applicazione esterna. Ad esempio, se si esegue l'esportazione bulk dei dati da caricare in un'applicazione che richiede valori separati da virgola, è possibile utilizzare un file di formato per inserire virgole come caratteri di terminazione del campo nei dati esportati.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta due tipi di file di formato: file di formato XML e file di formato non XML.  
  
 L' [utilità bcp](../../tools/bcp-utility.md) è il solo strumento in grado di generare un file di formato. Per altre informazioni, vedere [Creazione di un file di formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md). Per altre informazioni sui file di formato, vedere [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
> [!NOTE]
> Nei casi in cui un file di formato non viene fornito durante un'operazione di esportazione o importazione bulk, è possibile ignorare la formattazione predefinita nella riga di comando.

|Argomenti correlati|
|---|
|[Preparazione dei dati per l'importazione o l'esportazione bulk (SQL Server)](../../relational-databases/import-export/prepare-data-for-bulk-export-or-import-sql-server.md)|
|[Formati di dati per l'importazione o l'esportazione bulk (SQL Server)](../../relational-databases/import-export/data-formats-for-bulk-import-or-bulk-export-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare il formato nativo per importare o esportare dati (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare il formato carattere per importare o esportare dati (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare il formato nativo Unicode per importare o esportare dati (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare il formato carattere Unicode per importare o esportare dati (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](../../relational-databases/import-export/import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)|
|[Impostazione dei formati di dati per la compatibilità mediante bcp (SQL Server)](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Specificare il tipo di archiviazione di file tramite bcp (SQL Server)](../../relational-databases/import-export/specify-file-storage-type-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Specificare la lunghezza del prefisso nei file di dati tramite bcp (SQL Server)](../../relational-databases/import-export/specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Specificare la lunghezza di campo tramite bcp (SQL Server)](../../relational-databases/import-export/specify-field-length-by-using-bcp-sql-server.md)<br />&emsp;&#9679;&emsp;[Specificare i caratteri di terminazione del campo e della riga (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)|
|[Mantenimento dei valori Null o utilizzo dei valori predefiniti durante un'importazione bulk (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)|
|[Mantenere i valori Identity durante l'importazione bulk dei dati (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)|
|[File di formato per l'importazione o l'esportazione di dati (SQL Server)](../../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Creare un file di formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare un file di formato per l'importazione bulk dei dati (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare un file di formato per ignorare una colonna di una tabella (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare un file di formato per ignorare un campo dati (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)|
 
  
## <a name="more-information"></a>Altre informazioni!  
 [Prerequisiti per la registrazione minima nell'importazione bulk](../../relational-databases/import-export/prerequisites-for-minimal-logging-in-bulk-import.md)   
 [Esempi di importazione ed esportazione in blocco di documenti XML &#40;SQL Server&#41;](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [Copia di database in altri server](../../relational-databases/databases/copy-databases-to-other-servers.md)   
 [Esecuzione del caricamento bulk di dati XML &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [Esecuzione di operazioni di copia bulk](../../relational-databases/native-client/features/performing-bulk-copy-operations.md)   

  
  
