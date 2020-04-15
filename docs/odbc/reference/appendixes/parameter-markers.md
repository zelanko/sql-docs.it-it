---
title: Indicatori di parametro Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 132473de586094f79dd34c999d44f6dd59aefaef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303572"
---
# <a name="parameter-markers"></a>Marcatori di parametro
In conformità con la specifica SQL-92, un'applicazione non può inserire indicatori di parametro nelle posizioni seguenti. Per un elenco più completo, vedere la specifica SQL-92.  
  
-   In un elenco **SELECT**  
  
-   Come entrambe le *espressioni* in un *predicato di confronto*  
  
-   Come entrambi gli operandi di un operatore binario  
  
-   Come entrambi i primi e i secondi operandi di un'operazione **BETWEEN**  
  
-   Come primo e terzo operando di un'operazione **BETWEEN**  
  
-   Come espressione e primo valore di un'operazione **IN**  
  
-   Come operando di un'operazione unaria o -  
  
-   Come argomento di un *set-function-reference*  
  
 Per altre informazioni sugli indicatori di parametro, vedere la specifica SQL-92.For more information about parameter markers, see the SQL-92 specification. Per ulteriori informazioni sui parametri, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md).
