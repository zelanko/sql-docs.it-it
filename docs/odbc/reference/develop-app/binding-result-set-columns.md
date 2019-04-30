---
title: Colonne del Set di risultati di associazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: 4bc9c30f-83ae-4766-a746-032953c187ad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b92f317d72410a5dff56652dd9de1e3b2ba5c9cb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199278"
---
# <a name="binding-result-set-columns"></a>Associazione di colonne di set di risultati
Le applicazioni possono associare come colonne di tipo numero indefinito del set di risultati a propria scelta, tra cui non associazione colonne affatto. Quando viene recuperata una riga di dati, il driver restituisce i dati per le colonne associate all'applicazione. Indica se l'applicazione associa tutte le colonne nel set di risultati dipende dall'applicazione. Ad esempio, le applicazioni che generano report in genere hanno un formato fisso; tali applicazioni creare un set di risultati contenente tutte le colonne utilizzate nel rapporto e quindi eseguire l'associazione e recuperano i dati per tutte queste colonne. Applicazioni che consentono di visualizzare le schermate completa dei dati in alcuni casi consentono all'utente di decidere le colonne da visualizzare. tali applicazioni creano un set di risultati contenente tutte le colonne utente valuti, ma eseguire l'associazione e recuperare i dati solo per le colonne scelte dall'utente.  
  
 Dati possono essere recuperati da colonne non associate, chiamare **SQLGetData**. Ciò in genere viene chiamato per recuperare dati long, che spesso superano la lunghezza di un singolo buffer e devono essere recuperati in parti.  
  
 È possibile associare le colonne in qualsiasi momento, anche dopo le righe recuperate. Tuttavia, le nuove associazioni non sono effettive fino al successivo che viene recuperata una riga; essi non vengono applicate ai dati da righe già recuperate.  
  
 Una variabile rimane associata a una colonna fino a quando una variabile diversa è associata alla colonna, fino a quando non la colonna è stata annullata chiamando **SQLBindCol** con un puntatore null come indirizzo della variabile, fino a quando tutte le colonne non sono associate chiamando **SQLFreeStmt** con l'opzione SQL_UNBIND o finché non viene rilasciato l'istruzione. Per questo motivo, l'applicazione deve assicurarsi che tutte le variabili associate rimangono valide fino a quando sono associate. Per altre informazioni, vedere [allocazione e liberazione di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Poiché le associazioni di colonna sono solo le informazioni associate alla struttura di istruzione, possono essere impostate in qualsiasi ordine. Sono anche indipendenti del set di risultati. Si supponga, ad esempio, che un'applicazione associa le colonne del set di risultati generato dall'istruzione SQL seguente:  
  
```  
SELECT * FROM Orders  
```  
  
 Se l'applicazione esegue quindi l'istruzione SQL  
  
```  
SELECT * FROM Lines  
```  
  
 sullo stesso handle di istruzione, le associazioni di colonna per il primo set di risultati sono ancora attive perché queste sono le associazioni archiviate nella struttura di istruzione. Nella maggior parte dei casi, questa è una pratica di programmazione scarsa e deve essere evitata. Al contrario, l'applicazione deve chiamare **SQLFreeStmt** con l'opzione SQL_UNBIND a disassocia tutte le colonne precedenti e quindi associare nuovi.
