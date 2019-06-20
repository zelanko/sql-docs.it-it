---
title: Offset di associazione di parametri | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f1fd069336a52b0a27ae927880f749c02d2c1d43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62998923"
---
# <a name="parameter-binding-offsets"></a>Offset di associazione di parametri
Un'applicazione può specificare che un offset venga aggiunto all'associazione parametro buffer indirizzi e lunghezza/indicatore corrispondente buffer indirizzi quando **SQLExecDirect** oppure **SQLExecute** viene chiamato. Il risultato di queste aggiunte determina gli indirizzi usati in queste operazioni.  
  
 Offset di associazione consentono a un'applicazione modificare le associazioni senza chiamare **SQLBindParameter** per parametri associati in precedenza. Una chiamata a **SQLBindParameter** per riassociare un parametro viene modificato l'indirizzo del buffer e il puntatore di lunghezza/indicatore. Riassociazione con un offset, d'altra parte, semplicemente aggiunge un offset per l'indirizzo del buffer parametri associati esistenti e indirizzo di buffer di lunghezza/indicatore. Quando vengono utilizzati gli offset, le associazioni sono un "modello" della modalità di disposizione i buffer dell'applicazione e l'applicazione può passare questa "modello" a diverse aree di memoria tramite la modifica dell'offset. Un nuovo offset può essere specificato in qualsiasi momento e viene sempre aggiunto ai valori originariamente associati.  
  
 Per specificare un offset di associazione, l'applicazione imposta l'attributo di istruzione SQL_ATTR_PARAM_BIND_OFFSET_PTR all'indirizzo di un buffer SQLINTEGER. Prima che l'applicazione chiama una funzione che usa le associazioni, posiziona un offset in byte di questo buffer, purché l'indirizzo del buffer parametro né l'indirizzo del buffer di lunghezza/indicatore è 0 e il parametro associato è presente l'istruzione SQL. La somma dell'indirizzo e l'offset deve essere un indirizzo valido. (Ciò significa che uno o entrambi l'offset e l'indirizzo a cui viene aggiunta l'offset può essere valide, purché la somma è un indirizzo valido).  
  
> [!NOTE]  
>  Offset di associazione non sono supportati da ODBC 2. *x* driver.
