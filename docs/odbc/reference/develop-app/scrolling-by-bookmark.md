---
description: Scorrimento in base al segnalibro
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 52ef0813f3f9fd3f2d139a2549000c629943109e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476473"
---
# <a name="scrolling-by-bookmark"></a>Scorrimento in base al segnalibro
Quando si recuperano righe con **SQLFetchScroll**, un'applicazione può usare un segnalibro come base per la selezione della riga iniziale. Si tratta di una forma di indirizzamento assoluto, in quanto non dipende dalla posizione del cursore corrente. Per scorrere fino a una riga con segnalibro, l'applicazione chiama **SQLFetchScroll** con un *FetchOrientation* di SQL_FETCH_BOOKMARK. Questa operazione usa il segnalibro a cui fa riferimento l'attributo dell'istruzione SQL_ATTR_FETCH_BOOKMARK_PTR. L'operazione restituisce il set di righe che inizia con la riga identificata dal segnalibro. Un'applicazione può specificare un offset per questa operazione nell'argomento *FetchOffset* della chiamata a **SQLFetchScroll**. Quando viene specificato un offset, la prima riga del set di righe restituito viene determinata aggiungendo il numero nell'argomento *FetchOffset* al numero della riga identificata dal segnalibro. Questo utilizzo dell'argomento *FetchOffset* non è supportato se utilizzato con ODBC 2. driver *x* ; Quando un'applicazione chiama **SQLFetchScroll** in un ODBC 2. driver *x* con *FetchOrientation* impostato su SQL_FETCH_BOOKMARK, l'argomento *FetchOffset* deve essere impostato su 0.
