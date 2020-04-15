---
title: Funzione SQLSetScrollOptions . Documenti Microsoft
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 056fc203581e1d5d8323b09ac62d692093d8c0f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287268"
---
# <a name="sqlsetscrolloptions-function"></a>Funzione SQLSetScrollOptions
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: Deprecated  
  
 **Riepilogo**  
 In ODBC *3.x*la funzione ODBC 2.0 **SQLSetScrollOptions** è stata sostituita da chiamate a **SQLGetInfo** e **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Per ulteriori informazioni su ciò che Gestione Driver esegue il mapping di questa funzione a quando un'applicazione ODBC *2.x* utilizza un driver ODBC *3.x,* vedere mapping di [funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) nell'appendice G: Linee guida del driver per la compatibilità con le versioni precedenti.  
> 
> [!NOTE]
>  Quando Gestione Driver esegue il mapping di **SQLSetScrollOptions** per un'applicazione che utilizza un driver ODBC *3.x* che non supporta **SQLSetScrollOptions**, Gestione Driver imposta l'opzione di istruzione SQL_ROWSET_SIZE, non l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE , per il *RowsetSize* argomento **SQLSetScrollOption**. Di conseguenza, **SQLSetScrollOptions** non può essere utilizzato da un'applicazione durante il recupero di più righe da una chiamata a **SQLFetch** o **SQLFetchScroll**. e può essere utilizzato solo quando si recuperano più righe mediante una chiamata a **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Osservazioni  
 Se l'applicazione verrà eseguita in un sistema operativo a 64 bit, vedere [Informazioni a 64 bit ODBC](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
