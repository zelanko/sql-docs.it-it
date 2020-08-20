---
description: Predicato BETWEEN
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
ms.openlocfilehash: 2f2283f5824e4be0c9702bfe8feef9fe3109849a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500384"
---
# <a name="between-predicate"></a>Predicato BETWEEN
Ecco la sintassi:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Restituisce true solo se *expression1* è maggiore o uguale a *expression2* e *expression1* è minore o uguale a *expression3*.  
  
 La semantica di questa sintassi è diversa per i driver del database desktop e il motore Microsoft Jet. In Microsoft Jet SQL, *expression2* può essere maggiore di *expression3* , in modo che l'istruzione restituisca true solo se *expression1* è maggiore o uguale a *expression3*e *expression1* è minore o uguale a *expression2*.
