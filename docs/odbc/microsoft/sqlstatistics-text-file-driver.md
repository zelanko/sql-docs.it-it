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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4deede2060821ed05a58a637adcf09493fd910dc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037833"
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
