---
title: ODBC e l'interfaccia della riga di comando standard Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56dc0ac73c77cbbb77943d2e9ba308796b259dbb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305142"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC e l'interfaccia della riga di comando standard
ODBC è allineato con le seguenti specifiche e standard che gestiscono l'interfaccia a livello di chiamata (CLI). (Le funzionalità ODBC sono un superset di ciascuno di questi standard.)  
  
-   La specifica Open Group CAE "Data Management: SQL Call-Level Interface (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) Interfaccia a livello di chiamata (SQL/CLI)  
  
 Come risultato di questo allineamento, sono vere le seguenti condizioni:  
  
-   Un'applicazione scritta nelle specifiche Open Group e ISO CLI funzionerà con un driver ODBC *3.x* o un driver conforme agli standard quando viene compilata con i file di intestazione ODBC *3.x* e collegata alle librerie ODBC *3.x* e quando ottiene l'accesso al driver tramite Gestione driver ODBC *3.x.*  
  
-   Un driver scritto nelle specifiche Open Group e ISO CLI funzionerà con un'applicazione ODBC *3.x* o un'applicazione conforme agli standard quando viene compilata con i file di intestazione ODBC *3.x* e collegata alle librerie ODBC *3.x* e quando l'applicazione ottiene l'accesso al driver tramite Gestione driver ODBC *3.x.* Per ulteriori informazioni, vedere [Applicazioni e driver conformi agli standard](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 Il livello di conformità dell'interfaccia principale comprende tutte le funzionalità dell'interfaccia CLI ISO e tutte le funzionalità non facoltative dell'interfaccia della riga di comando Open Group. Le funzionalità facoltative dell'interfaccia della riga di comando Apri gruppo vengono visualizzate nei livelli di conformità dell'interfaccia più elevati. Poiché tutti i driver ODBC *3.x* sono necessari per supportare le funzionalità del livello di conformità dell'interfaccia Core, sono vere le seguenti condizioni:  
  
-   Un driver ODBC *3.x* supporterà tutte le funzionalità utilizzate da un'applicazione conforme agli standard.  
  
-   Un'applicazione ODBC *3.x* che utilizza solo le funzionalità dell'interfaccia della riga di comando ISO e le funzionalità non facoltative dell'interfaccia della riga di comando Open Group funzionerà con qualsiasi driver conforme agli standard.  
  
 Oltre alle specifiche dell'interfaccia a livello di chiamata contenute negli standard ISO/IEC e Open Group CLI, ODBC implementa le funzionalità seguenti. (Alcune di queste funzionalità esistevano nelle versioni di ODBC precedenti a ODBC *3.x*.)  
  
-   Recuperi multiriga da una singola chiamata di funzioneMultirow fetches by a single function call  
  
-   Associazione a una matrice di parametriBinding to an array of parameters  
  
-   Supporto dei segnalibri, incluso il recupero tramite segnalibro, i segnalibri a lunghezza variabile e l'aggiornamento e l'eliminazione in blocco tramite operazioni sui segnalibri su righe non contigue  
  
-   Associazione per riga  
  
-   Offset di rilegatura  
  
-   Supporto per batch di istruzioni SQL, in una stored procedure o come sequenza di istruzioni SQL eseguite tramite SQLExecute o **SQLExecDirectSupport** for batches of SQL statements, either in a stored procedure or as a sequence of SQL statements executed through **SQLExecute** or SQLExecDirect  
  
-   Conteggi di righe esatte o approssimative del cursore  
  
-   Operazioni di aggiornamento ed eliminazione posizionate e aggiornamenti ed eliminazioni in batch per chiamata di funzione (**SQLSetPos**)  
  
-   Funzioni di catalogo che estraggono informazioni dallo schema delle informazioni senza la necessità di supportare le visualizzazioni dello schema delle informazioni  
  
-   Sequenze di escape per outer join, funzioni scalari, valori letterali datetime, valori letterali di intervallo e stored procedure  
  
-   Librerie di traduzione della tabella codici  
  
-   Segnalazione del livello di conformità ANSI e del supporto SQL di un driver  
  
-   Popolazione automatica su richiesta del descrittore del parametro di implementazione  
  
-   Matrice avanzata di diagnostica e stato di riga e parametri  
  
-   Tipi di buffer dell'applicazione integer datetime, interval, numerico/decimal e a 64 bit  
  
-   Esecuzione asincrona  
  
-   Supporto delle stored procedure, incluse sequenze di escape, meccanismi di associazione dei parametri di output e funzioni di catalogoStored procedure support, including escape sequences, output parameter binding mechanisms, and catalog functions  
  
-   Miglioramenti della connessione, incluso il supporto per gli attributi di connessione e l'esplorazione degli attributiConnection enhancements including support for connection attributes and attribute browsing
