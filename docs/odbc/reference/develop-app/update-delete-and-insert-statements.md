---
title: Le istruzioni INSERT, DELETE e UPDATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2a2787be1bf44e1f214d396444a73b938acf7ce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67942832"
---
# <a name="update-delete-and-insert-statements"></a>Istruzioni UPDATE, DELETE e INSERT
Applicazioni basate su SQL apportano modifiche alle tabelle mediante l'esecuzione di **UPDATE**, **eliminare**, e **Inserisci** istruzioni. Queste istruzioni fanno parte del livello di conformità grammatica SQL minima e devono essere supportate da tutti i driver e origini dati.  
  
 La sintassi di tali istruzioni è:  
  
 **UPDATE** _-nome della tabella_  
  
 **SET** _column-identifier_ **=** {*expression* &#124; **NULL**}  
  
 [ **,** _colonna identificatore_ **=** {*espressione* &#124; **NULL**}]...  
  
 [**In cui** _condizione di ricerca_]  
  
 **DELETE FROM** _nome tabella_[**in cui** _condizioni di ricerca_]  
  
 **INSERT INTO** _nome tabella_[ **(** _colonna identificatore_ [ **,** _-identificatoredellacolonna_]... **)** ]  
  
 {*query-specification* &#124; **valori (** _insert-value_ [ **,** _insert-valore_]... **)** }  
  
 Si noti che il *query-specification* elemento è valido solo nelle grammatiche di Core e SQL estesa e che le *expression* e *condizione di ricerca* elementi diventano più complesse nelle grammatiche di Core e SQL estesa.  
  
 Come le altre istruzioni SQL, **UPDATE**, **eliminare**, e **Inserisci** istruzioni sono spesso più efficiente quando si usano i parametri. Ad esempio, l'istruzione seguente può essere preparata ed eseguita ripetutamente per inserire più righe nella tabella Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Questa efficienza può essere aumentata mediante il passaggio di matrici di valori di parametro. Per altre informazioni sui parametri delle istruzioni e le matrici di valori dei parametri, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md).
