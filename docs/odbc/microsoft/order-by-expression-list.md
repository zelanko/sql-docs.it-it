---
title: ORDER BY-elenco di espressioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ORDER BY clause [ODBC]
- SQL grammar [ODBC], order by clause
ms.assetid: 5ef88186-a99f-4e2c-a3f3-98a42d4f03a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cd88673c4b5309b7463256b85df4f92d6d360b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100789"
---
# <a name="order-by-expression-list"></a>Elenco di espressioni ORDER BY
Le espressioni possono essere utilizzate nella clausola ORDER BY. Nelle clausole seguenti, ad esempio, la tabella viene ordinata in base a tre espressioni chiave: a + b, c + d ed e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Nessun ordinamento consentito per le funzioni set o per un'espressione che contiene una funzione set.
