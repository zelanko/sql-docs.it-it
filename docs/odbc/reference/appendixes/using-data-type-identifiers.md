---
title: Utilizzo degli identificatori dei tipi di dati Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- identifiers [ODBC], data types
ms.assetid: 467e0c0c-a818-4737-8a24-3d8e15c7e162
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8be8eef0441d48ed03ea6ccf8f656627c1dd9b63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301422"
---
# <a name="using-data-type-identifiers"></a>Uso degli identificatori dei tipi di dati
Le applicazioni usano gli identificatori dei tipi di dati in due modi: per descrivere i buffer al driver e per recuperare i metadati relativi al set di risultati dal driver in modo che possano determinare il tipo di buffer C da utilizzare per archiviare i dati. Le applicazioni chiamano le seguenti funzioni per eseguire queste attività:  
  
-   **SQLBindParameter**, **SQLBindCol**e **SQLGetData** - per descrivere il tipo di dati C dei buffer dell'applicazione.  
  
-   **SQLBindParameter** - per descrivere il tipo di dati SQL dei parametri dinamici.  
  
-   **SQLColAttribute** e **SQLDescribeCol** - per recuperare i tipi di dati SQL delle colonne del set di risultati.  
  
-   **SQLDescribeParameter** - per recuperare i tipi di dati SQL dei parametri.  
  
-   **SQLColumns**, **SQLProcedureColumns**e **SQLSpecialColumns** - per recuperare i tipi di dati SQL di varie informazioni sullo schema  
  
-   **SQLGetTypeInfo** - per recuperare un elenco di tipi di dati supportati  
  
 Gli identificatori dei tipi di dati vengono archiviati nel campo SQL_DESC_CONCISE_TYPE di un descrittore. Le funzioni descrittore **SQLSetDescField** e **SQLSetDescRec** possono essere utilizzate con i tipi appropriati per eseguire le attività elencate nell'elenco precedente. Per ulteriori informazioni, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).
