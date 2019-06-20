---
title: Cursori misti | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ef8d5142397b4169513cf262ba4126ccba1fc1c3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66785834"
---
# <a name="mixed-cursors"></a>Cursori misti

Un cursore misto è una combinazione di un cursore gestito da keyset e un cursore dinamico. Viene usato quando il set di risultati è troppo grande per essere ragionevolmente salvato chiavi per l'intero set di risultati. Cursori misti vengono implementati mediante la creazione di un set di chiavi che è maggiore di set di righe, ma minore l'intero set di risultati.  
  
 Fino a quando l'applicazione scorre all'interno del keyset, il comportamento è gestito da keyset. Quando l'applicazione scorre fuori il keyset, il comportamento è dinamico: Il cursore recupera le righe richieste e crea un nuovo set di chiavi. Dopo aver creato il nuovo set di chiavi, viene ripristinato il comportamento gestito da keyset all'interno di tale set di chiavi.  
  
 Si supponga, ad esempio, un set di risultati include 1.000 righe e Usa un cursore misto con una dimensione del keyset pari a 100 e una dimensione di set di righe pari a 10. Quando il primo set di righe viene recuperato, il cursore viene creato un keyset costituito dalle chiavi per le prime 100 righe. Restituisce quindi le prime 10 righe, come richiesto.  
  
 Ora si supponga che un'altra applicazione Elimina righe 11 e 101. Se il cursore tenta di recuperare la riga 11, che si verificherà un gap perché ha una chiave per questa riga, ma non esiste alcuna riga. Questo è gestito da keyset comportamento. Se il cursore tenta di recuperare la riga 101, il cursore non rileverà che la riga è manca perché non dispone di una chiave per la riga. In alternativa, consente di recuperare che in precedenza era riga 102. Si tratta del comportamento del cursore dinamico.  
  
 Un cursore misto è equivalente a un cursore gestito da keyset quando la dimensione del keyset è uguale alla dimensione del set di risultati. Un cursore misto è equivalente a un cursore dinamico quando la dimensione del keyset è uguale a 1.
