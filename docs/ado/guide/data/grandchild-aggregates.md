---
title: Aggregazioni nipoti | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 148a2798d04bc7ec41832e5103d8ec097ffa9a0c
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82764822"
---
# <a name="grandchild-aggregates"></a>Aggregazioni nipote
Alla colonna del capitolo creata in una clausola di un comando Shape può essere assegnato un *nome di alias di capitolo* , in genere con la parola chiave As. È possibile identificare qualsiasi colonna in qualsiasi capitolo del **Recordset** di forma con un nome completo che identifichi l'elemento figlio contenente la colonna. Se, ad esempio, il capitolo padre, chap1, contiene un capitolo figlio CHAP2 con una colonna Amount, AMT, il nome completo sarà chap1. CHAP2. AMT. Il nome completo può quindi essere usato come argomento per una delle funzioni di aggregazione (SUM, AVG, MAX, MIN, COUNT, STDEV o ANY).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](../../../ado/guide/data/data-shaping-example.md)
