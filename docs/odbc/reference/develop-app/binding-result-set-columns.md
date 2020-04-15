---
title: Colonne del set di risultati di associazione Documenti Microsoft
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
ms.openlocfilehash: 558ceb79d42d82477b70a028395de82cc023c170
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306362"
---
# <a name="binding-result-set-columns"></a>Associazione di colonne di set di risultati
Le applicazioni possono associare il numero o il numero di colonne del set di risultati che preferiscono, inclusa l'associazione di nessuna colonna. Quando viene recuperata una riga di dati, il driver restituisce i dati per le colonne associate all'applicazione. Se l'applicazione associa tutte le colonne nel set di risultati dipende dall'applicazione. Ad esempio, le applicazioni che generano report hanno in genere un formato fisso; tali applicazioni creano un set di risultati contenente tutte le colonne utilizzate nel report, quindi associano e recuperano i dati per tutte queste colonne. Le applicazioni che visualizzano schermate piene di dati a volte consentono all'utente di decidere quali colonne visualizzare; tali applicazioni creano un set di risultati contenente tutte le colonne desiderate dall'utente, ma associano e recuperano i dati solo per le colonne scelte dall'utente.  
  
 I dati possono essere recuperati da colonne non associate chiamando **SQLGetData**. Questo è comunemente chiamato per recuperare i dati lunghi, che spesso supera la lunghezza di un singolo buffer e deve essere recuperato in parti.  
  
 Le colonne possono essere associate in qualsiasi momento, anche dopo il recupero delle righe. Tuttavia, le nuove associazioni non hanno effetto fino alla successiva recupero di una riga; non vengono applicati ai dati delle righe già recuperate.  
  
 Una variabile rimane associata a una colonna fino a quando non viene associata una variabile diversa alla colonna, fino a quando la colonna non viene associata chiamando **SQLBindCol** con un puntatore null come indirizzo della variabile, fino a quando tutte le colonne non vengono associate chiamando **SQLFreeStmt** con l'opzione SQL_UNBIND o fino a quando non viene rilasciata l'istruzione. Per questo motivo, l'applicazione deve assicurarsi che tutte le variabili associate rimangano valide finché sono associate. Per ulteriori informazioni, consultate [Allocazione e liberazione dei buffer.](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)  
  
 Poiché le associazioni di colonna sono solo informazioni associate alla struttura dell'istruzione, possono essere impostate in qualsiasi ordine. Sono inoltre indipendenti dal set di risultati. Si supponga, ad esempio, che un'applicazione esegua l'associazione delle colonne del set di risultati generato dall'istruzione SQL seguente:  
  
```  
SELECT * FROM Orders  
```  
  
 Se l'applicazione esegue quindi l'istruzione SQL  
  
```  
SELECT * FROM Lines  
```  
  
 sullo stesso handle di istruzione, le associazioni di colonna per il primo set di risultati sono ancora attive perché sono le associazioni archiviate nella struttura dell'istruzione. Nella maggior parte dei casi, questa è una pratica di programmazione scadente e dovrebbe essere evitata. Al contrario, l'applicazione deve chiamare **SQLFreeStmt** con l'opzione SQL_UNBIND per annullare l'associazione di tutte le colonne precedenti e quindi associare quelle nuove.
