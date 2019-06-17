---
title: SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0001f1d6e45e855b884028a595a2b61263c2e58
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63046684"
---
# <a name="sqlprocedures"></a>SQLProcedures
  Tutte le stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituiscono un valore. **SQLProcedures** riporta SQL_PT_FUNCTION per il set di risultati PROCEDURE_TYPE colonna.  
  
 **SQLProcedures** restituisce SQL_SUCCESS se esistono o meno valori per *CatalogName, SchemaName* oppure *ProcName* parametri. **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 **SQLProcedures** può essere eseguito su un cursore server statico. Un tentativo di eseguire **SQLProcedures** su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 **SQLProcedures** restituisce informazioni sulle procedure i cui nomi corrispondono *ProcName* e può essere eseguito dall'utente corrente o per cui l'utente corrente dispone dell'autorizzazione VIEW DEFINITION.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLProcedures](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
