---
description: Elenco di espressioni ORDER BY
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd084a1012d445c89cacba168f21267238bc250f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340617"
---
# <a name="order-by-expression-list"></a>Elenco di espressioni ORDER BY
Le espressioni possono essere utilizzate nella clausola ORDER BY. Nelle clausole seguenti, ad esempio, la tabella viene ordinata in base a tre espressioni chiave: a + b, c + d ed e.  
  
```  
SELECT * FROM emp  
ORDER BY a+b,c+d,e  
```  
  
 Nessun ordinamento consentito per le funzioni set o per un'espressione che contiene una funzione set.
