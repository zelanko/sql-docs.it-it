---
title: Tipo di dati C segnalibro | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 566f1065d30a47b2db234ba1f11f877725189fb7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292291"
---
# <a name="bookmark-c-data-type"></a>Tipo di dati C Bookmark
Il tipo di dati C segnalibro consente a un'applicazione di recuperare un segnalibro. I tipi di segnalibro C vengono utilizzati solo per recuperare i valori dei segnalibri che possono essere di lunghezza variabile. non devono essere convertiti in altri tipi di dati. Tramite un'applicazione viene recuperato un segnalibro dalla colonna 0 del set di risultati con **SQLBulkOperations** (con un'operazione di SQL_ADD), **SQLFetch**, **SQLFetchScroll**o **SQLGetData**. Per ulteriori informazioni, vedere [segnalibri](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
 Nella tabella seguente sono elencati i valori di *CType* per il tipo di dati c del segnalibro, il tipo di dati c ODBC che implementa il tipo di dati c del segnalibro e la definizione di questo tipo di dati da SQL. H.  
  
> [!NOTE]
>  Il tipo di dati SQL_C_BOOKMARK è stato deprecato. Le applicazioni ODBC *3. x* non devono utilizzare SQL_C_BOOKMARK. I driver ODBC *3. x* devono supportare SQL_C_BOOKMARK solo se vogliono lavorare con le applicazioni ODBC *2. x* che lo usano. Gestione driver esegue il mapping SQL_C_VARBOOKMARK SQL_C_BOOKMARK quando un'applicazione utilizza un driver ODBC *2. x* .  
  
|Identificatore di tipo C|Typedef ODBC C|Tipo C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Deprecato)|Segnalibro|unsigned long int|  
|SQL_C_VARBOOKMARK|SQLCHAR|unsigned char *|
