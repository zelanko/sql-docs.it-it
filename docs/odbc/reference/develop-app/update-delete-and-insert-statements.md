---
title: Istruzioni UPDATE, DELETE e INSERT | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942832"
---
# <a name="update-delete-and-insert-statements"></a>Istruzioni UPDATE, DELETE e INSERT
Le applicazioni basate su SQL consentono di apportare modifiche alle tabelle eseguendo le istruzioni **Update**, **Delete**e **Insert** . Queste istruzioni fanno parte del livello di conformità della grammatica SQL minimo e devono essere supportate da tutti i driver e dalle origini dati.  
  
 La sintassi di queste istruzioni è la seguente:  
  
 **Aggiorna** _nome tabella_  
  
 **Set** _column-identifier_ **=** {*Expression* &#124; **null**}  
  
 **=** [**,** _identificatore di colonna_ {*Expression* &#124; **null**}]...  
  
 [**Dove** _ricerca-condizione_]  
  
 **Elimina da** _nome-tabella_[**where** _Search-Condition_]  
  
 **Insert into** _Table-Name_[**(** _column-identifier_ [**,** _column-identifier_]... **)**]  
  
 {*query-Specification* &#124; **valori (** _Insert-value_ [**,** _Insert-value_]... **)**}  
  
 Si noti che l'elemento *query-Specification* è valido solo nelle grammatiche core e SQL estese e che l' *espressione* e gli elementi della *condizione di ricerca* diventano più complessi nelle grammatiche di base e SQL estese.  
  
 Analogamente ad altre istruzioni SQL, le istruzioni **Update**, **Delete**e **Insert** sono spesso più efficienti quando utilizzano parametri. L'istruzione seguente, ad esempio, può essere preparata e ripetutamente eseguita per inserire più righe nella tabella Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Questa efficienza può essere aumentata passando matrici di valori di parametro. Per ulteriori informazioni sui parametri di istruzione e sulle matrici di valori di parametro, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md).
