---
title: SQLStatistics (driver dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLStatistics function [ODBC], dBASE Driver
- DBase driver [ODBC], SQLStatistics
ms.assetid: 631cec1b-66b7-4103-b9a7-ffd81da3c442
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b3ccd07ad517b52a18dc25ddb3cb3882bd2eb61e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68037836"
---
# <a name="sqlstatistics-dbase-driver"></a>SQLStatistics (driver dBASE)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
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
