---
title: Transizioni dei descrittori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- state transitions [ODBC], descriptor
- transitioning states [ODBC], descriptor
- descriptor transitions [ODBC]
ms.assetid: 0cf24fe6-5e3c-45fa-81b8-4f52ddf8501d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 027b711c5c1a2cb2d35e65efdc2b00f441841d8c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240974"
---
# <a name="descriptor-transitions"></a>Transizioni dei descrittori
I descrittori di ODBC sono i seguenti tre stati.  
  
|State|Descrizione|  
|-----------|-----------------|  
|D0|Descrittore non allocato|  
|D1i|Descrittori allocati in modo implicito|  
|D1e|Descrittori allocati in modo esplicito|  
  
 Le tabelle seguenti mostrano come ogni funzione ODBC influisce sullo stato del descrittore.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
  
|D0<br /><br /> Non allocato|D1i<br /><br /> implicito|D1e<br /><br /> Esplicito|  
|------------------------|----------------------|----------------------|  
|D1i[1]|--|--|  
|D1e[2]|--|--|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_STMT.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
## <a name="sqlcopydesc"></a>SQLCopyDesc  
  
|D0<br /><br /> Non allocato|D1i<br /><br /> implicito|D1e<br /><br /> Esplicito|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
  
|D0<br /><br /> Non allocato|D1i<br /><br /> implicito|D1e<br /><br /> Esplicito|  
|------------------------|----------------------|----------------------|  
|--[1]|D0|--|  
|(IH)[2]|(HY017)|D0|  
  
 [1] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_STMT.  
  
 [2] questa riga Mostra le transizioni quando *HandleType* era SQL_HANDLE_DESC.  
  
## <a name="sqlgetdescfield-and-sqlgetdescrec"></a>SQLGetDescField e SQLGetDescRec  
  
|D0<br /><br /> Non allocato|D1i<br /><br /> implicito|D1e<br /><br /> Esplicito|  
|------------------------|----------------------|----------------------|  
|(IH)|--|--|  
  
## <a name="sqlsetdescfield-and-sqlsetdescrec"></a>SQLSetDescField and SQLSetDescRec  
  
|D0<br /><br /> Non allocato|D1i<br /><br /> implicito|D1e<br /><br /> Esplicito|  
|------------------------|----------------------|----------------------|  
|(IH)[1]|--|--|  
  
 [1] questa riga Mostra le transizioni quando *DescriptorHandle* era l'handle di un ARD, APD o IPD, o (per **SQLSetDescField**) quando *DescriptorHandle* era l'handle di un IRD e *FieldIdentifier* era SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR.  
  
## <a name="all-other-odbc-functions"></a>Tutte le altre funzioni ODBC  
  
|D0<br /><br /> Non allocato|D1i<br /><br /> implicito|D1e<br /><br /> Esplicito|  
|------------------------|----------------------|----------------------|  
|--|--|--|
