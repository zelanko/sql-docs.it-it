---
title: Nomi di tabella | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d72d7868d0e19719ea7992bdb8ccd1f61f3718d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633165"
---
# <a name="table-names"></a>Nomi di tabella
Quando si dBASE, Microsoft Excel, Paradox, o testo driver viene utilizzato, i nomi di tabella che si verificano nella clausola FROM di SELECT o DELETE, dopo la clausola INTO in istruzioni INSERT e dopo l'aggiornamento, CREATE TABLE e DROP TABLE può contenere un percorso valido, nome primario e file nome estensione .  
  
 Utilizzo di un nome di tabella in un' posizione in un'istruzione SQL non supporta l'uso dei percorsi o le estensioni, ma verrà accettate solo il nome principale (ad esempio, EMP da C:\ABC\EMP).  
  
 I nomi di correlazione (alias) possono essere utilizzati. Ad esempio:  
  
```  
SELECT *    
FROM C:\ABC\EMP T1    
WHERE T1.COL1 = 'aaa'  
```
