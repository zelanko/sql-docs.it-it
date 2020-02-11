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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.openlocfilehash: acb8d5f9687798bc0efa514ee8646b16140fcd36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100579"
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
