---
title: SqlStatistics (Driver Di Paradox) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5e9782eb22e4176a57aab7bdd3823982575a0d55
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299321"
---
# <a name="sqlstatistics-paradox-driver"></a>SQLStatistics (driver Paradox)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver Paradox.This topic provides Paradox Driver-specific information. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Percorso di una directory.<br /><br /> I criteri di ricerca non sono supportati nell'argomento *szTableQualifier.*|  
|TABLE_OWNER|VIENE restituito NULL in questa colonna perché il nome del proprietario non è supportato.|  
|TABLE_NAME|Nome di tabella non delimitato.<br /><br /> I criteri di ricerca non sono supportati nell'argomento *szTableName.*|  
|INDEX_QUALIFIER|Viene sempre restituito NULL.|  
|INDEX_NAME|Dipendente dall'indice.|  
|TYPE|Per TYPE verrà restituito solo SQL_TABLE_STAT o SQL_INDEX_OTHER.|  
|SEQ_IN_INDEX|Dipendente dall'indice.|  
|COLUMN_NAME|Dipendente dall'indice.|  
|COLLATION|Dipendente dall'indice.|  
|PAGES|Viene sempre restituito NULL.|  
  
 Il filtro si basa sull'univocità (argomento *fUnique).* Il *fAccuracy* parametro viene ignorato.
