---
title: Proprietà SQLProcedureColumns . Documenti Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1b942126a5ad73d5c41f28f60a63d22ef8584f24
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280058"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLProcedureColumns** restituisce una riga che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] segnala gli attributi del valore restituito di tutte le stored procedure.  
  
 **SQLProcedureColumns** restituisce SQL_SUCCESS se esistono o meno valori per i parametri *CatalogName*, *SchemaName*, *ProcName*o *ColumnName* . **SQLFetch** restituisce SQL_NO_DATA quando vengono utilizzati valori non validi in questi parametri.  
  
 **SQLProcedureColumns** può essere eseguito su un cursore server statico. Un tentativo di eseguire **SQLProcedureColumns** su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 Nella tabella seguente sono elencate le colonne restituite dal set di risultati **xml** e il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] modo in cui sono state estese per gestire i tipi di dati **udt** e xml tramite il driver ODBC Native Client:  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|Restituisce il nome del catalogo contenente il tipo definito dall'utente.|  
|SS_UDT_SCHEMA_NAME|Restituisce il nome dello schema contenente il tipo definito dall'utente.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Restituisce il nome completo dell'assembly del tipo definito dall'utente.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Restituisce il nome del catalogo nel quale è definito il nome di una raccolta di XML Schema. Se non è possibile trovare il nome del catalogo, questa variabile contiene una stringa vuota.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Restituisce il nome dello schema nel quale è definito il nome di una raccolta di XML Schema. Se non è possibile trovare il nome dello schema, questa variabile contiene una stringa vuota.|  
|SS_XML_SCHEMACOLLECTION_NAME|Restituisce il nome di una raccolta di XML Schema. Se non è possibile trovare il nome, questa variabile contiene una stringa vuota.|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns e parametri con valori di tabella  
 SQLProcedureColumns gestisce i parametri con valori di tabella in modo simile ai tipi CLR definiti dall'utente. Nelle righe restituite per i parametri con valori di tabella le colonne presentano i valori seguenti:  
  
|Nome colonna|Descrizione/valore|  
|-----------------|------------------------|  
|DATA_TYPE|SQL_SS_TABLE|  
|TYPE_NAME|Nome del tipo di tabella per il parametro con valori di tabella.|  
|COLUMN_SIZE|NULL|  
|BUFFER_LENGTH|0|  
|DECIMAL_DIGITS|Il numero delle colonne presenti nel parametro con valori di tabella.|  
|NUM_PREC_RADIX|NULL|  
|NULLABLE|SQL_NULLABLE|  
|REMARKS|NULL|  
|COLUMN_DEF|NULL I tipi di tabella potrebbero non avere valori predefiniti.|  
|SQL_DATA_TYPE|SQL_SS_TABLE|  
|SQL_DATEIME_SUB|NULL|  
|CHAR_OCTET_LENGTH|NULL|  
|IS_NULLABLE|"YES"|  
|SS_TYPE_CATALOG_NAME|Restituisce il nome del catalogo contenente la tabella o il tipo CLR definito dall'utente.|  
|SS_TYPE_SCHEMA_NAME|Restituisce il nome dello schema contenente la tabella o il tipo CLR definito dall'utente.|  
  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive sono disponibili le colonne SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME per restituire rispettivamente il catalogo e lo schema per i parametri con valori di tabella. Tali colonne vengono popolate per i parametri con valori di tabella e anche per i parametri del tipo CLR definito dall'utente. Questa funzionalità aggiuntiva non influenza le colonne di catalogo e di schema esistenti per i parametri del tipo CLR definito dall'utente. Vengono popolate anche per mantenere la compatibilità con le versioni precedenti.  
  
 In conformità con la specifica ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME vengono visualizzati prima di tutte le colonne specifiche del driver che sono state aggiunte nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dopo tutte le colonne richieste da ODBC stesso.  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere Parametri con valori di [tabella &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>Supporto di SQLProcedureColumns per le caratteristiche avanzate di data e ora  
 Per i valori restituiti per i tipi di data/ora, vedere [Metadati del catalogo](../../relational-databases/native-client-odbc-date-time/metadata-catalog.md).  
  
 Per ulteriori informazioni generali, vedere Miglioramenti di [data e ora &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>Supporto di SQLProcedureColumns per tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLProcedureColumns** supporta tipi CLR definiti dall'utente (UDT) di grandi dimensioni. Per ulteriori informazioni, vedere [Tipi CLR di grandi dimensioni definiti dall'utente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLProcedureColumnsSQLProcedureColumns Function](https://go.microsoft.com/fwlink/?LinkId=59363)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
