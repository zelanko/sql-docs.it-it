---
title: SQLProcedureColumns | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedureColumns function
ms.assetid: 6671e180-0072-4de5-90f5-314306d2ba9c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 21c0a7248f2e8c5313678f503b239cdf44d16ea7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046716"
---
# <a name="sqlprocedurecolumns"></a>SQLProcedureColumns
  `SQLProcedureColumns`Restituisce una riga che riporta gli attributi del valore restituito [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di tutte le stored procedure.  
  
 `SQLProcedureColumns`restituisce SQL_SUCCESS se sono presenti o meno valori per i parametri *CatalogName*, *SchemaName*, *ProcName*o *ColumnName* . **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 
  `SQLProcedureColumns` può essere eseguito in un cursore del server statico. Un tentativo di eseguire `SQLProcedureColumns` in un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO, che indica che il tipo di cursore è stato modificato.  
  
 Nella tabella seguente sono elencate le colonne restituite dal set di risultati e il modo in cui sono state estese **** per gestire i tipi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dati **UDT** e XML tramite il driver ODBC di Native Client:  
  
|Nome colonna|Descrizione|  
|-----------------|-----------------|  
|SS_UDT_CATALOG_NAME|Restituisce il nome del catalogo contenente il tipo definito dall'utente.|  
|SS_UDT_SCHEMA_NAME|Restituisce il nome dello schema contenente il tipo definito dall'utente.|  
|SS_UDT_ASSEMBLY_TYPE_NAME|Restituisce il nome completo dell'assembly del tipo definito dall'utente.|  
|SS_XML_SCHEMACOLLECTION_CATALOG_NAME|Restituisce il nome del catalogo nel quale è definito il nome di una raccolta di XML Schema. Se non è possibile trovare il nome del catalogo, questa variabile contiene una stringa vuota.|  
|SS_XML_SCHEMACOLLECTION_SCHEMA_NAME|Restituisce il nome dello schema nel quale è definito il nome di una raccolta di XML Schema. Se non è possibile trovare il nome dello schema, questa variabile contiene una stringa vuota.|  
|SS_XML_SCHEMACOLLECTION_NAME|Restituisce il nome di una raccolta di XML Schema. Se non è possibile trovare il nome, questa variabile contiene una stringa vuota.|  
  
## <a name="sqlprocedurecolumns-and-table-valued-parameters"></a>SQLProcedureColumns e parametri con valori di tabella  
 SQLProcedureColumns gestisce i parametri con valori di tabella in modo analogo ai tipi CLR definiti dall'utente. Nelle righe restituite per i parametri con valori di tabella le colonne presentano i valori seguenti:  
  
|Nome colonna|Descrizione/valore|  
|-----------------|------------------------|  
|DATA_TYPE|SQL_SS_TABLE|  
|TYPE_NAME|Nome del tipo di tabella per il parametro con valori di tabella.|  
|COLUMN_SIZE|NULL|  
|BUFFER_LENGTH|0|  
|DECIMAL_DIGITS|Il numero delle colonne presenti nel parametro con valori di tabella.|  
|NUM_PREC_RADIX|NULL|  
|NULLABLE|SQL_NULLABLE|  
|OSSERVAZIONI|NULL|  
|COLUMN_DEF|NULL. I tipi di tabella potrebbero non avere valori predefiniti.|  
|SQL_DATA_TYPE|SQL_SS_TABLE|  
|SQL_DATEIME_SUB|NULL|  
|CHAR_OCTET_LENGTH|NULL|  
|IS_NULLABLE|"YES"|  
|SS_TYPE_CATALOG_NAME|Restituisce il nome del catalogo contenente la tabella o il tipo CLR definito dall'utente.|  
|SS_TYPE_SCHEMA_NAME|Restituisce il nome dello schema contenente la tabella o il tipo CLR definito dall'utente.|  
  
 In [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive sono disponibili le colonne SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME per restituire rispettivamente il catalogo e lo schema per i parametri con valori di tabella. Tali colonne vengono popolate per i parametri con valori di tabella e anche per i parametri del tipo CLR definito dall'utente. Questa funzionalità aggiuntiva non influenza le colonne di catalogo e di schema esistenti per i parametri del tipo CLR definito dall'utente. Vengono popolate anche per mantenere la compatibilità con le versioni precedenti.  
  
 In conformità con la specifica ODBC, SS_TYPE_CATALOG_NAME e SS_TYPE_SCHEMA_NAME vengono visualizzati prima di tutte le colonne specifiche del driver che sono state aggiunte nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e dopo tutte le colonne richieste da ODBC stesso.  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-enhanced-date-and-time-features"></a>Supporto di SQLProcedureColumns per le caratteristiche avanzate di data e ora  
 Per i valori restituiti per i tipi data/ora, vedere [metadati del catalogo](../native-client-odbc-date-time/metadata-catalog.md).  
  
 Per informazioni più generali, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlprocedurecolumns-support-for-large-clr-udts"></a>Supporto di SQLProcedureColumns per tipi CLR definiti dall'utente di grandi dimensioni  
 
  `SQLProcedureColumns` supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi CLR definiti dall'utente di grandi dimensioni &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLProcedureColumns (funzione)](https://go.microsoft.com/fwlink/?LinkId=59363)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
