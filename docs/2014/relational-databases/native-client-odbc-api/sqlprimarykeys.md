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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: bf00ecd74b64b3910ba19365920baf914f86939c
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82705893"
---
# <a name="sqlprimarykeys"></a>SQLPrimaryKeys
  Una tabella potrebbe includere una colonna o colonne che possono essere utilizzate come identificatori di riga univoci, mentre le tabelle create senza un vincolo PRIMARY KEY restituiscono un set di risultati vuoto a SQLPrimaryKeys. La funzione ODBC [SQLSpecialColumns](sqlspecialcolumns.md) segnala l'identificatore di riga candidati per le tabelle senza chiavi primarie.  
  
 SQLPrimaryKeys restituisce SQL_SUCCESS se sono presenti o meno valori per i parametri *CatalogName*, *SchemaName*o *TableName* . SQLFetch restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 SQLPrimaryKeys può essere eseguito su un cursore del server statico. Il tentativo di eseguire SQLPrimaryKeys su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO indicante che il tipo di cursore è stato modificato.  
  
 Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta la segnalazione di informazioni per le tabelle nei server collegati accettando un nome in due parti per il parametro *CatalogName* : *linked_server_name. catalog_name*.  
  
## <a name="sqlprimarykeys-and-table-valued-parameters"></a>SQLPrimaryKeys e parametri con valori di tabella  
 Se l'attributo dell'istruzione SQL_SOPT_SS_NAME_SCOPE ha il valore SQL_SS_NAME_SCOPE_TABLE_TYPE, anziché il valore predefinito di SQL_SS_NAME_SCOPE_TABLE, SQLPrimaryKeys restituirà informazioni sulle colonne chiave primaria dei tipi di tabella. Per ulteriori informazioni su SQL_SOPT_SS_NAME_SCOPE, vedere [SQLSetStmtAttr](sqlsetstmtattr.md).  
  
 Per ulteriori informazioni sui parametri con valori di tabella, vedere [parametri con valori di tabella &#40;&#41;ODBC ](../native-client-odbc-table-valued-parameters/table-valued-parameters-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLPrimaryKeys (funzione)](https://go.microsoft.com/fwlink/?LinkId=59361)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
