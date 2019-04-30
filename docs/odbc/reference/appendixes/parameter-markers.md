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
manager: craigg
ms.openlocfilehash: cda6719eb46a4a05222bd54062e6cab98459d7dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181773"
---
# <a name="parameter-markers"></a>Marcatori di parametro
Conforme alla specifica di SQL-92, un'applicazione non è possibile posizionare gli indicatori di parametro nelle posizioni seguenti. Per un elenco più completo, vedere la specifica di SQL-92.  
  
-   In un **seleziona** elenco  
  
-   Come entrambe *expressions* in un *predicato di confronto*  
  
-   Come entrambi gli operandi dell'operatore binario  
  
-   Come entrambi gli operandi primi e la secondo di una **BETWEEN** operazione  
  
-   Come operandi del primo e del terzo di una **BETWEEN** operazione  
  
-   Come l'espressione sia il primo valore di un' **India** operazione  
  
-   Come operando di unario + or - operazione  
  
-   Come argomento di un *set-funzione-reference*  
  
 Per altre informazioni sui marcatori di parametro, vedere la specifica di SQL-92. Per altre informazioni sui parametri, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md).
