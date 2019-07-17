---
title: Accedere a schemi di inventario (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- columns table
- databases table
- exported metadata
- exporting, schemas of exported metadata
- foreign keys table
- forms table
- indexes, table
- inventory schemas
- macros table
- modules table
- queries table
- reference, inventory schemas
- reports table
- schemas of exported metadata
- schemas, exported metadata
- SSMA_Access_InventoryColumns
- SSMA_Access_InventoryDatabases
- SSMA_Access_InventoryForeignKeys
- SSMA_Access_InventoryForms
- SSMA_Access_InventoryIndexes
- SSMA_Access_InventoryMacros
- SSMA_Access_InventoryModules
- SSMA_Access_InventoryQueries
- SSMA_Access_InventoryReports
- SSMA_Access_InventoryTables
- tables, inventory
ms.assetid: fdd3cff2-4d62-4395-8acf-71ea8f17f524
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c140489877be5f34bc6d7a5b20a4ce36fdb3820f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068951"
---
# <a name="access-inventory-schemas-accesstosql"></a>Schemi di inventario di Access (AccessToSQL)
Le sezioni seguenti descrivono le tabelle che vengono create da SSMA durante l'esportazione degli schemi di accesso per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="databases"></a>Database  
I metadati del database viene esportato per la **SSMA_Access_InventoryDatabases** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|GUID che identifica in modo univoco ogni database. Questa colonna è anche la chiave primaria per la tabella.|  
|**DatabaseName**|**nvarchar(4000)**|Il nome del database di Access.|  
|**ExportTime**|**datetime**|Data e ora di che creazione di questi metadati da SSMA.|  
|**FilePath**|**nvarchar(4000)**|Il nome di file e percorso completo del database di Access.|  
|**FileSize**|**bigint**|Le dimensioni del database di Access in KB.|  
|**FileOwner**|**nvarchar(4000)**|L'account Windows specificato come proprietario del database di Access.|  
|**DateCreated**|**datetime**|Data e ora di che creazione del database di Access.|  
|**DateModified**|**datetime**|Data e ora che dell'ultima modifica apportata al database di Access.|  
|**TablesCount**|**int**|Il numero di tabelle nel database di Access.|  
|**QueriesCount**|**int**|Il numero di query del database di Access.|  
|**FormsCount**|**int**|Il numero di moduli nel database di Access.|  
|**ModulesCount**|**int**|Il numero di moduli nel database di Access.|  
|**ReportsCount**|**int**|Il numero di report nel database di Access.|  
|**MacrosCount**|**int**|Il numero di macro nel database di Access.|  
|**AccessVersion**|**nvarchar(4000)**|La versione di accesso del database.|  
|**Regole di confronto**|**nvarchar(4000)**|Le regole di confronto del database di Access. Regole di confronto determinano come un database Ordina e confronta le stringhe.|  
|**JetVersion**|**nvarchar(4000)**|La versione del motore di database Jet. Accedere ai database utilizzano il motore di database Jet sottostante.|  
|**IsUpdatable**|**bit**|Indica se il database può essere aggiornato. Se il valore è 1, il database è aggiornabile. Se il valore è 0, il database è di sola lettura.|  
|**QueryTimeout**|**int**|Configurato ODBC query valore di timeout per il database, in secondi. Il valore predefinito è 60 secondi.|  
  
## <a name="tables"></a>Tabelle  
Metadati della tabella vengono esportati per il **SSMA_Access_InventoryTables** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database che contiene questa tabella.|  
|**TableId**|**uniqueidentifier**|GUID che identifica in modo univoco la tabella. Questa colonna è anche la chiave primaria per la tabella.|  
|**TableName**|**nvarchar(4000)**|Nome della tabella.|  
|**RowsCount**|**int**|Numero di righe della tabella.|  
|**ValidationRule**|**nvarchar(4000)**|La regola che definisce un input valido per la tabella. Se è presente alcuna regola di convalida, il campo conterrà una stringa vuota.|  
|**LinkedTable**|**nvarchar(4000)**|Un'altra tabella, se presente, che è collegata con la tabella. Collegamento delle tabelle consente aggiunte, eliminazioni e gli aggiornamenti a altra tabella mediante questa tabella.|  
|**ExternalSource**|**nvarchar(4000)**|L'origine dati, se presente, che è associata alla tabella. Se una tabella collegata, ha un'origine dati esterna specificata in questo campo.|  
  
## <a name="columns"></a>Colonne  
I metadati della colonna viene esportato per la **SSMA_Access_InventoryColumns** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database che contiene questa colonna.|  
|**TableId**|**uniqueidentifier**|Identifica la tabella che contiene questa colonna.|  
|**ColumnId**|**int**|Incremento valore intero che identifica la colonna. **ColumnId** è la chiave primaria per la tabella.|  
|**ColumnName**|**nvarchar(4000)**|Nome della colonna.|  
|**IsNullable**|**bit**|Specifica se la colonna può contenere valori null. Se il valore è 1, la colonna può contenere valori null. Se il valore è 0, la colonna non può contenere valori null. Si noti che la regola di convalida può anche essere usata per impedire valori null.|  
|**DataType**|**nvarchar(4000)**|Digitare l'accesso ai dati della colonna, ad esempio **testo** oppure **lungo**.|  
|**IsAutoIncrement**|**bit**|Specifica se la colonna viene incrementato automaticamente i valori interi. Se il valore è 1, i numeri interi sono a incremento automatico.|  
|**Ordinal**|**smallint**|L'ordine della colonna nella tabella, a partire da zero.|  
|**DefaultValue**|**nvarchar(4000)**|Il valore predefinito per la colonna.|  
|**ValidationRule**|**nvarchar(4000)**|La regola che consente di convalidare i dati aggiunti o aggiornati nella colonna.|  
  
## <a name="indexes"></a>Indici  
I metadati dell'indice viene esportato per la **SSMA_Access_InventoryIndexes** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database che contiene questo indice.|  
|**TableId**|**uniqueidentifier**|Identifica la tabella che contiene questo indice.|  
|**IndexId**|**int**|Incremento valore intero che identifica l'indice. Questa colonna è la chiave primaria per la tabella.|  
|**IndexName**|**nvarchar(4000)**|Nome dell'indice.|  
|**ColumnsIncluded**|**nvarchar(4000)**|Elenca le colonne incluse nell'indice. I nomi delle colonne sono separati da un punto e virgola.|  
|**IsUnique**|**bit**|Specifica se ogni elemento in corrispondenza dell'indice deve essere univoco. In un indice multicolonna, la combinazione di valori deve essere univoca. Se il valore è 1, l'indice applica valori univoci.|  
|**IsPK**|**bit**|Specifica se l'indice è stato creato automaticamente come parte della definizione di chiave primaria.|  
|**IsClustered**|**bit**|Specifica se l'indice è cluster. Un indice cluster Riordina l'archiviazione fisica dei dati. Una tabella può avere un solo indice cluster.|  
  
## <a name="foreign-keys"></a>Chiavi esterne  
I metadati della chiave esterno viene esportato per la **SSMA_Access_InventoryForeignKeys** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database che contiene il vincolo foreign key.|  
|**TableId**|**uniqueidentifier**|Identifica la tabella che contiene il vincolo foreign key.|  
|**ForeignKeyId**|**int**|Incremento valore intero che identifica la chiave esterna. Questa colonna è la chiave primaria per la tabella.|  
|**ForeignKeyName**|**nvarchar(4000)**|Nome dell'indice.|  
|**ReferencedTableId**|**uniqueidentifier**|Identifica la tabella che contiene le colonne di origine.|  
|**SourceColumns**|**nvarchar(4000)**|Elenca le colonne di chiave esterna o di colonne.|  
|**ReferencedColumns**|**nvarchar(4000)**|Elenca la colonna chiave primaria o le colonne che fanno riferimento alla chiave esterna.|  
|**IsCascadeForUpdate**|**bit**|Specifica che, se il valore della chiave primaria viene aggiornato, vengono aggiornate anche tutte le righe che fanno riferimento a tale valore della chiave.|  
|**IsCascadeForDelete**|**bit**|Specifica che, se il valore della chiave primaria viene eliminato, vengono eliminate anche tutte le righe che fanno riferimento a tale valore della chiave.|  
|**IsEnforced**|**bit**|Specifica che il vincolo foreign key verrà applicato.|  
  
## <a name="queries"></a>Query  
Query metadati vengono esportati nel **SSMA_Access_InventoryQueries** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database contenente la query.|  
|**QueryId**|**int**|Incremento valore intero che identifica la query. Questa colonna è la chiave primaria per la tabella.|  
|**QueryName**|**nvarchar(4000)**|Nome della query.|  
|**QueryText**|**nvarchar(4000)**|Il codice query SQL, ad esempio un'istruzione SELECT.|  
|**IsUpdateable**|**bit**|Specifica se la query è di sola lettura o aggiornabili.|  
|**QueryType**|**nvarchar(4000)**|Specifica il tipo di query, ad esempio **selezionate** oppure **SetOperation**.|  
|**ExternalSource**|**nvarchar(4000)**|Se la query fa riferimento a un'origine dati esterna, questa è la stringa di connessione usata dalla query.|  
  
## <a name="forms"></a>Form  
I metadati di modulo vengono esportati per il **SSMA_Access_InventoryForms** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database che contiene questo modulo.|  
|**FormId**|**int**|Incremento valore intero che identifica il modulo. Questa colonna è la chiave primaria per la tabella.|  
|**FormName**|**nvarchar(4000)**|Nome del form.|  
  
## <a name="macros"></a>Macro  
Metadati della macro vengono esportati per il **SSMA_Access_InventoryMacros** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database che contiene la macro.|  
|**MacroId**|**int**|Incremento valore intero che identifica la macro. Questa colonna è la chiave primaria per la tabella.|  
|**Nomemacro**|**nvarchar(4000)**|Il nome della macro.|  
  
## <a name="reports"></a>Report  
I metadati del report viene esportato per la **SSMA_Access_InventoryReports** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database che contiene il report.|  
|**ReportId**|**int**|Incremento valore intero che identifica il report. Questa colonna è la chiave primaria per la tabella.|  
|**NomeReport**|**nvarchar(4000)**|Nome del report.|  
  
## <a name="modules"></a>Moduli  
I metadati di modulo vengono esportati per il **SSMA_Access_InventoryModules** tabella. Questa tabella contiene le colonne seguenti:  
  
|Nome colonna|Tipo di dati|Descrizione|  
|---------------|-------------|---------------|  
|**DatabaseId**|**uniqueidentifier**|Identifica il database che contiene il modulo.|  
|**ModuleId**|**int**|Incremento valore intero che identifica il modulo. Questa colonna è la chiave primaria per la tabella.|  
|**ModuleName**|**nvarchar(4000)**|Il nome del modulo.|  
  
## <a name="see-also"></a>Vedere anche  
[Esportazione di un inventario di Access](exporting-an-access-inventory-accesstosql.md)  
  
