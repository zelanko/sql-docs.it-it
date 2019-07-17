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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e59db823f8b84edfb5c92f2d142c8238449e3323
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107583"
---
# <a name="setting-the-transaction-isolation-level"></a>Impostazione del livello di isolamento delle transazioni
Per impostare il livello di isolamento delle transazioni, un'applicazione usa l'attributo di connessione SQL_ATTR_TXN_ISOLATION. Se l'origine dati non supporta il livello di isolamento richiesto, il driver o l'origine dati è possibile impostare un livello superiore. Per determinare quali isolamento della transazione i livelli di un'origine dati supporta e quali il livello di isolamento predefinito è, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_TXN_ISOLATION_OPTION e SQL_DEFAULT_TXN_ISOLATION, rispettivamente.  
  
 Livelli di isolamento della transazione più elevati offrono la massima protezione per l'integrità dei dati del database. Le transazioni serializzabili sono garantite sarà interessato da altre transazioni e pertanto garantite per mantenere l'integrità del database.  
  
 Tuttavia, un livello superiore di isolamento delle transazioni può provocare prestazioni più lente poiché aumenta le probabilità che l'applicazione dovrà attendere i blocchi sui dati da rilasciare. Un'applicazione può specificare un livello inferiore di isolamento per migliorare le prestazioni nei casi seguenti:  
  
-   Quando si può garantire che nessun altro sono presenti transazioni che potrebbero interferire con le transazioni di un'applicazione. Questa situazione si verifica solo in circostanze limitate, ad esempio quando una persona in una piccola azienda mantiene i file dBASE contenenti i dati sul personale in un unico computer e non condivide tali file.  
  
-   Quando è più importanti di accuratezza ed eventuali errori di velocità è probabile che sia di dimensioni ridotte. Ad esempio, si supponga che un'azienda rende molti piccoli sales e che le vendite di grandi dimensioni sono rare. Una transazione che stima il valore totale delle vendite di tutto aprire potrebbe essere usare in modo sicuro il livello di isolamento Read Uncommitted. Anche se la transazione includerà gli ordini che sono in fase di apertura o chiusura e successivamente eseguito il rollback, si sarebbe in genere annullano reciprocamente e la transazione sarebbe molto più veloce perché non è bloccato ogni volta che si rileva un ordine di questo tipo.  
  
 Per altre informazioni, vedere [la concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md).
