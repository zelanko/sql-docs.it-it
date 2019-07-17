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
ms.openlocfilehash: 1a0ac99729966acdcb03c2aab0175c34bba0c08a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138122"
---
# <a name="between-predicate"></a>Predicato BETWEEN
La sintassi seguente:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Restituisce true solo se *expression1* è maggiore o uguale a *expression2* e *expression1* è minore o uguale a *expression3*.  
  
 La semantica di questa sintassi è diversa per i driver di Database Desktop e la gestione di Microsoft Jet. In SQL di Microsoft Jet *expression2* può essere maggiore *expression3* in modo che l'istruzione restituirà TRUE solo se *expression1* è maggiore o uguale a *expression3*, e *expression1* è minore o uguale a *expression2*.
