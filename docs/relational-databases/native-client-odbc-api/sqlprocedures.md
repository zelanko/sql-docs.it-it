---
title: SQLProcedures | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLProcedures function
ms.assetid: ec41f017-f5e0-40ef-913a-65d206068631
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a2b8d05b17507c5e8c940e1fa324decd5c0c5db1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68131225"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Tutte le stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituiscono un valore. **SQLProcedures** riporta SQL_PT_FUNCTION per il set di risultati PROCEDURE_TYPE colonna.  
  
 **SQLProcedures** restituisce SQL_SUCCESS se esistono o meno valori per *CatalogName, SchemaName* oppure *ProcName* parametri. **SQLFetch** restituisce SQL_NO_DATA quando in questi parametri vengono utilizzati valori non validi.  
  
 **SQLProcedures** può essere eseguito su un cursore server statico. Un tentativo di eseguire **SQLProcedures** su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO che indica che il tipo di cursore è stato modificato.  
  
 **SQLProcedures** restituisce informazioni sulle procedure i cui nomi corrispondono *ProcName* e può essere eseguito dall'utente corrente o per cui l'utente corrente dispone dell'autorizzazione VIEW DEFINITION.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLProcedures](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
