---
title: Informazioni sull'importazione ed esportazione bulk di dati (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e90afe2092623fa1dd356e51af5fff7a19e9a2ca
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66012115"
---
# <a name="bulk-import-and-export-of-data-sql-server"></a>Informazioni sull'importazione ed esportazione bulk di dati (SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'esportazione in blocco dei dati (*dati in blocco*) da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'importazione in blocco dei dati in una tabella o in una vista non partizionata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'importazione e l'esportazione bulk sono essenziali per trasferire in modo efficiente i dati tra [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e origini dei dati eterogenee. Per*esportazione bulk* si intende la copia di dati da una tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un file di dati. L'*importazione in blocco* indica il caricamento di dati da un file di dati a una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Ad esempio, è possibile esportare dati da un'applicazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel in un file di dati e quindi eseguire l'importazione bulk di tali dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Contenuto dell'argomento**  
  
-   [Introduzione alle operazioni di importazione ed esportazione bulk](#Intro)  
  
-   [Attività correlate](#RelatedTasks)  
  
##  <a name="bulk-import-and-bulk-export-overview"></a><a name="Intro"></a>Panoramica sull'importazione e l'esportazione bulk  
 In questa sezione vengono elencati e confrontati sinteticamente i vari metodi disponibili per l'importazione e l'esportazione bulk dei dati. Vengono inoltre introdotti i file di formato.  
  
 **Contenuto dell'argomento:**  
  
-   [Metodi per l'importazione e l'esportazione bulk di dati](#MethodsForBuliIE)  
  
-   [File di formato](#FFs)  
  
###  <a name="methods-for-bulk-importing-and-exporting-data"></a><a name="MethodsForBuliIE"></a>Metodi per l'importazione e l'esportazione bulk di dati  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta l'esportazione bulk dei dati da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e l'importazione bulk dei dati in una tabella o in una vista non partizionata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sono disponibili le modalità di base seguenti.  
  
|Metodo|Descrizione|Importazione dei dati|Esportazione dei dati|  
|------------|-----------------|------------------|------------------|  
|[utilità bcp](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)|Utilità della riga di comando (Bcp.exe) che esegue l'esportazione e l'importazione bulk dei dati e genera file di formato.|Sì|Sì|  
|[BULK INSERT - istruzione](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che importa i dati direttamente da un file di dati in una tabella di database o in una vista non partizionata.|Sì|No|  
|[INSERT ... Istruzione SELECT * FROM OPENROWSET(BULK...)](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)|Istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] che usa il provider di set di righe con lettura bulk OPENROWSET per eseguire l'importazione bulk dei dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] specificando la funzione OPENROWSET(BULK...) per selezionare i dati in un'istruzione INSERT.|Sì|No|  
  
> [!IMPORTANT]  
>  I file con valori delimitati da virgole (CSV) non sono supportati nelle operazioni di importazione bulk di SQL Server. In alcuni casi, tuttavia, è possibile utilizzare un file CSV come file di dati per un'importazione bulk di dati in SQL Server. Si noti che il carattere di terminazione del campo di un file CSV non può essere una virgola. Per altre informazioni, vedere [Preparazione dei dati per l'importazione o l'esportazione bulk &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md).  
  
###  <a name="format-files"></a><a name="FFs"></a>File di formato  
 Utilità **bcp** , BULK INSERT e INSERT... SELECT \* FROM OPENROWSET (bulk...) supportano tutti l'utilizzo di un *file di formato* specializzato che archivia le informazioni sul formato per ogni campo di un file di dati. Un file di formato può inoltre contenere informazioni sulla tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrispondente. Il file di formato può essere utilizzato per specificare tutte le informazioni sul formato necessarie per l'esportazione e l'importazione bulk dei dati da e verso un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 I file di formato costituiscono un modo flessibile per interpretare i dati così come presenti nel file di dati durante l'importazione, nonché per formattare i dati nel file di dati durante l'esportazione. Grazie a questa flessibilità, non è necessario scrivere codice specifico per interpretare i dati o riformattarli in base ai requisiti specifici di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o dell'applicazione esterna. Ad esempio, se si esegue l'esportazione bulk dei dati da caricare in un'applicazione che richiede valori separati da virgola, è possibile utilizzare un file di formato per inserire virgole come caratteri di terminazione del campo nei dati esportati.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta due tipi di file di formato: file di formato XML e file di formato non XML.  
  
 L'utilità **bcp** è il solo strumento in grado di generare un file di formato. Per altre informazioni, vedere [Creazione di un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md). Per altre informazioni sui file di formato, vedere [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md).  
  
> [!NOTE]  
>  Nei casi in cui un file di formato non viene fornito durante un'operazione di esportazione o importazione bulk, è possibile ignorare la formattazione predefinita nella riga di comando.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Importare ed esportare dati per operazioni bulk usando l'utilità bcp &#40;SQL Server&#41;](import-and-export-bulk-data-by-using-the-bcp-utility-sql-server.md)  
  
-   [Importazione di dati per operazioni bulk utilizzando BULK INSERT o OPENROWSET&#40;BULK...&#41; &#40;SQL Server&#41;](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md)  
  
-   [Mantenere i valori Identity durante l'importazione in blocco dei dati &#40;SQL Server&#41;](keep-identity-values-when-bulk-importing-data-sql-server.md)  
  
-   [Mantenimento dei valori Null o uso dei valori predefiniti durante un'importazione bulk &#40;SQL Server&#41;](keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)  
  
-   [Preparare i dati per l'importazione o l'esportazione in blocco &#40;SQL Server&#41;](prepare-data-for-bulk-export-or-import-sql-server.md)  
  
 **Per utilizzare un file di formato**  
  
-   [Creazione di un file di formato &#40;SQL Server&#41;](create-a-format-file-sql-server.md)  
  
-   [Usare un file di formato per l'importazione in blocco dei dati &#40;SQL Server&#41;](use-a-format-file-to-bulk-import-data-sql-server.md)  
  
-   [Utilizzo di un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati &#40;SQL Server&#41;](use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)  
  
-   [Utilizzo di un file di formato per escludere un campo di dati &#40;SQL Server&#41;](use-a-format-file-to-skip-a-data-field-sql-server.md)  
  
-   [Utilizzo di un file di formato per ignorare una colonna di una tabella &#40;SQL Server&#41;](use-a-format-file-to-skip-a-table-column-sql-server.md)  
  
 **Per utilizzare formati di dati per l'importazione o l'esportazione bulk**  
  
-   [Importare dati in formato nativo e carattere da versioni precedenti di SQL Server](import-native-and-character-format-data-from-earlier-versions-of-sql-server.md)  
  
-   [Utilizzo del formato carattere per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato nativo per importare o esportare dati &#40;SQL Server&#41;](use-native-format-to-import-or-export-data-sql-server.md)  
  
-   [Utilizzo del formato carattere Unicode per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](use-unicode-character-format-to-import-or-export-data-sql-server.md)  
  
-   [Usare il formato Unicode nativo per importare o esportare dati &#40;SQL Server&#41;](use-unicode-native-format-to-import-or-export-data-sql-server.md)  
  
 **Per specificare i formati di dati per la compatibilità mediante bcp**  
  
1.  [Impostazione dei caratteri di terminazione del campo e della riga &#40;SQL Server&#41;](specify-field-and-row-terminators-sql-server.md)  
  
2.  [Specificare la lunghezza del prefisso nei file di dati con bcp &#40;SQL Server&#41;](specify-prefix-length-in-data-files-by-using-bcp-sql-server.md)  
  
3.  [Specifica del tipo di archiviazione di file tramite bcp &#40;SQL Server&#41;](specify-file-storage-type-by-using-bcp-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Prerequisiti per la registrazione minima nell'importazione bulk](prerequisites-for-minimal-logging-in-bulk-import.md)   
 [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [Esempi di importazione ed esportazione bulk di documenti XML &#40;SQL Server&#41;](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)   
 [Copiare database in altri server](../databases/copy-databases-to-other-servers.md)   
 [Esecuzione del caricamento bulk di dati XML &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-xpath-queries/bulk-load-xml/performing-bulk-load-of-xml-data-sqlxml-4-0.md)   
 [Esecuzione di operazioni di copia bulk](../native-client/features/performing-bulk-copy-operations.md)   
 [Utilità bcp](../../tools/bcp-utility.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](format-files-for-importing-or-exporting-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](/sql/t-sql/functions/openrowset-transact-sql)  
  
  
