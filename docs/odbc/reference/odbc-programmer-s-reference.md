---
title: I programmatori ODBC&#39;riferimento s | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], reference
ms.assetid: b33c3c43-ae66-44a3-be17-9cd82624dd96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c83a7de609d200da2957a65b9325d031eda49780
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63273035"
---
# <a name="odbc-programmer39s-reference"></a>I programmatori ODBC&#39;riferimento
Il *riferimento per programmatori ODBC* contiene le sezioni seguenti.  
  
-   [What ' s New in ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) Elenca le nuove funzionalità ODBC che sono state aggiunte in Windows 8 SDK.  
  
-   [ODBC programma di esempio](../../odbc/reference/sample-odbc-program.md) presenta un programma di esempio ODBC.  
  
-   [Introduzione a ODBC](../../odbc/reference/introduction-to-odbc.md) fornisce una breve storia di Structured Query Language e ODBC e informazioni concettuali sull'interfaccia ODBC.  
  
-   [Lo sviluppo di applicazioni](../../odbc/reference/develop-app/developing-applications.md) contiene informazioni sullo sviluppo di applicazioni che usano l'interfaccia ODBC e driver che l'implementano.  
  
-   [Installazione e configurazione Software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) fornisce informazioni su una riferimento a una funzione DLL di installazione e configurazione.  
  
-   [Sviluppo di un Driver ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contiene informazioni sulla scrittura di un driver.  
  
-   [Riferimento all'API](../../odbc/reference/syntax/odbc-reference.md) contiene informazioni semantiche per tutte le funzioni ODBC e sintassi.  
  
-   [Appendici ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contengono dettagli tecnici e fanno riferimento a tabelle di codici di errore ODBC, i tipi di dati e la grammatica SQL.  
  
## <a name="working-with-the-odbc-documentation"></a>Utilizzo con la documentazione di ODBC  
 L'interfaccia ODBC è progettato per l'uso con il linguaggio di programmazione C. Uso dell'interfaccia ODBC si estende su tre aree: Le istruzioni SQL, chiamate di funzione ODBC e programmazione C. Questa documentazione si presuppone quanto segue:  
  
-   Una conoscenza del linguaggio di programmazione C.  
  
-   Una conoscenza generale DBMS e una certa familiarità con SQL.  
  
 Le convenzioni tipografiche seguenti vengono usate.  
  
|Formato|Utilizzo|  
|------------|--------------|  
|SELECT * FROM|Lettere maiuscole indicano le istruzioni SQL, i nomi delle macro e termini utilizzati a livello di comando del sistema operativo.|  
|`RETCODE SQLFetch(hdbc)`|Il tipo di carattere a spaziatura fissa viene usato per righe di comando di esempio e il codice del programma.|  
|*argument*|Le parole in corsivo indicano argomenti a livello di codice, informazioni che l'utente o l'applicazione deve fornire o enfasi di word.|  
|**SQLEndTran**|In grassetto di sintassi deve essere digitata esattamente come indicato, inclusi i nomi delle funzioni.|  
|&#124;|Una barra verticale separa le due opzioni si escludono a vicenda in una riga di sintassi.|  
|...|I puntini di sospensione indica che gli argomenti possono essere ripetuti più volte.|  
|. . .|Una colonna di tre punti indica mantenimento delle righe di codice precedenti.|  
  
## <a name="about-the-code-examples"></a>Informazioni sugli esempi di codice  
 Gli esempi di codice in questa guida sono destinati solo a scopo illustrativo. Poiché vengono scritti principalmente per dimostrare i principi ODBC, l'efficienza è talvolta stato riservato a fini di chiarezza. Inoltre, intere sezioni di codice in alcuni casi sono stati omessi per maggiore chiarezza. Queste includono le definizioni di funzioni non ODBC (tali funzioni i cui nomi non iniziano con "SQL") e la maggior parte degli errori.  
  
 Tutti gli esempi di codice usano le stringhe ANSI e lo stesso schema di database, viene visualizzato all'inizio di [funzioni di catalogo](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Argomenti consigliati  
 Per altre informazioni su SQL, sono disponibili i seguenti standard:  
  
-   Database SQL con l'integrità miglioramento, ANSI, ANSI 1989 X3.135-1989 - Language.  
  
-   Linguaggio di database - SQL: ANSI X3H2 and ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Open Group, la gestione dei dati: Structured Query Language (SQL), versione 2 (The Open Group, 1996).  
  
 Oltre a standard e le guide di SQL specifico del fornitore, molti libri descrivono SQL, tra cui:  
  
-   Data, J. C., con Darwen, Hugh: *Una Guida allo Standard SQL* (Addison-Wesley, 1993).  
  
-   Emerson, Sandra l, Darnovsky, Maria e Bowman, S. Judith: *Il manuale di SQL pratico* (Addison-Wesley, 1989).  
  
-   Groff, James R. and Weinberg, Paul N.: *Using SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *La comprensione di SQL* (Sybex, 1990).  
  
-   Hursch, Jack "l". e J. Carolyn: *SQL, linguaggio di Query strutturate* (scheda documentazione, 1988).  
  
-   Melton, Jim, and Simon, Alan R.: *Informazioni sulle nuove SQL: A Complete Guide* (Morgan Kaufmann Publishers, 1993).  
  
-   Convenzione Pascal, Fabian: *SQL e relazionali nozioni di base* (M & T libri, 1990).  
  
-   Trimble, J. Harvey, Jr e Chappell, David: *Un'introduzione visiva al SQL* (Wiley, 1989).  
  
-   Van der reti LAN, Rick F.: *Introduzione a SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL e database relazionali* (Microtrend libri, 1990).  
  
-   Viescas, John: *Guida di riferimento rapido SQL* (Microsoft Corp., 1989).  
  
 Per ulteriori informazioni sull'elaborazione delle transazioni, vedere:  
  
-   Gray, J. N. e Reuter, Andreas: *Elaborazione delle transazioni: Concetti e tecniche* (Morgan Kaufmann editori, 1993).  
  
-   Hackathorn, Richard D.: *Connettività al Database Enterprise* (Wiley & Sons, 1993).  
  
 Per altre informazioni sulle interfacce a livello di chiamata, sono disponibili i seguenti standard:  
  
-   Open Group *gestione dati: Chiamata a livello interfaccia SQL (CLI), C451* (Open Group 1995).  
  
-   ISO/IEC 9075-3:1995, interfaccia a livello di chiamata (SQL/CLI).  
  
 Per altre informazioni su ODBC, una serie di libri disponibili, tra cui:  
  
-   Geiger, Kyle: *All'interno di ODBC* (Microsoft Press®, 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, ortopedico, Andrew, croce, Jim e Lilley, W. Albert: *Utilizzo di ODBC 2* (Que, 1994).  
  
-   Johnston, Tom e Osborne, contrassegnare: *Guida per gli sviluppatori ODBC* (Howard W. Sams & aziendale, 1994).  
  
-   Centro-settentrionali, Davide: *Programmazione di Multi-DBMS Windows: Usa C++, Visual Basic, ODBC, OLE 2 e strumenti per i progetti DBMS* (Wiley John & Sons, Inc., 1995).  
  
-   Stegman, Michael O., Signore, Robert e Creamer, John: *La soluzione ODBC, Open Database Connectivity in ambienti distribuiti* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *Utilizzo di ODBC 2* (Que, 1994).  
  
-   Merlano, fattura: *Impara da solo ODBC in 21 giorni* (Howard W. Sams & aziendale, 1994).
