---
title: Offset di binding di parametri | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282493"
---
# <a name="parameter-binding-offsets"></a>Offset di associazione di parametri
Un'applicazione può specificare che un offset viene aggiunto agli indirizzi del buffer dei parametri associati e agli indirizzi di buffer di lunghezza/indicatore corrispondenti quando viene chiamato **SQLExecDirect** o **SQLExecute** . Il risultato di queste aggiunte determina gli indirizzi utilizzati in queste operazioni.  
  
 Gli offset di binding consentono a un'applicazione di modificare i binding senza chiamare **SQLBindParameter** per i parametri associati in precedenza. Una chiamata a **SQLBindParameter** per riassociare un parametro modifica l'indirizzo del buffer e il puntatore di lunghezza/indicatore. Il riassociazione con un offset, d'altra parte, aggiunge semplicemente un offset all'indirizzo del buffer dei parametri associati esistente e all'indirizzo del buffer di lunghezza/indicatore. Quando si utilizzano gli offset, i binding sono un "modello" di come sono disposti i buffer dell'applicazione e l'applicazione può spostare questo "modello" in aree di memoria diverse modificando l'offset. Un nuovo offset può essere specificato in qualsiasi momento e viene sempre aggiunto ai valori associati originariamente.  
  
 Per specificare un offset di binding, l'applicazione imposta l'attributo dell'istruzione SQL_ATTR_PARAM_BIND_OFFSET_PTR sull'indirizzo di un buffer SQLINTEGER. Prima che l'applicazione chiami una funzione che usa i binding, inserisce un offset in byte in questo buffer, purché né l'indirizzo del buffer dei parametri né l'indirizzo del buffer di lunghezza/indicatore è 0 e il parametro associato è nell'istruzione SQL. La somma dell'indirizzo e dell'offset deve essere un indirizzo valido. Ciò significa che sia l'offset che l'indirizzo a cui viene aggiunto l'offset possono essere non validi, purché la somma sia un indirizzo valido.  
  
> [!NOTE]  
>  Gli offset di binding non sono supportati da ODBC 2. driver *x* .
