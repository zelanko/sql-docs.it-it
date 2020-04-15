---
title: Cursori Misti Documenti Microsoft
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a91dacf8ea9c0ed0db2c3b64634ddd53b854a534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307436"
---
# <a name="mixed-cursors"></a>Cursori misti

Un cursore misto è una combinazione di un cursore basato su keyset e un cursore dinamico. Viene utilizzato quando il set di risultati è troppo grande per salvare ragionevolmente le chiavi per l'intero set di risultati. I cursori misti vengono implementati creando un keyset più piccolo dell'intero set di risultati ma più grande del set di righe.  
  
 Finché l'applicazione scorre all'interno del keyset, il comportamento è basato su keyset. Quando l'applicazione scorre all'esterno del keyset, il comportamento è dinamico: il cursore recupera le righe richieste e crea un nuovo keyset. Dopo aver creato il nuovo keyset, il comportamento viene ripristinato su keyset-driven all'interno di tale keyset.  
  
 Si supponga, ad esempio, che un set di risultati abbia 1.000 righe e utilizzi un cursore misto con una dimensione del set di chiavi pari a 100 e una dimensione del set di righe pari a 10.For example, suppose a result set has 1,000 rows and uses a mixed cursor with a keyset size of 100 and a rowset size of 10. Quando viene recuperato il primo set di righe, il cursore crea un keyset costituito dalle chiavi per le prime 100 righe. Restituisce quindi le prime 10 righe, come richiesto.  
  
 Si supponga ora che un'altra applicazione elimini le righe 11 e 101. Se il cursore tenta di recuperare la riga 11, avrà uno spazio perché dispone di una chiave per questa riga ma non esiste alcuna riga; si tratta di un comportamento basato su keyset. Se il cursore tenta di recuperare la riga 101, il cursore non rileverà che la riga è mancante perché non dispone di una chiave per la riga. Al contrario, recupererà ciò che in precedenza era la riga 102. Si tratta del comportamento dinamico del cursore.  
  
 Un cursore misto equivale a un cursore basato su keyset quando la dimensione del set di chiavi è uguale alla dimensione del set di risultati. Un cursore misto equivale a un cursore dinamico quando la dimensione del keyset è uguale a 1.
