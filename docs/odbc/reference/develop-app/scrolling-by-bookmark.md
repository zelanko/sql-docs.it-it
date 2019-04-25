---
title: Scorrimento in base al segnalibro | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90ba6ed3a6feb163fbe1eaf39cce14ae501c232e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468377"
---
# <a name="scrolling-by-bookmark"></a>Scorrimento in base al segnalibro
Durante il recupero di righe con **SQLFetchScroll**, un'applicazione può utilizzare un segnalibro come base per la selezione della riga iniziale. Si tratta di una forma di indirizzamento assoluto, in quanto non dipende dalla posizione del cursore corrente. Scorrere fino a una riga con segnalibro, l'applicazione chiama **SQLFetchScroll** con un *FetchOrientation* impostato su sql_fetch_bookmark. Questa operazione Usa il segnalibro a cui punta l'attributo di istruzione SQL_ATTR_FETCH_BOOKMARK_PTR. L'operazione restituisce il set di righe che inizia con la riga identificata dal segnalibro. Un'applicazione può specificare un offset per questa operazione nel *FetchOffset* argomento della chiamata a **SQLFetchScroll**. Quando viene specificato un offset, la prima riga del set di righe restituito è determinata dall'aggiunta del numero nel *FetchOffset* argomento per il numero della riga identificata dal segnalibro. Questo utilizzo dei *FetchOffset* argomento non è supportato quando usato con l'API ODBC 2. *x* driver; quando un'applicazione chiama **SQLFetchScroll** in un'API ODBC 2. *x* driver con *FetchOrientation* impostato su SQL_FETCH_BOOKMARK, il *FetchOffset* argomento deve essere impostato su 0.
