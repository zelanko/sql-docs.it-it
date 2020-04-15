---
title: Chiamata a SQLSetPos . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSetPos
- SQLSetPos function [ODBC], calling
- upgrading applications [ODBC], SQLSetPos
- backward compatibility [ODBC], SqlSetPos
- application upgrades [ODBC], SQLSetPos
ms.assetid: 846354b8-966c-4c2c-b32f-b0c8e649cedd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46cfbb4e2e6b60f620cd7e38272bf9308ece91bc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306242"
---
# <a name="calling-sqlsetpos"></a>Chiamata di SQLSetPos
In ODBC *2.x*il puntatore alla matrice di stato della riga era un argomento di **SQLExtendedFetch**. La matrice di stato della riga è stata successivamente aggiornata da una chiamata a **SQLSetPos**. Alcuni driver si sono affidati al fatto che questa matrice non cambia tra **SQLExtendedFetch** e **SQLSetPos**. In ODBC *3.x*, il puntatore alla matrice di stato è un campo descrittore e pertanto l'applicazione può facilmente modificarlo in modo che punti a una matrice diversa. Questo può essere un problema quando un'applicazione ODBC *3.x* utilizza un driver ODBC *2.x* ma chiama **SQLSetStmtAttr** per impostare il puntatore di stato della matrice e chiama **SQLFetchScroll** per recuperare i dati. Gestione Driver esegue il mapping come una sequenza di chiamate a **SQLExtendedFetch**. Nel codice seguente, viene in genere generato un errore quando Gestione Driver esegue il mapping della seconda chiamata **SQLSetStmtAttr** quando si lavora con un driver ODBC *2.x:*  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 L'errore verrebbe generato se non fosse possibile modificare il puntatore di stato della riga in ODBC *2.x* tra le chiamate a **SQLExtendedFetch**. Invece, Gestione Driver esegue i seguenti passaggi quando si lavora con un driver ODBC *2.x:*  
  
1.  Inizializza un flag interno di Gestione Driver *fSetPosError su* TRUE.  
  
2.  Quando un'applicazione chiama **SQLFetchScroll**, Gestione Driver imposta *fSetPosError* su FALSE.  
  
3.  Quando l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR, Gestione Driver imposta *fSetPosError* uguale aTRUE.  
  
4.  Quando l'applicazione chiama **SQLSetPos**, con *fSetPosError* uguale a TRUE, Gestione Driver genera SQL_ERROR con SQLSTATE HY011 (attributo non può essere impostato ora) per indicare che l'applicazione ha tentato di chiamare **SQLSetPos** dopo aver modificato il puntatore di stato della riga ma prima di chiamare **SQLFetchScroll**.
