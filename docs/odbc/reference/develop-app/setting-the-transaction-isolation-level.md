---
title: Impostazione del livello di isolamento delle transazioni | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299811"
---
# <a name="setting-the-transaction-isolation-level"></a>Impostazione del livello di isolamento delle transazioni
Per impostare il livello di isolamento della transazione, un'applicazione utilizza l'attributo di connessione SQL_ATTR_TXN_ISOLATION. Se l'origine dati non supporta il livello di isolamento richiesto, il driver o l'origine dati può impostare un livello superiore. Per determinare i livelli di isolamento delle transazioni supportati da un'origine dati e il livello di isolamento predefinito, un'applicazione chiama rispettivamente **SQLGetInfo** con le opzioni SQL_TXN_ISOLATION_OPTION e SQL_DEFAULT_TXN_ISOLATION.  
  
 Livelli più elevati di isolamento delle transazioni offrono la massima protezione per l'integrità dei dati del database. Le transazioni serializzabili non sono necessariamente interessate da altre transazioni e pertanto garantiscono l'integrità del database.  
  
 Tuttavia, un livello più elevato di isolamento delle transazioni può causare un rallentamento delle prestazioni perché aumenta le probabilità che l'applicazione debba attendere il rilascio dei blocchi sui dati. Un'applicazione può specificare un livello di isolamento inferiore per migliorare le prestazioni nei casi seguenti:  
  
-   Quando è possibile garantire che non esistano altre transazioni che potrebbero interferire con le transazioni di un'applicazione. Questa situazione si verifica solo in circostanze limitate, ad esempio quando una persona di una piccola azienda gestisce file dBASE che contengono dati personali in un computer e non condividono questi file.  
  
-   Quando la velocità è più critica dell'accuratezza ed è probabile che si verifichino errori di dimensioni ridotte. Si supponga, ad esempio, che una società abbia molte vendite di piccole dimensioni e che le vendite di grandi dimensioni siano rare. Una transazione che stima il valore totale di tutte le vendite aperte potrebbe utilizzare in modo sicuro il livello di isolamento READ UNCOMMITTED. Sebbene la transazione includa gli ordini che vengono aperti o chiusi e di cui ne viene eseguito il rollback, in genere vengono annullati e la transazione risulta molto più veloce perché non viene bloccata ogni volta che viene rilevato un ordine di questo tipo.  
  
 Per ulteriori informazioni, vedere [concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md).
