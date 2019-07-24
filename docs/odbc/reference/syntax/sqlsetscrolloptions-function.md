---
title: Funzione SQLSetScrollOptions | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 77a85caefadb54c3db2716c4db18b504e02da996
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/19/2019
ms.locfileid: "68342935"
---
# <a name="sqlsetscrolloptions-function"></a>Funzione SQLSetScrollOptions
**Conformità**  
 Versione introdotta: Conformità agli standard ODBC 1,0: Funzionalità deprecate  
  
 **Riepilogo**  
 In ODBC *3. x*, la funzione ODBC 2,0 **SQLSetScrollOptions** è stata sostituita dalle chiamate a **SQLGetInfo** e **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Per ulteriori informazioni su ciò che Gestione driver esegue il mapping di questa funzione a quando un'applicazione ODBC *2. x* utilizza un driver ODBC *3. x* , vedere [mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) nell'appendice G: Linee guida driver per la compatibilità con le versioni precedenti.  
> 
> [!NOTE]
>  Quando Gestione driver esegue il mapping di **SQLSetScrollOptions** per un'applicazione che utilizza un driver ODBC *3. x* che non supporta **SQLSetScrollOptions**, gestione driver imposta l'opzione dell'istruzione SQL_ROWSET_SIZE, non il SQL_ATTR_ROW_ Attributo dell'istruzione ARRAY_SIZE, per l'argomento *RowsetSize* in **SQLSetScrollOption**. Di conseguenza, **SQLSetScrollOptions** non può essere utilizzato da un'applicazione durante il recupero di più righe mediante una chiamata  a SQLFetch o **SQLFetchScroll**. Può essere utilizzato solo quando si recuperano più righe tramite una chiamata a **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Note  
 Se l'applicazione viene eseguita su un sistema operativo a 64 bit, vedere [informazioni su ODBC 64-bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni di riferimento sulle API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
