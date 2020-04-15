---
title: Programmatori ODBC&#39;s Riferimento Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6a9ca32627b9703465dcfca554fdc32ae01442e7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280511"
---
# <a name="odbc-programmer39s-reference"></a>Guida di riferimento a programmator&#39;i ODBC
*Il riferimento per programmatori ODBC* contiene le sezioni seguenti.  
  
-   [Novità di ODBC 3.8](../../odbc/reference/what-s-new-in-odbc-3-8.md) sono elencate le nuove funzionalità ODBC aggiunte in Windows 8 SDK.  
  
-   [Programma ODBC di esempio](../../odbc/reference/sample-odbc-program.md) presenta un programma ODBC di esempio.  
  
-   [Introduzione a ODBC](../../odbc/reference/introduction-to-odbc.md) fornisce una breve cronologia di Structured Query Language e ODBC e informazioni concettuali sull'interfaccia ODBC.  
  
-   [Lo sviluppo di applicazioni](../../odbc/reference/develop-app/developing-applications.md) contiene informazioni sullo sviluppo di applicazioni che utilizzano l'interfaccia ODBC e i driver che la implementano.  
  
-   [L'installazione e la configurazione del software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) forniscono informazioni sull'installazione e un riferimento alle funzioni DLL di installazione.  
  
-   [Lo sviluppo di un driver ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contiene informazioni sulla scrittura di un driver.  
  
-   [Riferimento API](../../odbc/reference/syntax/odbc-reference.md) contiene informazioni sulla sintassi e sulla semantica per tutte le funzioni ODBC.  
  
-   [Le appendici ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) contengono dettagli tecnici e tabelle di riferimento per codici di errore ODBC, tipi di dati e grammatica SQL.  
  
## <a name="working-with-the-odbc-documentation"></a>Utilizzo della documentazione ODBC  
 L'interfaccia ODBC è progettata per essere usata con il linguaggio di programmazione C. L'uso dell'interfaccia ODBC si estende su tre aree: istruzioni SQL, chiamate di funzione ODBC e programmazione C. In questa documentazione si presuppone quanto segue:This documentation assumes the following:  
  
-   Una conoscenza di lavoro del linguaggio di programmazione C.  
  
-   Conoscenza generale del DBMS e familiarità con SQL.  
  
 Vengono utilizzate le seguenti convenzioni tipografiche.  
  
|Format|Utilizzo|  
|------------|--------------|  
|SELEZIONARE DA|Le lettere maiuscole indicano istruzioni SQL, nomi di macro e termini utilizzati a livello di comando del sistema operativo.|  
|`RETCODE SQLFetch(hdbc)`|Il tipo di carattere monospazio viene utilizzato per le righe di comando di esempio e il codice del programma.|  
|*argument*|Le parole in corsivo indicano argomenti a livello di codice, informazioni che l'utente o l'applicazione deve fornire o enfasi di parola.|  
|**SQLEndTran**|Il grassetto indica che la sintassi deve essere digitata esattamente come illustrato, inclusi i nomi delle funzioni.|  
|&#124;|Una barra verticale separa due scelte che si escludono a vicenda in una riga di sintassi.|  
|...|I ellissi indicano che gli argomenti possono essere ripetuti più volte.|  
|. . .|Una colonna di tre punti indica la continuazione delle righe di codice precedenti.|  
  
## <a name="about-the-code-examples"></a>Informazioni sugli esempi di codice  
 Gli esempi di codice in questa guida sono progettati solo a scopo illustrativo. Poiché sono scritti principalmente per dimostrare i principi ODBC, l'efficienza è stata talvolta messa da parte nell'interesse della chiarezza. Inoltre, intere sezioni di codice sono state talvolta omesse per chiarezza. Questi includono le definizioni di funzioni non ODBC (quelle funzioni i cui nomi non iniziano con "SQL") e la maggior parte della gestione degli errori.  
  
 In tutti gli esempi di codice vengono utilizzate stringhe ANSI e lo stesso schema di database, illustrato all'inizio di [Funzioni di](../../odbc/reference/develop-app/catalog-functions.md)catalogo.  
  
## <a name="recommended-reading"></a>Argomenti consigliati  
 Per ulteriori informazioni su SQL, sono disponibili i seguenti standard:  
  
-   Linguaggio di database - SQL con miglioramento dell'integrità, ANSI, 1989 ANSI X3.135-1989.  
  
-   Linguaggio database - SQL: ANSI X3H2 e ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Apri gruppo, gestione dei dati: SQL (Structured Query Language), versione 2 (Gruppo aperto, 1996).  
  
 Oltre agli standard e alle guide SQL specifiche del fornitore, molti libri descrivono SQL, tra cui:In addition to standards and vendor-specific SQL guides, many books describe SQL, including:  
  
-   Data, C. J., con Darwen, Hugh: *A Guide to the SQL Standard* (Addison-Wesley, 1993).  
  
-   Emerson, Sandra L., Darnovsky, Marcy e Bowman, Judith S.: *The Practical SQL Handbook* (Addison-Wesley, 1989).  
  
-   Groff, James R. e Weinberg, Paul N.: *Using SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *Comprendere SQL* (Sybex, 1990).  
  
-   Hursch, Jack L. e Carolyn J.: *SQL, The Structured Query Language* (TAB Books, 1988).  
  
-   Melton, Jim e Simon, Alan R.: *Comprendere il nuovo SQL: una guida completa* (Morgan Kaufmann Publishers, 1993).  
  
-   Pascal, Fabian: *Sql e Nozioni di base relazionali* (M & T Books, 1990).  
  
-   Trimble, J. Harvey Jr. e Chappell, David: *A Visual Introduction to SQL* (Wiley, 1989).  
  
-   Van der Lans, Rick F.: *Introduzione a SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL e database relazionali* (Microtrend Books, 1990).  
  
-   Viescas, John: *Guida di riferimento rapido a SQL* (Microsoft Corp., 1989).  
  
 Per ulteriori informazioni sull'elaborazione delle transazioni, vedere:For additional information about transaction processing, see:  
  
-   Grigio, J. N. e Reuter, Andreas: *Transaction Processing: Concepts and Techniques* (Morgan Kaufmann Publishers, 1993).  
  
-   Hackathorn, Richard D.: *Enterprise Database Connectivity* (Wiley & Sons, 1993).  
  
 Per ulteriori informazioni sulle interfacce a livello di chiamata, sono disponibili i seguenti standard:  
  
-   Apri gruppo, Gestione dati: interfaccia a livello di *chiamata SQL (CLI), C451* (Open Group, 1995).  
  
-   ISO/IEC 9075-3:1995, interfaccia a livello di chiamata (SQL/CLI).  
  
 Per ulteriori informazioni su ODBC, sono disponibili numerosi libri, tra cui:  
  
-   Geiger, Kyle: *All'interno di ODBC* (Microsoft Press® 1995).  
  
-   Gryphon, Robert, Charpentier, Luc, Oelschlager, Jon, Shoemaker, Andrew, Cross, Jim e Lilley, Albert W.: *Using ODBC 2* (Que, 1994).  
  
-   Johnston, Tom e Osborne, Mark: *ODBC Developers Guide* (Howard W. Sams & Company, 1994).  
  
-   Nord, Ken: *Programmazione di Windows Multi-DBMS: utilizzo di C, Visual Basic, ODBC, OLE 2 e strumenti per* i progetti DBMS (John Wiley & Sons, Inc., 1995).  
  
-   Stegman, Michael O., Signore, Robert e Creamer, John: *The ODBC Solution, Open Database Connectivity in Distributed Environments* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *Utilizzo di ODBC 2* (Que, 1994).  
  
-   Whiting, Bill: *Teach Yourself ODBC in Twenty-One Days* (Howard W. Sams & Company, 1994).
