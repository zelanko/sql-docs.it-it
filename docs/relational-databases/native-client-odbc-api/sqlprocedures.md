---
title: Proprietà SQLProcedures . Documenti Microsoft
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 14ff76504c9a36657be60ba4855cf252474071d7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302372"
---
# <a name="sqlprocedures"></a>SQLProcedures
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Tutte le stored procedure di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituiscono un valore. **SQLProcedures** segnala SQL_PT_FUNCTION per il PROCEDURE_TYPE di colonna del set di risultati.  
  
 **SQLProcedures** restituisce SQL_SUCCESS se esistono o meno valori per i parametri *CatalogName, SchemaName* o *ProcName.* **SQLFetch** restituisce SQL_NO_DATA quando vengono utilizzati valori non validi in questi parametri.  
  
 **SQLProcedures** può essere eseguito su un cursore server statico. Un tentativo di eseguire **SQLProcedures** su un cursore aggiornabile (dinamico o keyset) restituirà SQL_SUCCESS_WITH_INFO, a indicare che il tipo di cursore è stato modificato.  
  
 **SQLProcedures** restituisce informazioni su tutte le procedure i cui nomi corrispondono *a ProcName* e possono essere eseguite dall'utente corrente o per le quali all'utente corrente è stata concessa l'autorizzazione VIEW DEFINITION.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLProceduresSQLProcedures Function](https://go.microsoft.com/fwlink/?LinkId=59364)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
