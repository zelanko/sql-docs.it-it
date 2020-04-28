---
title: Chiamata di SQLSetPos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306242"
---
# <a name="calling-sqlsetpos"></a>Chiamata di SQLSetPos
In ODBC *2. x*, il puntatore alla matrice di stato della riga era un argomento di **SQLExtendedFetch**. La matrice di stato della riga è stata aggiornata in un secondo momento da una chiamata a **SQLSetPos**. Alcuni driver si basano sul fatto che questa matrice non cambia tra **SQLExtendedFetch** e **SQLSetPos**. In ODBC *3. x*il puntatore alla matrice di stato è un campo del descrittore e pertanto l'applicazione può modificarla in modo che punti a una matrice diversa. Questo può costituire un problema quando un'applicazione ODBC *3. x* utilizza un driver ODBC *2. x* ma chiama **SQLSetStmtAttr** per impostare il puntatore di stato della matrice e chiama **SQLFetchScroll** per recuperare i dati. Gestione driver esegue il mapping come una sequenza di chiamate a **SQLExtendedFetch**. Nel codice seguente, in genere viene generato un errore quando Gestione driver esegue il mapping della seconda chiamata **SQLSetStmtAttr** quando si utilizza un driver ODBC *2. x* :  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 L'errore viene generato se non è possibile modificare il puntatore dello stato della riga in ODBC *2. x* tra le chiamate a **SQLExtendedFetch**. Al contrario, gestione driver esegue i passaggi seguenti quando si utilizza un driver ODBC *2. x* :  
  
1.  Inizializza un flag di gestione driver interno *fSetPosError* su true.  
  
2.  Quando un'applicazione chiama **SQLFetchScroll**, gestione driver imposta *fSetPosError* su false.  
  
3.  Quando l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR, gestione driver imposta *FSETPOSERROR* uguale a true.  
  
4.  Quando l'applicazione chiama **SQLSetPos**, con *FSETPOSERROR* uguale a true, gestione driver genera SQL_ERROR con SQLState HY011 (non è possibile impostare l'attributo) per indicare che l'applicazione ha tentato di chiamare **SQLSetPos** dopo aver modificato il puntatore dello stato della riga, ma prima di chiamare **SQLFetchScroll**.
