---
title: ODBC e l'interfaccia della riga di comando standard | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305142"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC e l'interfaccia della riga di comando standard
ODBC è allineato alle specifiche e agli standard seguenti che gestiscono l'interfaccia della riga di comando (CLI). Le funzionalità ODBC sono un superset di ognuno di questi standard.  
  
-   La specifica CAE del gruppo Open "Gestione dati: interfaccia della riga di comando di SQL (CLI)"  
  
-   Interfaccia a livello di chiamata ISO/IEC 9075-3:1995 (E) (SQL/CLI)  
  
 In seguito a questo allineamento, si verifica quanto segue:  
  
-   Un'applicazione scritta nelle specifiche dell'interfaccia della riga di comando ISO e del gruppo aperto funzionerà con un driver ODBC *3. x* o un driver conforme agli standard quando viene compilato con i file di intestazione ODBC *3. x* e collegato alle librerie ODBC 3 *.* x e quando ottiene l'accesso al driver tramite Gestione driver ODBC *3. x* .  
  
-   Un driver scritto nelle specifiche dell'interfaccia della riga di comando ISO e del gruppo aperto funzionerà con un'applicazione ODBC *3. x* o un'applicazione conforme agli standard quando viene compilata con i file di intestazione ODBC *3. x* e collegata alle librerie ODBC *3.* x e quando l'applicazione ottiene l'accesso al driver tramite Gestione driver ODBC *3. x* . Per ulteriori informazioni, vedere [applicazioni e driver conformi agli standard](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 Il livello di conformità dell'interfaccia di base comprende tutte le funzionalità nell'interfaccia della riga di comando ISO e tutte le funzionalità non facoltative nell'interfaccia della riga di comando del gruppo aperto. Le funzionalità facoltative dell'interfaccia della riga di comando di gruppo aperto vengono visualizzate nei livelli di conformità dell'interfaccia più elevati. Poiché tutti i driver ODBC *3. x* sono necessari per supportare le funzionalità del livello di conformità dell'interfaccia principale, sono soddisfatte le condizioni seguenti:  
  
-   Un driver ODBC *3. x* supporterà tutte le funzionalità usate da un'applicazione conforme agli standard.  
  
-   Un'applicazione ODBC *3. x* che usa solo le funzionalità dell'interfaccia della riga di comando ISO e le funzionalità non facoltative dell'interfaccia della riga di comando di gruppo aperto funzioneranno con qualsiasi driver conforme agli standard.  
  
 Oltre alle specifiche dell'interfaccia a livello di chiamata contenute negli standard dell'interfaccia della riga di comando ISO/IEC e Open Group, ODBC implementa le funzionalità seguenti. (Alcune di queste funzionalità erano disponibili nelle versioni di ODBC precedenti a ODBC *3. x*).  
  
-   Più righe recupera da una singola chiamata di funzione  
  
-   Associazione a una matrice di parametri  
  
-   Supporto dei segnalibri, incluso il recupero da segnalibro, segnalibri a lunghezza variabile e l'aggiornamento e l'eliminazione bulk tramite operazioni segnalibro su righe non contigue  
  
-   Associazione per riga  
  
-   Offset di binding  
  
-   Supporto per batch di istruzioni SQL, in una stored procedure o come sequenza di istruzioni SQL eseguite tramite **SQLExecute** o **SQLExecDirect**  
  
-   Conteggio delle righe di cursore esatte o approssimative  
  
-   Operazioni di aggiornamento ed eliminazione posizionate e aggiornamenti in batch ed eliminazioni per chiamata di funzione (**SQLSetPos**)  
  
-   Funzioni di catalogo che estraggono informazioni dallo schema informativo senza la necessità di supportare le viste degli schemi delle informazioni  
  
-   Sequenze di escape per outer join, funzioni scalari, valori letterali datetime, valori letterali intervallo e stored procedure  
  
-   Librerie di conversione di pagine di codice  
  
-   Segnalazione del livello di conformità ANSI di un driver e del supporto SQL  
  
-   Popolamento automatico su richiesta del descrittore del parametro di implementazione  
  
-   Diagnostica avanzata e matrici di stato di righe e parametri  
  
-   Tipi di buffer di applicazione DateTime, Interval, numeric/Decimal e a 64 bit  
  
-   Esecuzione asincrona  
  
-   Supporto delle stored procedure, incluse sequenze di escape, meccanismi di associazione di parametri di output e funzioni di catalogo  
  
-   Miglioramenti della connessione, incluso il supporto per gli attributi di connessione e l'esplorazione degli attributi
