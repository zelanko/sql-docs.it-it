---
title: Lista di espressioni DI ORDER BY Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 272fa0be844569d322679d444807f8c332b4837b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291221"
---
# <a name="order-by-expression-list"></a>Elenco di espressioni ORDER BY
Le espressioni possono essere utilizzate nella clausola ORDER BY. Nelle clausole seguenti, ad esempio, la tabella viene ordinata in base a tre espressioni chiave: a-b, c'd ed e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Non è consentito ordinare nelle funzioni set o in un'espressione che contiene una funzione set.
