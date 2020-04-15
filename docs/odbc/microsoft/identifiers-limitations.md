---
title: Limitazioni degli identificatori Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC]
- desktop database drivers [ODBC]
ms.assetid: b3466382-71cb-4f82-8318-092a8fcef3df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7154f2db09b69e6376b1fe3af1de3f2c646ee94e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286251"
---
# <a name="identifiers-limitations"></a>Limitazioni degli identificatori
Se un identificatore contiene uno spazio o un simbolo speciale, l'identificatore deve essere racchiuso tra virgolette. Un nome valido è una stringa di non più di 64 caratteri, di cui il primo carattere non deve essere uno spazio. I nomi validi non possono includere i caratteri di controllo o i caratteri speciali seguenti: ' &#124; [ ] . ! $ .  
  
 Non utilizzare le parole riservate elencate nella grammatica SQL nell'Appendice C di *ODBC Programmer's Reference* (o la forma abbreviata di queste parole riservate) come identificatori (ovvero nomi di tabella o di colonna), a meno che non si racchiuda la parola tra virgolette rovesciate (').
