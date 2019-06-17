---
title: SQLStatistics (Driver Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Paradox driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Paradox Driver
ms.assetid: 886cab83-d599-4fbc-9c88-e8cb833aac4b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 634fbcdbf78515e59295e679072ffa5fd08e4823
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62686928"
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics (driver Paradox)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Paradox. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Il percorso di una directory.<br /><br /> Criteri di ricerca non sono supportata nel *szTableQualifier* argomento.|  
|TABLE_OWNER|Poiché il nome del proprietario non è supportato in questa colonna viene restituito NULL.|  
|TABLE_NAME|Nome della tabella non delimitato.<br /><br /> Criteri di ricerca non sono supportata nel *szTableName* argomento.|  
|INDEX_QUALIFIER|Viene sempre restituito NULL.|  
|INDEX_NAME|Indice dipendente.|  
|TYPE|Verranno restituiti solo SQL_TABLE_STAT o SQL_INDEX_OTHER per tipo.|  
|SEQ_IN_INDEX|Indice dipendente.|  
|COLUMN_NAME|Indice dipendente.|  
|COLLATION|Indice dipendente.|  
|PAGES|Viene sempre restituito NULL.|  
  
 Il filtro si basa sull'univocità (la *fUnique* argomento). Il *fAccuracy* parametro viene ignorato.
