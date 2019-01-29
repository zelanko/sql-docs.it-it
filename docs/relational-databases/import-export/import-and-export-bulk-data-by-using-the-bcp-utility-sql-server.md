---
title: Importare ed esportare dati per operazioni bulk usando l'utilità bcp (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 09/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: data-movement
ms.topic: conceptual
helpviewer_keywords:
- bulk exporting [SQL Server], bcp utility
- bulk importing [SQL Server], bcp utility
- bcp utility [SQL Server], about bcp utility
ms.assetid: 73e949de-67a3-4c84-9735-7da1ad4ba34a
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 86652126be5c58068de4aaff5d7500d91f3c6f02
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55045527"
---
# <a name="import-and-export-bulk-data-by-using-the-bcp-utility-sql-server"></a>Importazione ed esportazione di dati per operazioni bulk tramite l'utilità bcp (SQL Server)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Questo argomento offre una panoramica sull'uso dell'[utilità bcp](../../tools/bcp-utility.md) per l'esportazione di dati da qualsiasi posizione di un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui è possibile usare un'istruzione SELECT, incluse le viste partizionate.  
  
 L'utilità bcp (Bcp.exe) è uno strumento della riga di comando che utilizza l'API del programma per la copia bulk (BCP). L'utilità bcp consente di eseguire le operazioni seguenti:  
  
-   Esportazioni bulk di dati da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un file di dati.  
  
-   Esportazioni bulk di dati da una query.  
  
-   Importazioni bulk di dati da un file di dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Generazione di file di formato.  
  
 L'utilità bcp è accessibile con il comando **bcp** . Per usare il comando **bcp** un'importazione in blocco di dati, è necessario conoscere lo schema della tabella e i tipi di dati delle colonne, a meno che non venga usato un file di formato preesistente.  
  
 L'utilità consente di esportare dati da una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un file di dati per utilizzarli in altri programmi. Consente inoltre di importare dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da un altro programma, in genere un altro sistema di gestione di database (DBMS, Database Management System). I dati vengono innanzitutto esportati dal programma di origine in un file di dati e quindi, in un'operazione separata, vengono copiati dal file di dati in una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Le opzioni del comando **bcp** consentono di specificare il tipo di dati del file di dati e altre informazioni. Se tali opzioni non vengono specificate, verrà richiesto di immettere le informazioni sulla formattazione, ad esempio il tipo dei campi dati di un file di dati. Verrà quindi richiesto se si desidera creare un file di formato contenente le risposte interattive fornite. Un file di formato risulta spesso utile per assicurare la flessibilità per operazioni future di importazione o esportazione bulk. È possibile specificare il file di formato in comandi **bcp** successivi per file di dati equivalenti. Per altre informazioni, vedere [Impostazione dei formati di dati per la compatibilità mediante bcp &#40;SQL Server&#41;](../../relational-databases/import-export/specify-data-formats-for-compatibility-when-using-bcp-sql-server.md).  
  
>**Nota.** l'utilità bcp viene scritta con la copia bulk di ODBC.
  
 Per una descrizione della sintassi del comando **bcp** , vedere [Utilità bcp](../../tools/bcp-utility.md).  
  
## <a name="examples"></a>Esempi  

|Gli argomenti seguenti contengono esempi relativi all'uso di bcp: |
|---|
|[bcp Utility](../../tools/bcp-utility.md)<br /><br />Formati di dati per l'importazione o l'esportazione bulk (SQL Server)<br />&emsp;&#9679;&emsp;[Usare il formato nativo per importare o esportare dati (SQL Server)](../../relational-databases/import-export/use-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare il formato carattere per importare o esportare dati (SQL Server)](../../relational-databases/import-export/use-character-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare il formato nativo Unicode per importare o esportare dati (SQL Server)](../../relational-databases/import-export/use-unicode-native-format-to-import-or-export-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare il formato carattere Unicode per importare o esportare dati (SQL Server)](../../relational-databases/import-export/use-unicode-character-format-to-import-or-export-data-sql-server.md)<br /><br />[Impostazione dei caratteri di terminazione del campo e della riga (SQL Server)](../../relational-databases/import-export/specify-field-and-row-terminators-sql-server.md)<br /><br />[Mantenimento dei valori Null o utilizzo dei valori predefiniti durante un'importazione bulk (SQL Server)](../../relational-databases/import-export/keep-nulls-or-use-default-values-during-bulk-import-sql-server.md)<br /><br />[Mantenere i valori Identity durante l'importazione bulk dei dati (SQL Server)](../../relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server.md)<br /><br />File di formato per l'importazione o l'esportazione di dati (SQL Server)<br />&emsp;&#9679;&emsp;[Creare un file di formato (SQL Server)](../../relational-databases/import-export/create-a-format-file-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare un file di formato per l'importazione bulk dei dati (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-bulk-import-data-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare un file di formato per ignorare una colonna di una tabella (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-table-column-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare un file di formato per ignorare un campo dati (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-skip-a-data-field-sql-server.md)<br />&emsp;&#9679;&emsp;[Usare un file di formato per eseguire il mapping tra le colonne della tabella e i campi del file di dati (SQL Server)](../../relational-databases/import-export/use-a-format-file-to-map-table-columns-to-data-file-fields-sql-server.md)<br /><br />[Esempi di importazione ed esportazione bulk di documenti XML (SQL Server)](../../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)<br /><p>                                                                                                                                                                                                                  </p>|

  
## <a name="more-examples-and-information"></a>Altri esempi e informazioni  
 [INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/insert-transact-sql.md)   
 [Clausola SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-clause-transact-sql.md)   
 [bcp Utility](../../tools/bcp-utility.md)   
 [Prepararsi all'importazione in blocco dei dati &#40;SQL Server&#41;](../../relational-databases/import-export/prepare-to-bulk-import-data-sql-server.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md)   
 [Informazioni sull'importazione ed esportazione in blocco di dati &#40;SQL Server&#41;](../../relational-databases/import-export/bulk-import-and-export-of-data-sql-server.md)   
 [OPENROWSET &#40;Transact-SQL&#41;](../../t-sql/functions/openrowset-transact-sql.md)   
 [Creare un file di formato &#40;SQL Server&#41;](../../relational-databases/import-export/create-a-format-file-sql-server.md)  
  
  
