---
title: Marcatori di parametro | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81303572"
---
# <a name="parameter-markers"></a>Marcatori di parametro
In conformità con la specifica SQL-92, un'applicazione non può inserire marcatori di parametro nei percorsi seguenti. Per un elenco più completo, vedere la specifica di SQL-92.  
  
-   In un elenco di **selezione**  
  
-   Come entrambe le *espressioni* in un *predicato di confronto*  
  
-   Come entrambi gli operandi di un operatore binario  
  
-   Sia il primo che il secondo operando di un'operazione **between**  
  
-   Sia il primo che il terzo operando di un'operazione **between**  
  
-   Sia l'espressione che il primo valore di un'operazione **in**  
  
-   Come operando di un'operazione unaria + o-  
  
-   Come argomento di *set-Function-Reference*  
  
 Per ulteriori informazioni sugli indicatori di parametro, vedere la specifica SQL-92. Per ulteriori informazioni sui parametri, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md).
