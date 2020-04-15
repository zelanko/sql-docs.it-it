---
title: Descrizione dei parametri Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f4d9284294707da0a469bf75ff9812ad5f7855bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305942"
---
# <a name="describing-parameters"></a>Descrizione di parametri
**SQLBindParameter** include argomenti che descrivono il parametro: il tipo SQL, la precisione e la scala. Il driver utilizza queste informazioni, o *metadati,* per convertire il valore del parametro nel tipo richiesto dall'origine dati. A prima vista, potrebbe sembrare che il driver è in una posizione migliore per conoscere i metadati del parametro rispetto all'applicazione; dopo tutto, il driver può facilmente individuare i metadati per una colonna del set di risultati. A quanto pare, questo non è il caso. In primo luogo, la maggior parte delle origini dati non forniscono un modo per il driver per individuare i metadati dei parametri. In secondo luogo, la maggior parte delle applicazioni conosce già i metadati.  
  
 Se un'istruzione SQL è hardcoded nell'applicazione, il writer dell'applicazione conosce già il tipo di ogni parametro. Se un'istruzione SQL viene costruita dall'applicazione in fase di esecuzione, l'applicazione può determinare i metadati durante la compilazione dell'istruzione. Ad esempio, quando l'applicazione costruisce la clausola  
  
```  
WHERE OrderID = ?  
```  
  
 può chiamare **SQLColumns** per il OrderID colonna.  
  
 L'unica situazione in cui l'applicazione non è in grado di determinare facilmente i metadati del parametro è quando l'utente immette un'istruzione con parametri. In questo caso, l'applicazione chiama **SQLPrepare** per preparare l'istruzione, **SQLNumParams** per determinare il numero di parametri e **SQLDescribeParam** per descrivere ogni parametro. Tuttavia, come è stato annotato in precedenza, la maggior parte delle origini dati non forniscono un modo per il driver per individuare i metadati dei parametri, pertanto **SQLDescribeParam** non è ampiamente supportato.
