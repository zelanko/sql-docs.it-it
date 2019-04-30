---
title: Limitazioni degli identificatori | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c781113124d456e1ba866546d6ada7a17371d71f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208522"
---
# <a name="identifiers-limitations"></a>Limitazioni degli identificatori
Se un identificatore contiene uno spazio o un simbolo speciale, l'identificatore deve essere racchiuso tra virgolette back. Un nome valido è una stringa non più di 64 caratteri, di cui il primo carattere non deve essere uno spazio. I nomi validi non possono contenere caratteri di controllo o i caratteri speciali seguenti: ' &#124; # *? [ ] . ! $ .  
  
 Non utilizzare parole riservate elencate nella grammatica SQL nell'appendice C del *riferimento per programmatori ODBC* (o la forma abbreviata delle parole riservate) come identificatori (vale a dire, tabella o colonna di nomi), a meno che non si racchiudono la parola di backup virgolette singole (').
