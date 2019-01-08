---
title: Marcatori di parametro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 833e2740e54f07701fb66a894bb5e4798c4a42e2
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516398"
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
