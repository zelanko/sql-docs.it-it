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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1f3ff800938574bec81e9cbb86839e014085a2a8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283857"
---
# <a name="between-predicate"></a>Predicato BETWEEN
Ecco la sintassi:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Restituisce true solo se *expression1* è maggiore o uguale a *expression2* e *expression1* è minore o uguale a *expression3*.  
  
 La semantica di questa sintassi è diversa per i driver del database desktop e il motore Microsoft Jet. In Microsoft Jet SQL, *expression2* può essere maggiore di *expression3* , in modo che l'istruzione restituisca true solo se *expression1* è maggiore o uguale a *expression3*e *expression1* è minore o uguale a *expression2*.
