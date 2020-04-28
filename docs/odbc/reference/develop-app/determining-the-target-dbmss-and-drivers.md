---
title: Determinazione dei sistemi DBMS e dei driver di destinazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- target DBMSs and drivers in interoperability [ODBC]
- interoperability [ODBC], target dbmss and drivers
ms.assetid: 23bee0f6-e12a-4598-b34e-df11a8086829
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f8811e4d289a8fc89c2c3773aab973df523025f5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305872"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinazione dei DBMS e dei driver di destinazione
La domanda successiva da considerare è, quali sono i DBMS di destinazione per l'applicazione e quali sono i driver disponibili che supportano questi sistemi DBMS? Poiché le applicazioni generiche tendono a essere altamente interoperative, la questione dei DBMS di destinazione è la più applicabile alle applicazioni personalizzate e verticali. Tuttavia, la domanda dei driver di destinazione si applica a tutte le applicazioni, perché i driver variano notevolmente in velocità, qualità, supporto delle funzionalità e disponibilità. Inoltre, se i driver devono essere ridistribuiti con l'applicazione, è necessario prendere in considerazione il costo e la disponibilità dei piani di licenza.  
  
 Per molte applicazioni personalizzate, i DBMS di destinazione sono ovvi: sono DBMS esistenti a cui l'applicazione è progettata per accedere. Devono essere presi in considerazione anche i DBMS a cui è pianificata la migrazione futura. Tuttavia, la domanda principale per queste applicazioni è il driver o i driver da usare con loro. Per altre applicazioni personalizzate, ovvero quelle che non sono progettate per accedere a un sistema DBMS esistente, è possibile scegliere i DBMS di destinazione in base al supporto delle funzionalità, al supporto utente simultaneo, alla disponibilità dei driver e all'accessibilità.  
  
 Per le applicazioni verticali, i DBMS di destinazione vengono in genere scelti in base al supporto delle funzionalità, alla disponibilità dei driver e al mercato. Un'applicazione verticale progettata per le piccole imprese, ad esempio, deve essere destinata a DBMS accessibili a tali aziende; un'applicazione verticale progettata come componente aggiuntivo per i DBMS esistenti deve essere destinata a DBMS ampiamente diffusi.  
  
 Quando si scelgono i DBMS di destinazione, è necessario considerare le differenze tra i database desktop e server. I database desktop come dBASE, Paradox e Btrieve sono meno potenti dei database server. Poiché in genere si accede ai motori SQL meno potenti disponibili nella maggior parte dei driver basati su file, spesso manca il supporto completo delle transazioni, supporta un minor numero di utenti simultanei e SQL limitato. Tuttavia, sono poco costosi e hanno una base installata di grandi dimensioni.  
  
 I database server come Oracle, DB2 e SQL Server offrono il supporto completo delle transazioni, supportano molti utenti simultanei e hanno SQL avanzato. Sono molto più costosi e hanno una base installata di dimensioni minori. D'altra parte, i prezzi del software tendono a essere più elevati, in modo da compensare un mercato potenziale più piccolo.  
  
 In questo modo, è talvolta possibile scegliere i DBMS di destinazione in base alle funzionalità richieste dall'applicazione e al mercato di destinazione dell'applicazione. Ad esempio, un sistema di immissione degli ordini per le aziende di grandi dimensioni potrebbe non essere destinato ai database desktop perché questi non sono idonei per supportare le transazioni. Un sistema simile progettato per le piccole imprese potrebbe escludere la maggior parte dei database del server in base ai costi. E gli sviluppatori di applicazioni generiche possono essere destinati a entrambi, ma evitare di usare le funzionalità avanzate disponibili nei database del server.
