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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f94b1191815f37728a2d8de8fc1175113644bc5a
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793892"
---
# <a name="calling-sqlsetpos"></a>Chiamata di SQLSetPos
In ODBC *2.x*, il puntatore alla matrice di stato di riga è un argomento per **SQLExtendedFetch**. La matrice di stato di riga in un secondo momento è stata aggiornata da una chiamata a **SQLSetPos**. Alcuni driver sul fatto che questa matrice non viene modificato tra si basavano **SQLExtendedFetch** e **SQLSetPos**. In ODBC *3.x*, il puntatore alla matrice di stato è un campo di descrizione e pertanto l'applicazione può modificare facilmente in modo che punti a un'altra matrice. Può trattarsi di un problema quando un'applicazione ODBC *3.x* applicazione funziona con un database ODBC *2.x* driver, ma viene eseguita la chiamata **SQLSetStmtAttr** per impostare il puntatore dello stato della matrice e chiama  **SQLFetchScroll** per recuperare i dati. Gestione Driver ne esegue il mapping come una sequenza di chiamate a **SQLExtendedFetch**. Nel codice seguente, generato un errore verrebbe normalmente quando viene eseguito il mapping del secondo gestione Driver **SQLSetStmtAttr** chiamare quando si lavora con un database ODBC *2.x* driver:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStatus, 0);  
SQLFetchScroll(hstmt, fFetchType, iRow);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_STATUS_PTR, rgfRowStat1, 0);  
SQLSetPos(hstmt, iRow, fOption, fLock);  
```  
  
 Verrà generato l'errore se si sono verificati alcuna possibilità di modificare il puntatore dello stato della riga in ODBC *2.x* tra le chiamate a **SQLExtendedFetch**. Al contrario, gestione Driver esegue i passaggi seguenti quando si lavora con un database ODBC *2.x* driver:  
  
1.  Inizializza un flag interno di gestione Driver *fSetPosError* su TRUE.  
  
2.  Quando un'applicazione chiama **SQLFetchScroll**, gestione Driver imposta *fSetPosError* su FALSE.  
  
3.  Quando l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR, gestione Driver imposta *fSetPosError* toTRUE uguale.  
  
4.  Quando l'applicazione chiama **SQLSetPos**, con *fSetPosError* uguale a TRUE, gestione Driver genera SQL_ERROR con SQLSTATE HY011 (attributo non può essere impostato a questo punto) per indicare che l'applicazione tentativo di chiamare **SQLSetPos** dopo aver modificato l'indicatore di misura lo stato di riga, ma prima di chiamare **SQLFetchScroll**.
