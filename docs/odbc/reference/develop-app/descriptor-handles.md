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
ms.openlocfilehash: 24e3d4c87f3bc461a339a6cb635d64f20dc73e20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106157"
---
# <a name="descriptor-handles"></a>Handle del descrittore
Un *descrittore* è una raccolta di metadati che descrive i parametri di un'istruzione SQL o le colonne di un set di risultati, come osservato dall'applicazione o dal driver (noto anche come *implementazione*). Pertanto, un descrittore può riempire uno dei quattro ruoli:  
  
-   **Descrittore del parametro dell'applicazione (APD).** Contiene informazioni sui buffer dell'applicazione associati ai parametri in un'istruzione SQL, ad esempio i relativi indirizzi, lunghezze e tipi di dati C.  
  
-   **Descrittore del parametro di implementazione (dpi).** Contiene informazioni sui parametri in un'istruzione SQL, ad esempio i tipi di dati SQL, le lunghezze e il supporto di valori null.  
  
-   **Descrittore di riga dell'applicazione (ARD).** Contiene informazioni sui buffer dell'applicazione associati alle colonne di un set di risultati, ad esempio indirizzi, lunghezze e tipi di dati C.  
  
-   **Descrittore della riga di implementazione (IRD).** Contiene informazioni sulle colonne di un set di risultati, ad esempio i tipi di dati, le lunghezze e il supporto di valori null.  
  
 I quattro descrittori (uno che riempie ogni ruolo) vengono allocati automaticamente quando viene allocata un'istruzione. Questi sono noti come *descrittori allocati automaticamente* e sono sempre associati a tale istruzione. Le applicazioni possono inoltre allocare descrittori con **SQLAllocHandle**. Questi sono noti come *descrittori allocati in modo esplicito*. Vengono allocate in una connessione e possono essere associate a una o più istruzioni su tale connessione per soddisfare il ruolo di un oggetto APD o ARD su tali istruzioni.  
  
 La maggior parte delle operazioni in ODBC può essere eseguita senza l'utilizzo esplicito di descrittori da parte dell'applicazione. Tuttavia, i descrittori forniscono un comodo collegamento per alcune operazioni. Si supponga, ad esempio, che un'applicazione voglia inserire dati da due diversi set di buffer. Per usare il primo set di buffer, chiama ripetutamente **SQLBindParameter** per associarli ai parametri in un'istruzione **Insert** , quindi eseguire l'istruzione. Per usare il secondo set di buffer, questo processo viene ripetuto. In alternativa, è possibile impostare Binding per il primo set di buffer in un descrittore e per il secondo set di buffer in un altro descrittore. Per spostarsi tra i set di binding, l'applicazione chiama semplicemente **SQLSetStmtAttr** e associa il descrittore corretto all'istruzione come APD.  
  
 Per ulteriori informazioni sui descrittori, vedere [tipi di descrittori](../../../odbc/reference/develop-app/types-of-descriptors.md).
