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
ms.openlocfilehash: 251ae0e4e94cec903e2c4b5cf687ed9b8b41dfc8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67952396"
---
# <a name="identifiers-limitations"></a>Limitazioni degli identificatori
Se un identificatore contiene uno spazio o un simbolo speciale, l'identificatore deve essere racchiuso tra virgolette. Un nome valido è una stringa di non più di 64 caratteri, di cui il primo carattere non deve essere uno spazio. I nomi validi non possono contenere caratteri di controllo o i caratteri speciali seguenti:' &#124; # *? [ ] . ! $ .  
  
 Non utilizzare le parole riservate elencate nella grammatica SQL nell'Appendice C del riferimento per *programmatori ODBC* (o il formato abbreviato di queste parole riservate) come identificatori (ovvero nomi di tabella o di colonna), a meno che non si circondi la parola tra virgolette (').
