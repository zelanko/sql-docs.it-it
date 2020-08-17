---
description: Uso degli identificatori dei tipi di dati
title: Utilizzo degli identificatori dei tipi di dati | Microsoft Docs
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
ms.openlocfilehash: 54fe7267ea70dc50b0b40f16b27a1306fea533f2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88386277"
---
# <a name="using-data-type-identifiers"></a>Uso degli identificatori dei tipi di dati
Le applicazioni utilizzano gli identificatori dei tipi di dati in due modi: per descrivere i buffer al driver e per recuperare i metadati relativi al set di risultati dal driver, in modo che possano determinare il tipo di buffer C da usare per archiviare i dati. Per eseguire queste attività, le applicazioni chiamano le funzioni seguenti:  
  
-   **SQLBindParameter**, **SQLBindCol**e **SQLGetData** : per descrivere il tipo di dati C dei buffer di applicazione.  
  
-   **SQLBindParameter** : per descrivere il tipo di dati SQL di parametri dinamici.  
  
-   **SQLColAttribute** e **SQLDescribeCol** : per recuperare i tipi di dati SQL delle colonne del set di risultati.  
  
-   **SQLDescribeParameter** : per recuperare i tipi di dati SQL dei parametri.  
  
-   **SQLColumns**, **SQLProcedureColumns**e **SQLSpecialColumns** : per recuperare i tipi di dati SQL di varie informazioni sullo schema  
  
-   **SQLGetTypeInfo** -per recuperare un elenco dei tipi di dati supportati  
  
 Gli identificatori dei tipi di dati vengono archiviati nel campo SQL_DESC_CONCISE_TYPE di un descrittore. Le funzioni descrittore **SQLSetDescField** e **SQLSetDescRec** possono essere usate con i tipi appropriati per eseguire le attività elencate nell'elenco precedente. Per ulteriori informazioni, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).
