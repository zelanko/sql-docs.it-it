---
title: Gli identificatori dei tipi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cbefab0f02f3229d8b4c0a62a568634ec222290b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305672"
---
# <a name="type-identifiers"></a>Identificatori di tipi
Per descrivere i tipi di dati SQL e C, ODBC definisce due set di *gli identificatori dei tipi*. Un identificatore di tipo descrive il tipo di una colonna di SQL o un buffer di C. Si tratta di un **#define** valore e viene in genere passata come argomento di funzione o restituito nei metadati.  
  
 Ad esempio, la chiamata seguente a **SQLBindParameter** associa una variabile di tipo valore SQL_DATE_STRUCT a un parametro di data in un'istruzione SQL. L'identificatore di tipo C SQL_C_TYPE_DATE specifica il tipo dei *data* variabile e l'identificatore del tipo SQL_TYPE_DATE SQL specifica il tipo del parametro dinamico.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```
