---
title: Aggiunta di segnalibri righe in ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- ODBC cursors, scrolling rows
- bookmarks [ODBC]
ms.assetid: 9cfcd243-c9d4-4c2a-abc4-399dbabe5f6b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d58ce5236a2d74e1749e88f0bffa9ca86f974733
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62740051"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>Scorrimento e recupero di righe - Applicazione di segnalibri alle righe in ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Un segnalibro è un valore utilizzato per identificare una riga di dati. Il significato del valore del segnalibro è noto solo al driver o all'origine dati. Un segnalibro, ad esempio, può essere tanto semplice quanto un numero di riga o tanto complesso quanto un indirizzo del disco. In ODBC l'applicazione richiede un segnalibro per una determinata riga, lo archivia e lo passa nuovamente al cursore per tornare alla riga.  
  
 Durante il recupero di righe con [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md), un'applicazione può utilizzare un segnalibro come base per la selezione della riga iniziale. Si tratta di una forma di indirizzamento assoluto, in quanto non dipende dalla posizione del cursore corrente. Scorrere fino a una riga con segnalibro, l'applicazione chiama **SQLFetchScroll** con un *FetchOrientation* impostato su sql_fetch_bookmark. Questa operazione utilizza il segnalibro a cui punta l'attributo dell'opzione SQL_ATTR_FETCH_BOOKMARK_PTR. L'operazione restituisce il set di righe che inizia con la riga identificata dal segnalibro. Un'applicazione può specificare un offset per questa operazione nel *FetchOffset* argomento della chiamata a **SQLFetchScroll**. Quando viene specificato un offset, la prima riga del set di righe restituita è determinata dall'aggiunta del numero nell'argomento FetchOffset al numero della riga identificata dal segnalibro. Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta solo segnalibri su cursori statici e keyset. Se viene richiesto un cursore dinamico quando si impostano segnalibri, viene invece aperto un cursore keyset.  
  
 I segnalibri sono anche utilizzabile con il **SQLBulkOperations** funzione per eseguire operazioni su un set di righe a partire dal segnalibro.  
  
## <a name="see-also"></a>Vedere anche  
 [Scorrimento e recupero di righe](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
