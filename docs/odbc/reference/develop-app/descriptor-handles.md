---
title: Handle descrittore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application parameter descriptor [ODBC]
- automatically allocated descriptors [ODBC]
- implementation row descriptor [ODBC]
- descriptor handles [ODBC]
- handles [ODBC], descriptor
- implementation parameter descriptor [ODBC]
- apd [ODBC]
- ard [ODBC]
- explicitly allocated descriptors [ODBC]
- ipd [ODBC]
- ird [ODBC]
- application row descriptor [ODBC]
ms.assetid: 7741035c-f3e7-4c89-901e-fe528392f67d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3aa085cc0a098f557ca7a8cbddcd787a178b79d0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760766"
---
# <a name="descriptor-handles"></a>Handle del descrittore
Oggetto *descrittore* è una raccolta di metadati che descrivono i parametri di un'istruzione SQL o le colonne di un set di risultati, come illustrato per l'applicazione o il driver (noto anche come il *implementazione*). Di conseguenza, un descrittore può compilare uno qualsiasi dei quattro ruoli:  
  
-   **Descrittore di parametri dell'applicazione (APD).** Contiene informazioni sui buffer di applicazione associate ai parametri in un'istruzione SQL, ad esempio relativi indirizzi, le lunghezze e tipi di dati C.  
  
-   **Descrizione del parametro di implementazione (IPD).** Contiene informazioni sui parametri in un'istruzione SQL, ad esempio i tipi di dati SQL, le lunghezze e supporto dei valori null.  
  
-   **Descrittore delle righe dell'applicazione (ARD).** Contiene informazioni sui buffer di applicazione associati alle colonne in un set di risultati, ad esempio relativi indirizzi, le lunghezze e tipi di dati C.  
  
-   **Descrittore riga di implementazione (IRD).** Contiene informazioni sulle colonne in un set di risultati, ad esempio i tipi di dati SQL, le lunghezze e supporto di valori null.  
  
 I descrittori di quattro (un riempimento di ogni ruolo) vengono allocati automaticamente quando viene allocata un'istruzione. Si parla *allocato automaticamente descrittori* e sempre associate a tale istruzione. Le applicazioni possono inoltre allocare descrittori con **SQLAllocHandle**. Si parla *allocata in modo esplicito i descrittori*. Essi vengono allocate in una connessione e può essere associati a una o più istruzioni in tale connessione per soddisfare il ruolo di un APD o ARD su tali istruzioni.  
  
 La maggior parte delle operazioni in ODBC possono essere eseguite senza l'utilizzo esplicito di descrittori di dall'applicazione. Tuttavia, i descrittori forniscono un comodo collegamento per alcune operazioni. Si supponga, ad esempio, che un'applicazione vuole inserire i dati da due set diversi di buffer. Per usare il primo set di buffer, doveva chiamare ripetutamente **SQLBindParameter** associazione ai parametri in un **Inserisci** istruzione e quindi eseguire l'istruzione. Per usare il secondo set di buffer, è necessario ripetere questo processo. In alternativa, è possibile configurare le associazioni per il primo set di buffer nel descrittore di uno e il secondo set di buffer nel descrittore di un altro. Per passare tra i set di associazioni, l'applicazione chiama semplicemente **SQLSetStmtAttr** e associare il descrittore corretto con l'istruzione come APD.  
  
 Per altre informazioni sui descrittori, vedere [tipi di descrittori](../../../odbc/reference/develop-app/types-of-descriptors.md).
