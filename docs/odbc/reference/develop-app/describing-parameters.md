---
title: Che descrive i parametri | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], describing parameters
ms.assetid: 118d0f47-2afd-4955-bb47-38b1e2c2f38f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d32e5212ba1ba28262d871498f2974485d38233
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68040025"
---
# <a name="describing-parameters"></a>Descrizione di parametri
**SQLBindParameter** dispone di argomenti che descrivono il parametro: il tipo SQL, precisione e scala. Il driver Usa tali informazioni, oppure *metadati,* per convertire il valore del parametro nel tipo richiesto dall'origine dati. A prima vista, potrebbe sembrare che il driver è in una posizione migliore per conoscere i metadati dei parametri rispetto all'applicazione; Dopo tutto, il driver può individuare facilmente i metadati per un risultato di set di colonne. Ebbene, questo non avviene. In primo luogo, la maggior parte delle origini dati non forniscono un modo per il driver individuare i metadati del parametro. In secondo luogo, la maggior parte delle applicazioni conoscono già i metadati.  
  
 Se un'istruzione SQL è hardcoded nell'applicazione, il writer dell'applicazione conosce già il tipo di ogni parametro. Se viene costruita un'istruzione SQL dall'applicazione in fase di esecuzione, l'applicazione può determinare i metadati durante la compilazione dell'istruzione. Ad esempio, quando l'applicazione crea la clausola  
  
```  
WHERE OrderID = ?  
```  
  
 è possibile chiamare **SQLColumns** per la colonna OrderID.  
  
 L'unica situazione in cui l'applicazione non è facile determinare i metadati dei parametri è quando l'utente immette un'istruzione con parametri. In questo caso, l'applicazione chiama **SQLPrepare** preparare l'istruzione **SQLNumParams** per determinare il numero di parametri, e **SQLDescribeParam** per descrivere ogni parametro. Tuttavia, come indicato in precedenza, la maggior parte delle origini dati non forniscono un modo per il driver individuare i metadati del parametro, pertanto **SQLDescribeParam** non è supportato.
