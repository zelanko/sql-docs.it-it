---
title: Comportamenti del cursore | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- version-based optimistic concurrency
- cursors [ODBC], cursor behaviors
- ODBC applications, cursors
- SQL_ATTR_CURSOR_SENSITIVITY option
- SQL_ATTR_CURSOR_SCROLLABLE option
- sensitivity behavior of cursor
- ODBC cursors, cursor behaviors
ms.assetid: 742ddcd2-232b-4aa1-9212-027df120ad35
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c5ded9f42da267cfd137f0adfd4465d965d9a06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63188568"
---
# <a name="cursor-behaviors"></a>Comportamenti dei cursori
  ODBC supporta le opzioni ISO per la specifica del comportamento dei cursori mediante lo scorrimento e la sensibilità. Questi comportamenti vengono specificati impostando le opzioni SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY in una chiamata a [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md). Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa queste opzioni richiedendo cursori server con le caratteristiche seguenti.  
  
|Impostazioni del comportamento del cursore|Caratteristiche del cursore server richieste|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE e SQL_SENSITIVE|Cursore gestito da keyset e concorrenza ottimistica basata sulla versione|  
|SQL_SCROLLABLE e SQL_INSENSITIVE|Cursore statico e concorrenza di sola lettura|  
|SQL_SCROLLABLE e SQL_UNSPECIFIED|Cursore statico e concorrenza di sola lettura|  
|SQL_NONSCROLLABLE e SQL_SENSITIVE|Cursore forward-only e concorrenza ottimistica basata sulla versione|  
|SQL_NONSCROLLABLE e SQL_INSENSITIVE|Set di risultati predefinito (forward only, di sola lettura)|  
|SQL_NONSCROLLABLE e SQL_UNSPECIFIED|Set di risultati predefinito (forward only, di sola lettura)|  
  
 Per la concorrenza ottimistica basata sulla versione è richiesta una colonna **timestamp** nella tabella sottostante. Se è richiesto il controllo della concorrenza ottimistica basata sulla versione in una tabella che non dispone di una colonna di tipo **timestamp** , il server utilizza la concorrenza ottimistica basata sui valori.  
  
## <a name="scrollability"></a>Scorrimento  
 Quando SQL_ATTR_CURSOR_SCROLLABLE è impostato su SQL_SCROLLABLE, il cursore supporta tutti i valori diversi per il parametro *FetchOrientation* di [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md). Quando SQL_ATTR_CURSOR_SCROLLABLE è impostato su SQL_NONSCROLLABLE, il cursore supporta solo un valore *FetchOrientation* di SQL_FETCH_NEXT.  
  
## <a name="sensitivity"></a>Sensibilità  
 Quando SQL_ATTR_CURSOR_SENSITIVITY è impostato su SQL_SENSITIVE, il cursore riflette le modifiche dei dati apportate dall'utente corrente di cui è stato eseguito il commit da altri utenti. Quando SQL_ATTR_CURSOR_SENSITIVITY è impostato su SQL_INSENSITIVE, il cursore non riflette le modifiche dei dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di cursori &#40;&#41;ODBC](using-cursors-odbc.md)  
  
  
