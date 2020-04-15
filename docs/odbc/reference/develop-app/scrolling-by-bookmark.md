---
title: Scorrimento di Bookmark Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
- scrolling rows [ODBC]
ms.assetid: 4862f098-41a4-4bd2-894e-f71bb97f9bc0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 454e29abdf848fdf4f4eaae090e7cc326f0048df
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304192"
---
# <a name="scrolling-by-bookmark"></a>Scorrimento in base al segnalibro
Quando si recuperano righe con **SQLFetchScroll**, un'applicazione può utilizzare un segnalibro come base per la selezione della riga iniziale. Si tratta di una forma di indirizzamento assoluto, in quanto non dipende dalla posizione del cursore corrente. Per scorrere fino a una riga con segnalibro, l'applicazione chiama **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_BOOKMARK. Questa operazione utilizza il segnalibro a cui punta l'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR. L'operazione restituisce il set di righe che inizia con la riga identificata dal segnalibro. Un'applicazione può specificare un offset per questa operazione nell'argomento *FetchOffset* della chiamata a **SQLFetchScroll**. Quando viene specificato un offset, la prima riga del set di righe restituito viene determinata aggiungendo il numero nell'argomento *FetchOffset* al numero della riga identificata dal segnalibro. Questo utilizzo dell'argomento *FetchOffset* non è supportato se utilizzato con ODBC 2. *x* driver; quando un'applicazione chiama **SQLFetchScroll** in un ODBC 2. *x* driver con *FetchOrientation* impostato su SQL_FETCH_BOOKMARK, il *FetchOffset* argomento deve essere impostato su 0.
