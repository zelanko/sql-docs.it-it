---
description: Associazione di colonne di set di risultati
title: Colonne del set di risultati di associazione | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6a228de81deb5cdfdaa62ee7940185b14bcaef8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499944"
---
# <a name="binding-result-set-columns"></a>Associazione di colonne di set di risultati
Le applicazioni possono associare il numero di colonne del set di risultati che scelgono, inclusa l'associazione di nessuna colonna. Quando viene recuperata una riga di dati, il driver restituisce i dati per le colonne con binding all'applicazione. Il fatto che l'applicazione associ tutte le colonne nel set di risultati dipende dall'applicazione. Ad esempio, le applicazioni che generano report hanno in genere un formato fisso; in tali applicazioni viene creato un set di risultati contenente tutte le colonne utilizzate nel report, quindi vengono associati e recuperati i dati per tutte le colonne. Le applicazioni che visualizzano le schermate piene dei dati a volte consentono all'utente di decidere quali colonne visualizzare; tali applicazioni creano un set di risultati contenente tutte le colonne desiderate dall'utente, ma associano e recuperano i dati solo per le colonne scelte dall'utente.  
  
 I dati possono essere recuperati da colonne non vincolate chiamando **SQLGetData**. Questa operazione viene comunemente chiamata per recuperare dati Long, che spesso superano la lunghezza di un singolo buffer e devono essere recuperati in parti.  
  
 È possibile associare le colonne in qualsiasi momento, anche dopo il recupero delle righe. Tuttavia, le nuove associazioni non diventano effettive fino alla successiva recupero di una riga; non vengono applicati ai dati delle righe già recuperate.  
  
 Una variabile rimane associata a una colonna fino a quando non viene associata a una variabile diversa, fino a quando la colonna non è associata chiamando **SQLBindCol** con un puntatore null come indirizzo della variabile, fino a quando tutte le colonne non sono associate chiamando **SQLFreeStmt** con l'opzione SQL_UNBIND o fino a quando l'istruzione non viene rilasciata. Per questo motivo, l'applicazione deve assicurarsi che tutte le variabili associate rimangano valide fino a quando vengono associate. Per altre informazioni, vedere [allocazione e liberazione dei buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md).  
  
 Poiché le associazioni di colonna sono semplicemente informazioni associate alla struttura dell'istruzione, possono essere impostate in qualsiasi ordine. Sono inoltre indipendenti dal set di risultati. Si supponga, ad esempio, che un'applicazione associ le colonne del set di risultati generato dall'istruzione SQL seguente:  
  
```  
SELECT * FROM Orders  
```  
  
 Se l'applicazione esegue quindi l'istruzione SQL  
  
```  
SELECT * FROM Lines  
```  
  
 nello stesso handle di istruzione, le associazioni di colonna per il primo set di risultati sono ancora attive perché si tratta delle associazioni archiviate nella struttura dell'istruzione. Nella maggior parte dei casi, si tratta di una procedura di programmazione insufficiente e deve essere evitata. Al contrario, l'applicazione deve chiamare **SQLFreeStmt** con l'opzione SQL_UNBIND per annullare il binding di tutte le colonne precedenti e quindi associarne di nuove.
