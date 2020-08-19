---
description: Scorrimento e recupero di righe - Applicazione di segnalibri alle righe in ODBC
title: Segnalibro di righe in ODBC | Microsoft Docs
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e183a969cb6208cebbeef0d5c0fc662f9a93381f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423873"
---
# <a name="scrolling-and-fetching-rows---bookmarking-rows-in-odbc"></a>Scorrimento e recupero di righe - Applicazione di segnalibri alle righe in ODBC
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Un segnalibro è un valore utilizzato per identificare una riga di dati. Il significato del valore del segnalibro è noto solo al driver o all'origine dati. Un segnalibro, ad esempio, può essere tanto semplice quanto un numero di riga o tanto complesso quanto un indirizzo del disco. In ODBC l'applicazione richiede un segnalibro per una determinata riga, lo archivia e lo passa nuovamente al cursore per tornare alla riga.  
  
 Quando si recuperano righe con [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md), un'applicazione può usare un segnalibro come base per la selezione della riga iniziale. Si tratta di una forma di indirizzamento assoluto, in quanto non dipende dalla posizione del cursore corrente. Per scorrere fino a una riga con segnalibro, l'applicazione chiama **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_BOOKMARK. Questa operazione utilizza il segnalibro a cui punta l'attributo dell'opzione SQL_ATTR_FETCH_BOOKMARK_PTR. L'operazione restituisce il set di righe che inizia con la riga identificata dal segnalibro. Un'applicazione può specificare un offset per questa operazione nell'argomento *FetchOffset* della chiamata a **SQLFetchScroll**. Quando viene specificato un offset, la prima riga del set di righe restituita è determinata dall'aggiunta del numero nell'argomento FetchOffset al numero della riga identificata dal segnalibro. Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta solo segnalibri su cursori statici e keyset. Se viene richiesto un cursore dinamico quando si impostano segnalibri, viene invece aperto un cursore keyset.  
  
 I segnalibri possono essere usati anche con la funzione **SQLBulkOperations** per eseguire operazioni su un set di righe a partire dal segnalibro.  
  
## <a name="see-also"></a>Vedere anche  
 [Scorrimento e recupero di righe](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows.md)  
  
  
