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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286501"
---
# <a name="what-is-odbc"></a>Informazioni su ODBC
Molti equivoci su ODBC sono disponibili nel mondo informatico. Per l'utente finale, è un'icona del pannello di controllo di Microsoft® Windows®. Al programmatore di applicazioni, si tratta di una libreria che contiene routine di accesso ai dati. Per molti altri, è la risposta a tutti i problemi di accesso al database mai immaginati.  
  
 In primo luogo, ODBC è una specifica per un'API di database. Questa API è indipendente da un sistema operativo o DBMS. Sebbene in questo manuale venga utilizzato C, l'API ODBC è indipendente dal linguaggio. L'API ODBC si basa sulle specifiche dell'interfaccia della riga di comando di Open Group e ISO/IEC. ODBC 3. *x* implementa completamente entrambe le specifiche. le versioni precedenti di ODBC sono basate su versioni preliminari di queste specifiche, ma non sono state implementate completamente, e aggiungono funzionalità generalmente richieste dagli sviluppatori di applicazioni di database basate su schermo, ad esempio cursori scorrevoli.  
  
 Le funzioni nell'API ODBC sono implementate dagli sviluppatori di driver specifici del sistema DBMS. Le applicazioni chiamano le funzioni in questi driver per accedere ai dati in modo indipendente dal sistema DBMS. Gestione driver gestisce la comunicazione tra le applicazioni e i driver.  
  
 Sebbene Microsoft fornisca una gestione driver per i computer che eseguono Microsoft Windows® 95 e versioni successive, ha scritto diversi driver ODBC e chiama funzioni ODBC da alcune applicazioni, chiunque può scrivere applicazioni e driver ODBC. Infatti, la maggior parte delle applicazioni e dei driver ODBC attualmente disponibili sono scritti da società diverse da Microsoft. Inoltre, i driver e le applicazioni ODBC sono disponibili nel® di Macintosh e in un'ampia gamma di piattaforme UNIX.  
  
 Per aiutare gli sviluppatori di applicazioni e driver, Microsoft offre un SDK (Software Development Kit) ODBC per computer che eseguono Windows 95 e versioni successive che fornisce gestione driver, DLL del programma di installazione, strumenti di test e applicazioni di esempio. Microsoft ha collaborato con il software Visigenic per trasferire questi SDK a Macintosh e a un'ampia gamma di piattaforme UNIX.  
  
 È importante comprendere che ODBC è progettato per esporre le funzionalità del database, non per integrarle. Pertanto, i writer di applicazioni non dovrebbero prevedere che l'utilizzo di ODBC trasforma improvvisamente un semplice database in un motore di database relazionale con funzionalità complete. Non è previsto che i writer di driver implementino la funzionalità non trovata nel database sottostante. Un'eccezione è che gli sviluppatori che scrivono i driver che accedono direttamente ai dati dei file, ad esempio i dati in un file Xbase, sono necessari per scrivere un motore di database che supporta almeno una funzionalità SQL minima. Un'altra eccezione è che il componente ODBC del Windows SDK, incluso in precedenza nell'SDK di Microsoft Data Access Components (MDAC), fornisce una libreria di cursori che simula i cursori scorrevoli per i driver che implementano un determinato livello di funzionalità.  
  
 Le applicazioni che utilizzano ODBC sono responsabili di qualsiasi funzionalità tra database. ODBC, ad esempio, non è un motore di join eterogeneo né un processore di transazioni distribuito. Tuttavia, poiché è indipendente dal sistema DBMS, può essere utilizzato per compilare questi strumenti tra database.
