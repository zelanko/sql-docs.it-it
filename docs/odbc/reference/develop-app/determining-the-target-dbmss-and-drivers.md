---
title: Per determinare il DBMS di destinazione e i driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7065aa88d60a508df9946d38d0dded220c4bb7a1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106144"
---
# <a name="determining-the-target-dbmss-and-drivers"></a>Determinazione dei DBMS e dei driver di destinazione
La domanda successiva da prendere in considerazione è, quali sono il DBMS di destinazione per l'applicazione e quali driver sono disponibili che supportano tali DBMS? Poiché applicazioni generiche tendono a essere estremamente interoperativi, la questione del DBMS di destinazione è più applicabile alle applicazioni personalizzate e verticale. Tuttavia, la domanda dei driver di destinazione si applica a tutte le applicazioni, poiché i driver variano notevolmente in velocità, qualità, il supporto delle funzionalità e disponibilità. Inoltre, se i driver devono essere ridistribuito con l'applicazione, i costi e la disponibilità di piani di contratti multilicenza dovranno essere considerati.  
  
 Per molte applicazioni personalizzate, la destinazione DBMS sono evidenti: Essi sono esistenti DBMS che l'applicazione è progettata per accedere. Deve essere considerato anche DBMS in cui è pianificata migrazione futura. Tuttavia, la domanda importante per queste applicazioni è che i driver da usare con essi. Per altre applicazioni personalizzate: quelli che non sono progettati per accedere a un DBMS esistente - il DBMS di destinazione può essere scelto in base a supporto delle funzionalità, il supporto di utenti simultanei, la disponibilità di driver e convenienza.  
  
 Per le applicazioni verticali, la destinazione di che DBMS in genere vengono scelti in base il supporto delle funzionalità, la disponibilità di driver e sul mercato. Ad esempio, un'applicazione di verticale progettata per le piccole imprese deve avere come destinazione DBMS che sono accessibili da tali aziende; un'applicazione verticale progettata come componente aggiuntivo di DBMS esistente deve avere come destinazione ampiamente usato DBMS.  
  
 Quando si sceglie di DBMS di destinazione, le differenze tra i database desktop e server devono essere considerate. I database desktop, ad esempio Paradox, dBASE e Btrieve sono meno potenti rispetto ai database del server. Poiché in genere sono accessibili attraverso i meno potenti motori SQL trovati nel driver più basati su file, spesso non includono il supporto delle transazioni pieno, supportano un minor numero di utenti simultanei e non dispongono di SQL. Tuttavia, sono poco costose e hanno una grande base installata.  
  
 Server database, ad esempio Oracle, DB2 e SQL Server forniscono il supporto delle transazioni pieno, supportano molti utenti simultanei e hanno SQL avanzate. Sono molto più costose e avere una base installata più piccoli. D'altra parte, i prezzi di software tendono a essere superiore, l'offset in qualche modo un mercato potenziale più piccolo.  
  
 Di conseguenza, destinazione DBMS in alcuni casi può essere scelto in base le funzionalità richieste dall'applicazione e il mercato di destinazione dell'applicazione. Ad esempio, un sistema di immissione dell'ordine per le aziende di grandi dimensioni potrebbe non essere destinati i database desktop perché questi non dispongono di supporto delle transazioni sufficiente. Un simile sistema progettato per le piccole imprese potrà escludere la maggior parte dei database del server in base ai costi. E gli sviluppatori di applicazioni generiche potrebbero entrambi come destinazione, ma evitare di utilizzare le caratteristiche avanzate presenti nel database del server.
