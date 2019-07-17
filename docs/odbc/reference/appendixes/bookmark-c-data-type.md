---
title: Tipo di dati C Bookmark | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], bookmark C data type
- pseudo-type identifiers [ODBC], bookmark C data type
- data types [ODBC], pseudo-type identifiers
- bookmarks [ODBC]
- bookmark C data type [ODBC]
ms.assetid: add88e48-ada3-4c0c-a5ac-e78903d3ff41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 86488da93470a61a54638e9c60e6e1795a9da4dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125750"
---
# <a name="bookmark-c-data-type"></a>Tipo di dati C Bookmark
Il tipo di dati C bookmark consente a un'applicazione recuperare un segnalibro. I tipi di segnalibro C vengono utilizzati solo per recuperare i valori di segnalibro che possono variare in lunghezza; essi non devono essere convertiti in altri tipi di dati. Un'applicazione recupera dalla colonna 0 il risultato impostata con un segnalibro **SQLBulkOperations** (con un'operazione di SQL_ADD), **SQLFetch**, **SQLFetchScroll**, o **SQLGetData**. Per altre informazioni, vedere [segnalibri](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 La tabella seguente elenca il valore di *CType* per il tipo di dati C bookmark, digitare il tipo di dati C ODBC che implementa il tipo di dati C bookmark e la definizione dei dati da SQL. H.  
  
> [!NOTE]
>  Il tipo di dati SQL_C_BOOKMARK è stato deprecato. ODBC *3.x* applicazioni non deve usare SQL_C_BOOKMARK. ODBC *3.x* driver devono supportare SQL_C_BOOKMARK solo se si desidera lavorare con ODBC *2.x* le applicazioni che lo usano. Gestione Driver esegue il mapping SQL_C_VARBOOKMARK a SQL_C_BOOKMARK quando un'applicazione funziona con un database ODBC *2.x* driver.  
  
|Identificatore di tipo C|Typedef di ODBC C|Tipo C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Deprecato)|SEGNALIBRO|long int senza segno|  
|SQL_C_VARBOOKMARK|SQLCHAR *|unsigned char *|
