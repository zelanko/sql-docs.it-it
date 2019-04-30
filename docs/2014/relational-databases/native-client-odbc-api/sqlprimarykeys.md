---
title: SQLPrimaryKeys | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLPrimaryKeys function
ms.assetid: bc61cd5b-d2f4-4f87-abc7-743cf9ea772d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a12392f9e70fec2fae3b7790b43f12779b8868b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63046687"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  Una tabella può includere una o più colonne possono essere usato come identificatori di riga univoci e le tabelle create senza un vincolo PRIMARY KEY restituiscono un set a SQLPrimaryKeys di risultati vuoto. La funzione ODBC [SQLSpecialColumns](sqlspecialcolumns.md) report possibili di identificatori per le tabelle senza chiavi primarie di riga.  
  
 SQLPrimaryKeys restituisce SQL_SUCCESS se esistono o meno valori per *CatalogName*, *SchemaName*, o *TableName* parametri. SQLFetch restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 SQLPrimaryKeys può essere eseguito su un cursore server statico. Un tentativo di eseguire SQLPrimaryKeys su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta la segnalazione di informazioni relative alle tabelle sui server collegati mediante l'accettazione di un nome in due parti per il *CatalogName* parametro: *Linked_server_name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys e parametri con valori di tabella  
 Se l'attributo dell'istruzione SQL_SOPT_SS_NAME_SCOPE è impostato sul valore SQL_SS_NAME_SCOPE_TABLE_TYPE, anziché il valore predefinito di SQL_SS_NAME_SCOPE_TABLE, SQLPrimaryKeys restituisce informazioni sulle colonne chiavi primarie dei tipi di tabella. Per altre informazioni su SQL_SOPT_SS_NAME_SCOPE, vedere [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Per altre informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;ODBC&#41;](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLPrimaryKeys Function](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
