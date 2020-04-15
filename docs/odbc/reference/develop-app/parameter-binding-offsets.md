---
title: Offset dell'associazione di parametri Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets of parameters [ODBC]
- binding offsets of parameters [ODBC]
ms.assetid: 309339e9-9ccd-4a58-8aa4-b6dc88f4eb7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de67b230883f3cf8a582e73ce82e8c4bd7d21ad0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282493"
---
# <a name="parameter-binding-offsets"></a>Offset di associazione di parametri
Un'applicazione può specificare che un offset viene aggiunto agli indirizzi del buffer di parametri associati e gli indirizzi del buffer di lunghezza/indicatore corrispondenti quando viene chiamato **SQLExecDirect** o **SQLExecute.** Il risultato di queste aggiunte determina gli indirizzi utilizzati in queste operazioni.  
  
 Gli offset di binding consentono a un'applicazione di modificare le associazioni senza chiamare **SQLBindParameter** per i parametri associati in precedenza. Una chiamata a **SQLBindParameter** per riassociare un parametro modifica l'indirizzo del buffer e il puntatore di lunghezza/indicatore. La riassociazione con un offset, d'altra parte, aggiunge semplicemente un offset all'indirizzo del buffer del parametro associato esistente e all'indirizzo del buffer di lunghezza/indicatore. Quando vengono utilizzati gli offset, le associazioni sono un "modello" di come vengono disposti i buffer dell'applicazione e l'applicazione può spostare questo "modello" in diverse aree di memoria modificando l'offset. Un nuovo offset può essere specificato in qualsiasi momento e viene sempre aggiunto ai valori associati in origine.  
  
 Per specificare un offset di associazione, l'applicazione imposta l'attributo dell'istruzione SQL_ATTR_PARAM_BIND_OFFSET_PTR sull'indirizzo di un buffer SQLINTEGER. Prima che l'applicazione chiami una funzione che utilizza le associazioni, inserisce un offset in byte in questo buffer, purché né l'indirizzo del buffer del parametro né l'indirizzo del buffer length/indicator siano 0 e il parametro associato si trova nell'istruzione SQL. La somma dell'indirizzo e dell'offset deve essere un indirizzo valido. Ciò significa che uno o entrambi l'offset e l'indirizzo a cui viene aggiunto l'offset possono non essere validi, purché la somma sia un indirizzo valido.  
  
> [!NOTE]  
>  Gli offset di associazione non sono supportati da ODBC 2. *x* driver.
