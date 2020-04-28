---
title: SQLStatistics (driver file di testo) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Text File Driver
ms.assetid: 311afc01-d656-425f-be43-4a8e7cbc9a97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 76b9810236b4ec415f8abb8ecefca748c13b51c8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299311"
---
# <a name="sqlstatistics-text-file-driver"></a>SQLStatistics (driver file di testo)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver del file di testo. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Percorso di una directory.<br /><br /> I criteri di ricerca non sono supportati nell'argomento *szTableQualifier* .|  
|TABLE_OWNER|In questa colonna viene restituito NULL perché il nome del proprietario non è supportato.|  
|TABLE_NAME|Nome di tabella non delimitato.<br /><br /> I criteri di ricerca non sono supportati nell'argomento *szTableName* .|  
|INDEX_QUALIFIER|Viene sempre restituito NULL.|  
|INDEX_NAME|Dipendente dall'indice.|  
|TYPE|Per il tipo verranno restituiti solo SQL_TABLE_STAT o SQL_INDEX_OTHER.|  
|SEQ_IN_INDEX|Dipendente dall'indice.|  
|COLUMN_NAME|Dipendente dall'indice.|  
|COLLATION|Dipendente dall'indice.|  
|PAGES|Viene sempre restituito NULL.|  
  
 Il filtro è basato sull'univocità (argomento *fUnique* ). Il parametro *fAccuracy* viene ignorato.
