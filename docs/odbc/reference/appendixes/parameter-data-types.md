---
title: 'Tipi di dati dei parametri : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: f29bb70937df32e03480c13c7ef739eb273f15eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303582"
---
# <a name="parameter-data-types"></a>Tipi di dati parametro
Anche se ogni parametro specificato con **SQLBindParameter** viene definito utilizzando un tipo di dati SQL, i parametri in un'istruzione SQL non hanno alcun tipo di dati intrinseco. Pertanto, gli indicatori di parametro possono essere inclusi in un'istruzione SQL solo se i relativi tipi di dati possono essere dedotti da un altro operando nell'istruzione. Ad esempio, in un'espressione aritmetica come ? COLONNA1, il tipo di dati del parametro può essere dedotto dal tipo di dati della colonna denominata rappresentata da COLUMN1. Un'applicazione non può utilizzare un indicatore di parametro se non è possibile determinare il tipo di dati.  
  
 Nella tabella seguente viene descritto come viene determinato un tipo di dati per diversi tipi di parametri, in conformità con SQL-92. Per una specifica più completa sull'inferenza del tipo di parametro quando vengono utilizzate altre clausole SQL, vedere la specifica SQL-92.  
  
|Posizione del parametro|Tipo di dati presunto|  
|---------------------------|-----------------------|  
|Un operando di un operatore aritmetico binario o di confrontoOne operand of a binary arithmetic or comparison operator|Uguale all'altro operando|  
|Il primo operando in una clausola **BETWEEN**|Uguale al secondo operando|  
|Secondo o terzo operando in una clausola **BETWEEN**|Uguale al primo operando|  
|Espressione utilizzata con **IN**|Uguale al primo valore o alla colonna del risultato della sottoquery|  
|Valore utilizzato con **IN**|Uguale all'espressione o al primo valore se è presente un indicatore di parametro nell'espressione|  
|Valore di modello utilizzato con **LIKE**|VARCHAR|  
|Un valore di aggiornamento utilizzato con **UPDATE**|Uguale alla colonna di aggiornamento|
