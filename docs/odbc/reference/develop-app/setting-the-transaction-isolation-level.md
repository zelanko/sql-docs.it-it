---
title: Impostazione del livello di isolamento della transazione Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- isolation levels [ODBC]
- transaction isolation [ODBC]
- transactions [ODBC], isolation
ms.assetid: 64a037f0-5065-4f45-9669-6710404a540c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 80401b276355a47469355cb6921d768d168398ae
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299811"
---
# <a name="setting-the-transaction-isolation-level"></a>Impostazione del livello di isolamento delle transazioni
Per impostare il livello di isolamento della transazione, un'applicazione utilizza l'attributo di connessione SQL_ATTR_TXN_ISOLATION. Se l'origine dati non supporta il livello di isolamento richiesto, il driver o l'origine dati può impostare un livello superiore. Per determinare i livelli di isolamento delle transazioni supportati da un'origine dati e il livello di isolamento predefinito, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_TXN_ISOLATION_OPTION e SQL_DEFAULT_TXN_ISOLATION, rispettivamente.  
  
 Livelli più elevati di isolamento delle transazioni offrono la massima protezione per l'integrità dei dati del database. Le transazioni serializzabili sono garantite per non essere influenzate da altre transazioni e pertanto garantite per mantenere l'integrità del database.  
  
 Tuttavia, un livello più elevato di isolamento delle transazioni può causare un miglioramento delle prestazioni perché aumenta le probabilità che l'applicazione debba attendere il rilascio dei blocchi sui dati. Un'applicazione può specificare un livello di isolamento inferiore per migliorare le prestazioni nei casi seguenti:An application can specify a lower level of isolation to increase performance in the following cases:  
  
-   Quando è possibile garantire che non esistano altre transazioni che potrebbero interferire con le transazioni di un'applicazione. Questa situazione si verifica solo in circostanze limitate, ad esempio quando una persona in una piccola azienda gestisce i file dBASE che contengono i dati sul personale su un computer e non condivide questi file.  
  
-   Quando la velocità è più critica della precisione ed eventuali errori sono probabilmente piccoli. Si supponga, ad esempio, che un'azienda effettui molte piccole vendite e che le vendite di grandi dimensioni siano rare. Una transazione che stima il valore totale di tutte le vendite aperte potrebbe utilizzare in modo sicuro il livello di isolamento Lettura senza commit. Anche se la transazione includerebbe gli ordini che vengono aperti o chiusi e che vengono successivamente sottoposti a rollback, questi in genere si annullano a vicenda e la transazione sarebbe molto più veloce perché non viene bloccata ogni volta che rileva tale ordine.  
  
 Per ulteriori informazioni, vedere [Concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md).
