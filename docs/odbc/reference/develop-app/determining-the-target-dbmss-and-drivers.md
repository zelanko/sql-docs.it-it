---
title: Determinazione dei DBSMO e dei driver di destinazione Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305872"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinazione dei DBMS e dei driver di destinazione
La domanda successiva da considerare è: quali sono i DBSMO di destinazione per l'applicazione e quali driver sono disponibili che supportano tali DBSMO? Poiché le applicazioni generiche tendono ad essere altamente interoperabili, la questione dei DBSMO di destinazione è più applicabile alle applicazioni personalizzate e verticali. Tuttavia, la questione dei driver di destinazione si applica a tutte le applicazioni, perché i driver variano ampiamente in termini di velocità, qualità, supporto delle funzionalità e disponibilità. Inoltre, se i driver devono essere ridistribuiti con l'applicazione, è necessario considerare il costo e la disponibilità dei piani di licenza.  
  
 Per molte applicazioni personalizzate, i DBSMO di destinazione sono ovvi: sono DBSMO esistenti a cui l'applicazione è progettata per accedere. Occorre considerare anche i DBSMO a cui è pianificata la migrazione futura. Tuttavia, la domanda principale per queste applicazioni è quale driver o driver da utilizzare con loro. Per altre applicazioni personalizzate, ovvero quelle non progettate per accedere a un sistema DBMS esistente, i DBMS di destinazione possono essere scelti in base al supporto delle funzionalità, al supporto utente simultaneo, alla disponibilità dei driver e all'accessibilità.  
  
 Per le applicazioni verticali, i DBSMO di destinazione vengono in genere scelti in base al supporto delle funzionalità, alla disponibilità dei driver e al mercato. Ad esempio, un'applicazione verticale progettata per le piccole imprese deve essere destinata a i DBSMO accessibili a tali aziende; un'applicazione verticale progettata come componente aggiuntivo per i DBSMO esistenti deve essere destinata a DBS ampiamente utilizzati.  
  
 Quando si sceglie i DBSMO di destinazione, è necessario considerare le differenze tra i database desktop e server. I database desktop come dBASE, Paradox e Btrieve sono meno potenti dei database server. Poiché in genere è possibile accedervi tramite i motori SQL meno potenti disponibili nella maggior parte dei driver basati su file, spesso mancano di supporto completo per le transazioni, supportano un numero inferiore di utenti simultanei e hanno SQL limitato. Tuttavia, sono poco costosi e hanno una grande base installata.  
  
 I database server come Oracle, DB2 e SQL Server forniscono supporto completo per le transazioni, supportano molti utenti simultanei e dispongono di SQL avanzato. Sono molto più costosi e hanno una base installata più piccola. D'altra parte, i prezzi del software tendono ad essere più alti, un po 'compensando un mercato potenziale più piccolo.  
  
 Pertanto, i DBSMO di destinazione a volte possono essere scelti in base alle funzionalità richieste dall'applicazione e dal mercato di destinazione dell'applicazione. Ad esempio, un sistema di registrazione degli ordini per le aziende di grandi dimensioni potrebbe non essere destinato ai database desktop perché questi non dispongono di un supporto adeguato per le transazioni. Un sistema simile progettato per le piccole imprese potrebbe escludere la maggior parte dei database server in base ai costi. E gli sviluppatori di applicazioni generiche potrebbero indirizzare entrambi, ma evitare di utilizzare le funzionalità avanzate trovate nei database server.
