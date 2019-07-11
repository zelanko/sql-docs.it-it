---
title: Funzione SQLSetScrollOptions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e0c2a9c367df9cd71d68d73ff676c8df915237b
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793876"
---
# <a name="sqlsetscrolloptions-function"></a>Funzione SQLSetScrollOptions
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: Funzionalità deprecate  
  
 **Riepilogo**  
 In ODBC *3.x*, la funzione ODBC 2.0 **SQLSetScrollOptions** è stato sostituito dalle chiamate a **SQLGetInfo** e **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Per altre informazioni su cosa the Driver Manager esegue il mapping a questa funzione quando un'applicazione ODBC *2.x* applicazione funziona con un database ODBC *3.x* driver, vedere [Mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
> 
> [!NOTE]
>  Quando esegue il mapping di gestione Driver **SQLSetScrollOptions** per un'applicazione che utilizza un database ODBC *3.x* driver che non supporta **SQLSetScrollOptions**, il Driver Manager imposta l'opzione dell'istruzione SQL_ROWSET_SIZE, non l'attributo di istruzione SQL_ATTR_ROW_ARRAY_SIZE sul *RowsetSize* nell'argomento **SQLSetScrollOption**. Ne consegue **SQLSetScrollOptions** non può essere utilizzato da un'applicazione durante il recupero di più righe da una chiamata a **SQLFetch** oppure **SQLFetchScroll**. Può essere utilizzato solo quando più durante il recupero di righe da una chiamata a **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Note  
 Se l'applicazione verrà eseguita in un sistema operativo a 64 bit, vedere [le informazioni ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
