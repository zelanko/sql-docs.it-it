---
title: Predicato BETWEEN | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a4411345d790e64ae9fb21144a7d82ffe4cd45e8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301955"
---
# <a name="between-predicate"></a>Predicato BETWEEN
La sintassi seguente:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Restituisce true solo se *expression1* è maggiore o uguale a *expression2* e *expression1* è minore o uguale a *expression3*.  
  
 La semantica di questa sintassi è diversa per i driver di Database Desktop e la gestione di Microsoft Jet. In SQL di Microsoft Jet *expression2* può essere maggiore *expression3* in modo che l'istruzione restituirà TRUE solo se *expression1* è maggiore o uguale a *expression3*, e *expression1* è minore o uguale a *expression2*.
