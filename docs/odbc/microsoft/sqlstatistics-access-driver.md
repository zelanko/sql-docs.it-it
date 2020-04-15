---
title: SQLStatistics (Driver di accesso) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Access driver [ODBC], SQLStatistics
- SQLStatistics function [ODBC], Access Driver
ms.assetid: 6117ac77-1020-4f0c-8eed-e671c34c1f21
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f75f41bf63cbf224772955effa0f120b5d384111
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299361"
---
# <a name="sqlstatistics-access-driver"></a>SQLStatistics (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Colonna|Commenti|  
|------------|--------------|  
|TABLE_QUALIFIER|Viene restituito il percorso di un file di database per Microsoft Access.<br /><br /> I criteri di ricerca non sono supportati nell'argomento *szTableQualifier.*|  
|TABLE_OWNER|Viene restituito NULL in questa colonna, perché il nome del proprietario non è supportato.|  
|TABLE_NAME|Nome di tabella non delimitato.<br /><br /> I criteri di ricerca non sono supportati nell'argomento *szTableName.*|  
|INDEX_QUALIFIER|Viene sempre restituito NULL.|  
|INDEX_NAME|Dipendente dall'indice.|  
|TYPE|Per TYPE verrà restituito solo SQL_TABLE_STAT o SQL_INDEX_OTHER.|  
|SEQ_IN_INDEX|Dipendente dall'indice.|  
|COLUMN_NAME|Dipendente dall'indice.|  
|COLLATION|Dipendente dall'indice.|  
|CARDINALITY|Restituito solo per Microsoft Access.|  
|PAGES|Viene sempre restituito NULL.|  
  
 Il filtro si basa sull'univocità (argomento *fUnique).* Il *fAccuracy* parametro viene ignorato.
