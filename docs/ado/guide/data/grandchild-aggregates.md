---
description: Aggregazioni nipote
title: Aggregazioni nipoti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 02d481e55fa8fc41e022d41b88c9dcd6c4777dfe
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980712"
---
# <a name="grandchild-aggregates"></a>Aggregazioni nipote
Alla colonna del capitolo creata in una clausola di un comando Shape può essere assegnato un *nome di alias di capitolo* , in genere con la parola chiave As. È possibile identificare qualsiasi colonna in qualsiasi capitolo del **Recordset** di forma con un nome completo che identifichi l'elemento figlio contenente la colonna. Se, ad esempio, il capitolo padre, chap1, contiene un capitolo figlio CHAP2 con una colonna Amount, AMT, il nome completo sarà chap1. CHAP2. AMT. Il nome completo può quindi essere usato come argomento per una delle funzioni di aggregazione (SUM, AVG, MAX, MIN, COUNT, STDEV o ANY).  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](./data-shaping-example.md)