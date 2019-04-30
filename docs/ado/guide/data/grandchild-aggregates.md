---
title: Aggregazioni nipote | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- grandchild aggregates [ADO]
- data shaping [ADO], grandchild aggregates
ms.assetid: 4162d35f-2ce1-4218-80a5-b6933348837e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1bff3c8a155e1e9378acbb659f00817f478382e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161600"
---
# <a name="grandchild-aggregates"></a>Aggregazioni nipote
La colonna a capitoli creata in una clausola di un comando della forma può essere stata assegnata un *nome capitolo-alias* (in genere con la parola chiave AS). È possibile identificare ogni colonna in un capitolo del data shaping **Recordset** con un nome completo che identifica l'elemento figlio che contiene la colonna. Ad esempio, se il capitolo di padre, Cap1, include un capitolo figlio, Cap2, che dispone di una colonna amount amt, quindi il nome completo sarebbe chap1.chap2.amt. Il nome completo è quindi utilizzabile come argomento a una delle funzioni di aggregazione (SUM, AVG, MAX, MIN, COUNT, STDEV o qualsiasi).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](../../../ado/guide/data/data-shaping-example.md)
