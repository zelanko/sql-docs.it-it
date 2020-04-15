---
title: Tipo di dati Bookmark C Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292291"
---
# <a name="bookmark-c-data-type"></a>Tipo di dati C Bookmark
Il tipo di dati del segnalibro C consente a un'applicazione di recuperare un segnalibro. I tipi di segnalibro C vengono utilizzati solo per recuperare i valori dei segnalibri che possono essere di lunghezza variabile; non devono essere convertiti in altri tipi di dati. Un'applicazione recupera un segnalibro dalla colonna 0 del set di risultati con **SQLBulkOperations** (con un'operazione di SQL_ADD), **SQLFetch**, **SQLFetchScroll**o **SQLGetData**. Per ulteriori informazioni, consultate [Segnalibri.](../../../odbc/reference/develop-app/bookmarks-odbc.md)  
  
 Nella tabella seguente sono elencati il valore di *CType* per il tipo di dati segnalibro C, il tipo di dati C ODBC che implementa il tipo di dati segnalibro C e la definizione di questo tipo di dati da SQL. H.  
  
> [!NOTE]
>  Il tipo di dati SQL_C_BOOKMARK è deprecato. Le applicazioni ODBC *3.x* non devono utilizzare SQL_C_BOOKMARK. I driver ODBC *3.x* devono supportare SQL_C_BOOKMARK solo se desiderano lavorare con le applicazioni ODBC *2.x* che lo utilizzano. Gestione Driver esegue il mapping di SQL_C_VARBOOKMARK a SQL_C_BOOKMARK quando un'applicazione funziona con un driver ODBC *2.x.*  
  
|Identificatore del tipo C|ODBC C typedef|Tipo C|  
|-----------------------|--------------------|------------|  
|SQL_C_BOOKMARK<br />(Deprecato)|Segnalibro|unsigned long int|  
|SQL_C_VARBOOKMARK|Proprietà SQLCHAR .|unsigned char *|
