---
title: Informazioni su ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], about ODBC
ms.assetid: badf3a45-f941-44ae-a31d-393116f68a18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc9c7a3d9f75e1863d90b16986234e0036229d01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62714093"
---
# <a name="what-is-odbc"></a>Informazioni su ODBC
Molti pregiudizi ODBC esistono in tutto il mondo informatico. Per l'utente finale, è un'icona nel Pannello di controllo Microsoft® Windows®. Per i programmatori di applicazioni è una libreria che contiene la routine di accesso ai dati. Per molti altri, è la risposta a tutti i problemi di accesso di database che mai immaginato in precedenza.  
  
 Prima di tutto, ODBC è una specifica per un'API di database. Questa API è indipendente da qualsiasi un DBMS o sistema operativo. anche se questo manuale Usa C, l'API ODBC è indipendente dal linguaggio. L'API ODBC si basa sulle specifiche dell'interfaccia della riga da Open Group e ISO/IEC. ODBC 3. *x* completamente implementa entrambe queste specifiche - versioni precedenti di ODBC sono basate su versioni preliminari di queste specifiche ma non viene tuttavia implementata completamente - e aggiunge funzionalità comunemente necessarie per gli sviluppatori di su schermo applicazioni di database, ad esempio cursori scorrevoli.  
  
 Le funzioni dell'API ODBC vengono implementate dagli sviluppatori di driver specifici del DBMS. Applicazioni di chiamare le funzioni in questi driver per accedere ai dati in modo indipendente dal sistema DBMS. Un Driver Manager gestisce la comunicazione tra applicazioni e driver.  
  
 Sebbene Microsoft offre una Gestione driver per i computer che eseguono Microsoft Windows® 95 e versioni successive, ha scritto diversi driver ODBC e chiama funzioni ODBC da alcune delle relative applicazioni, chiunque può scrivere i driver e le applicazioni ODBC. In effetti, la maggior parte delle applicazioni ODBC e driver disponibili oggi vengono scritti da parte delle aziende diverse da Microsoft. Inoltre, le applicazioni e driver ODBC presenti nel Macintosh® e un'ampia gamma di piattaforme UNIX.  
  
 Per aiutare gli sviluppatori di applicazioni e driver, Microsoft offre un ODBC Software Development Kit (SDK) per i computer che eseguono Windows 95 e versioni successive che fornisce la gestione driver, DLL di installazione, gli strumenti di test e applicazioni di esempio. Microsoft ha creato un team con Visigenic Software convertire questi SDK per Macintosh e un'ampia gamma di piattaforme UNIX.  
  
 È importante comprendere che ODBC è progettato per esporre le funzionalità di database, non completarli. Di conseguenza, gli autori di applicazioni non aspettarsi che l'utilizzo di ODBC trasformerà improvvisamente un database semplice in un motore di database relazionale completamente in primo piano. Né gli sviluppatori di driver devono implementare funzionalità non trovata nel database sottostante. Un'eccezione è che gli sviluppatori che scrivono i driver che accedono direttamente ai dati dei file (ad esempio, i dati in un file Xbase) sono necessari per scrivere un motore di database che supporta la funzionalità SQL almeno minima. Un'altra eccezione è che il componente ODBC di Windows SDK, incluse in precedenza il SDK in Microsoft Data Access Components (MDAC), fornisce una libreria di cursori che simula i cursori scorrevoli per i driver che implementano un certo livello di funzionalità.  
  
 Le applicazioni che utilizzano ODBC sono tenute a qualsiasi funzionalità tra database. Ad esempio ODBC non è un motore di join eterogeneo, né si tratta di un'elaborazione delle transazioni distribuite. Tuttavia, poiché è indipendente dal sistema DBMS, può essere utilizzato per compilare tali strumenti tra database.
