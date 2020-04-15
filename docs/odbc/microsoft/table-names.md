---
title: Nomi di tabella Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL grammar [ODBC], table names
- table names [ODBC]
ms.assetid: f7a5cb0a-3be7-4f46-82f9-64ffdbceaa9b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91a415cd456186f18ef358b9d504145f78152774
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303122"
---
# <a name="table-names"></a>Nomi di tabella
Quando si utilizza il driver dBASE, Microsoft Excel, Paradox o Text, i nomi di tabella che si verificano nella clausola FROM di SELECT o DELETE, dopo la clausola INTO in INSERT e dopo UPDATE, CREATE TABLE e DROP TABLE possono contenere un percorso, un nome primario e un'estensione di file validi.  
  
 L'utilizzo di un nome di tabella in un'altra posizione in un'istruzione SQL non supporta l'utilizzo di percorsi o estensioni, ma accetta solo il nome primario (ad esempio, EMP FROM C:  
  
 È possibile utilizzare i nomi di correlazione (alias). Ad esempio:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
