---
title: Comportamenti del cursore Documenti Microsoft
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2e3400e52cd0b7574c07a3cf813b4cbca317df2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305478"
---
# <a name="cursor-behaviors"></a>Comportamenti dei cursori
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  ODBC supporta le opzioni ISO per la specifica del comportamento dei cursori mediante lo scorrimento e la sensibilità. Questi comportamenti vengono specificati impostando le opzioni SQL_ATTR_CURSOR_SCROLLABLE e SQL_ATTR_CURSOR_SENSITIVITY su una chiamata a [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa queste opzioni richiedendo cursori server con le caratteristiche seguenti.  
  
|Impostazioni del comportamento del cursore|Caratteristiche del cursore server richieste|  
|------------------------------|---------------------------------------------|  
|SQL_SCROLLABLE e SQL_SENSITIVE|Cursore gestito da keyset e concorrenza ottimistica basata sulla versione|  
|SQL_SCROLLABLE e SQL_INSENSITIVE|Cursore statico e concorrenza di sola lettura|  
|SQL_SCROLLABLE e SQL_UNSPECIFIED|Cursore statico e concorrenza di sola lettura|  
|SQL_NONSCROLLABLE e SQL_SENSITIVE|Cursore forward-only e concorrenza ottimistica basata sulla versione|  
|SQL_NONSCROLLABLE e SQL_INSENSITIVE|Set di risultati predefinito (forward only, di sola lettura)|  
|SQL_NONSCROLLABLE e SQL_UNSPECIFIED|Set di risultati predefinito (forward only, di sola lettura)|  
  
 La concorrenza ottimistica basata sulla versione richiede una colonna **timestamp** nella tabella sottostante. Se il controllo della concorrenza ottimistica basato sulla versione viene richiesto in una tabella che non dispone di una colonna **timestamp,** il server utilizza la concorrenza ottimistica basata sui valori.  
  
## <a name="scrollability"></a>Scorrimento  
 Quando SQL_ATTR_CURSOR_SCROLLABLE è impostato su SQL_SCROLLABLE, il cursore supporta tutti i diversi valori per il parametro *FetchOrientation* di [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md). Quando SQL_ATTR_CURSOR_SCROLLABLE è impostato su SQL_NONSCROLLABLE, il cursore supporta solo un *FetchOrientation* valore di SQL_FETCH_NEXT.  
  
## <a name="sensitivity"></a>Sensibilità  
 Quando SQL_ATTR_CURSOR_SENSITIVITY è impostato su SQL_SENSITIVE, il cursore riflette le modifiche dei dati apportate dall'utente corrente di cui è stato eseguito il commit da altri utenti. Quando SQL_ATTR_CURSOR_SENSITIVITY è impostato su SQL_INSENSITIVE, il cursore non riflette le modifiche dei dati.  
  
## <a name="see-also"></a>Vedere anche  
 Utilizzo delle [proprietà cursori](properties/cursor-properties.md) [(ODBC)](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md) 
  
  
