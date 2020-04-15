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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea0aa81188e5e58d3a66032af38700ece2d4e5b4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286501"
---
# <a name="what-is-odbc"></a>Informazioni su ODBC
Molti malintesi su ODBC esistono nel mondo informatico. Per l'utente finale, è un'icona in Microsoft® Windows® Pannello di controllo. Per il programmatore dell'applicazione, è una libreria contenente routine di accesso ai dati. Per molti altri, è la risposta a tutti i problemi di accesso al database mai immaginati.  
  
 In primo luogo, ODBC è una specifica per un'API di database. Questa API è indipendente da qualsiasi DBMS o sistema operativo; anche se questo manuale utilizza C, l'API ODBC è indipendente dalla lingua. L'API ODBC si basa sulle specifiche CLI di Open Group e ISO/IEC. ODBC 3. *x* implementa completamente entrambe queste specifiche - le versioni precedenti di ODBC erano basate su versioni preliminari di queste specifiche, ma non le implementava completamente - e aggiunge le funzionalità comunemente necessarie agli sviluppatori di applicazioni di database basate su schermo, ad esempio cursori scorrevoli.  
  
 Le funzioni nell'API ODBC vengono implementate dagli sviluppatori di driver specifici di DBMS. Le applicazioni chiamano le funzioni in questi driver per accedere ai dati in modo indipendente da DBMS. Gestione driver gestisce la comunicazione tra applicazioni e driver.  
  
 Sebbene Microsoft fornisca un gestore di driver per i computer che eseguono Microsoft Windows® 95 e versioni successive, ha scritto diversi driver ODBC e chiama le funzioni ODBC da alcune delle relative applicazioni, chiunque può scrivere applicazioni e driver ODBC. Infatti, la stragrande maggioranza delle applicazioni ODBC e driver disponibili oggi sono scritti da società diverse da Microsoft. Inoltre, i driver e le applicazioni ODBC esistono in Macintosh® e una varietà di piattaforme UNIX.  
  
 Per facilitare gli sviluppatori di applicazioni e driver, Microsoft offre un SDK (Software Development Kit) ODBC per i computer che eseguono Windows 95 e versioni successive che fornisce gestione driver, DLL del programma di installazione, strumenti di test e applicazioni di esempio. Microsoft ha collaborato con Visigenic Software per portare questi SDK in Macintosh e una varietà di piattaforme UNIX.  
  
 È importante comprendere che ODBC è progettato per esporre le funzionalità del database, non integrarle. Pertanto, i writer di applicazioni non devono aspettarsi che l'utilizzo di ODBC improvvisamente trasformare un database semplice in un motore di database relazionale completamente in primo piano. Né si prevede che i writer di driver implementino funzionalità non presenti nel database sottostante. Un'eccezione è che gli sviluppatori che scrivono i driver che accedono direttamente ai dati dei file (ad esempio i dati in un file Xbase) sono necessari per scrivere un motore di database che supporta almeno la funzionalità SQL minima. Un'altra eccezione è che il componente ODBC di Windows SDK, precedentemente incluso in Microsoft Data Access Components (MDAC), fornisce una libreria di cursori che simula cursori scorrevoli per i driver che implementano un determinato livello di funzionalità.  
  
 Le applicazioni che utilizzano ODBC sono responsabili di qualsiasi funzionalità tra database. Ad esempio, ODBC non è un motore di join eterogeneo, né un processore di transazioni distribuito. Tuttavia, poiché è indipendente da DBMS, può essere utilizzato per creare tali strumenti di database incrociati.
