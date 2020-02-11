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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046684"
---
# <a name="sqlprocedures"></a>SQLProcedures
  Tutte le stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituiscono un valore. **SQLProcedures** restituisce SQL_PT_FUNCTION per la colonna del set di risultati PROCEDURE_TYPE.  
  
 **SQLProcedures** restituisce SQL_SUCCESS se sono presenti o meno valori per i parametri *CatalogName, SchemaName* o *ProcName* . **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 **SQLProcedures** può essere eseguito su un cursore del server statico. Il tentativo di eseguire **SQLProcedures** su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO, a indicare che il tipo di cursore è stato modificato.  
  
 **SQLProcedures** restituisce informazioni su tutte le routine i cui nomi corrispondono a *ProcName* e possono essere eseguite dall'utente corrente o per cui all'utente corrente è stata concessa l'autorizzazione View definition.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLProcedures (funzione)](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
