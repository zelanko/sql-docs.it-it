---
title: 'Funzione SQLTransact : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTransact
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTransact
helpviewer_keywords:
- SQLTransact function [ODBC]
ms.assetid: 496249e0-8eff-4c60-8358-5543bc3ead9c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c7a4f1da36a7c233e9a1b5832ee83e86a5c1f77d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287081"
---
# <a name="sqltransact-function"></a>Funzione SQLTransact
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: Deprecated  
  
 **Riepilogo**  
 In ODBC *3.x*la funzione ODBC *2.x* **SQLTransact** è stata sostituita da **SQLEndTran**. Per ulteriori informazioni, vedere [SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
> [!NOTE]  
>  L'attributo SQL_ASYNC_DBC_FUNCTION_ENABLE, introdotto in ODBC 3.8, non è supportato da **SQLTransact**. Le applicazioni che utilizzano un'operazione asincrona su un handle di connessione devono utilizzare **SQLEndTran**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
