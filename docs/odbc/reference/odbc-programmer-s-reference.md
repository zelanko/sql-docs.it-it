---
title: Informazioni di riferimento su ODBC Programmer&#39;s | Microsoft Docs
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
ms.openlocfilehash: fd729956ee7bb1fccf7a8fceb7a435042df4df7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68111187"
---
# <a name="odbc-programmer39s-reference"></a>Informazioni di riferimento su ODBC Programmer&#39;s
Il *riferimento per programmatori ODBC* contiene le sezioni seguenti.  
  
-   Novità [di odbc 3,8](../../odbc/reference/what-s-new-in-odbc-3-8.md) sono elencate le nuove funzionalità ODBC aggiunte in Windows 8 SDK.  
  
-   Il [programma ODBC di esempio](../../odbc/reference/sample-odbc-program.md) presenta un programma ODBC di esempio.  
  
-   [Introduzione a ODBC](../../odbc/reference/introduction-to-odbc.md) fornisce una breve cronologia di Structured Query Language e ODBC e informazioni concettuali sull'interfaccia ODBC.  
  
-   [Lo sviluppo di applicazioni](../../odbc/reference/develop-app/developing-applications.md) contiene informazioni sullo sviluppo di applicazioni che utilizzano l'interfaccia ODBC e i driver che la implementano.  
  
-   [L'installazione e la configurazione del software ODBC](../../odbc/reference/install/installing-and-configuring-the-odbc-software.md) fornisce informazioni sull'installazione e un riferimento alle funzioni DLL di installazione.  
  
-   [Lo sviluppo di un driver ODBC](../../odbc/reference/develop-driver/developing-an-odbc-driver.md) contiene informazioni sulla scrittura di un driver.  
  
-   [Riferimento API](../../odbc/reference/syntax/odbc-reference.md) contiene informazioni sulla sintassi e sulla semantica per tutte le funzioni ODBC.  
  
-   Nelle [appendici ODBC](../../odbc/reference/appendixes/odbc-appendixes.md) sono contenuti i dettagli tecnici e le tabelle di riferimento per i codici di errore ODBC, i tipi di dati e la grammatica SQL.  
  
## <a name="working-with-the-odbc-documentation"></a>Utilizzo della documentazione ODBC  
 L'interfaccia ODBC è progettata per essere utilizzata con il linguaggio di programmazione C. L'utilizzo dell'interfaccia ODBC si estende in tre aree: istruzioni SQL, chiamate di funzioni ODBC e programmazione C. In questa documentazione si presuppone quanto segue:  
  
-   Conoscenza operativa del linguaggio di programmazione C.  
  
-   Conoscenza generale del sistema DBMS e una certa familiarità con SQL.  
  
 Vengono utilizzate le convenzioni tipografiche seguenti.  
  
|Format|Utilizzo|  
|------------|--------------|  
|SELEZIONARE * DA|Le lettere maiuscole indicano istruzioni SQL, nomi di macro e termini utilizzati a livello di comando del sistema operativo.|  
|`RETCODE SQLFetch(hdbc)`|Il tipo di carattere spazio vuoto viene usato per le righe di comando di esempio e il codice programma.|  
|*argomento*|Le parole in corsivo indicano gli argomenti programmatici, le informazioni che l'utente o l'applicazione deve fornire o la parola enfasi.|  
|**SQLEndTran**|Il tipo grassetto indica che la sintassi deve essere digitata esattamente come illustrato, inclusi i nomi di funzione.|  
|&#124;|Una barra verticale separa due scelte che si escludono a vicenda in una riga della sintassi.|  
|...|I puntini di sospensione indicano che gli argomenti possono essere ripetuti più volte.|  
|. . .|Una colonna di tre punti indica la continuazione delle righe di codice precedenti.|  
  
## <a name="about-the-code-examples"></a>Informazioni sugli esempi di codice  
 Gli esempi di codice in questa guida sono progettati solo a scopo illustrativo. Poiché vengono scritti principalmente per illustrare i principi ODBC, l'efficienza è stata talvolta accantonata per maggiore chiarezza. Inoltre, le sezioni intere del codice sono talvolta state omesse per maggiore chiarezza. Sono incluse le definizioni delle funzioni non ODBC (le funzioni i cui nomi non iniziano con "SQL") e la maggior parte della gestione degli errori.  
  
 In tutti gli esempi di codice vengono utilizzate stringhe ANSI e lo stesso schema di database, che viene visualizzato all'inizio delle [funzioni di catalogo](../../odbc/reference/develop-app/catalog-functions.md).  
  
## <a name="recommended-reading"></a>Argomenti consigliati  
 Per ulteriori informazioni su SQL, sono disponibili gli standard seguenti:  
  
-   Lingua del database: SQL con miglioramento dell'integrità, ANSI, 1989 ANSI X 3.135-1989.  
  
-   Lingua del database-SQL: ANSI X3H2 e ISO/IEC JTC1/SC21/WG3 9075:1992 (SQL-92).  
  
-   Aprire il gruppo Gestione dati: Structured Query Language (SQL), versione 2 (il gruppo aperto, 1996).  
  
 Oltre agli standard e alle guide SQL specifiche del fornitore, molti libri descrivono SQL, tra cui:  
  
-   Data, C. J., con Darwen, Hugh: *una guida per lo standard SQL* (Addison-Wesley, 1993).  
  
-   Emerson, Sandra L., Darnovsky, Marcy e Bowman, Judith S.: *il manuale pratico di SQL* (Addison-Wesley, 1989).  
  
-   Groff, James R. e Weinberg, Paul N.: *uso di SQL* (Osborne McGraw-Hill, 1990).  
  
-   Gruber, Martin: *informazioni su SQL* (Sybex, 1990).  
  
-   Hursch, Jack L. e Carolyn J.: *SQL, il Structured Query Language* (schede, 1988).  
  
-   Melton, Jim e Simon, Alan R.: *Understanding the New SQL: A complete guide* (Morgan Kaufmann publishers, 1993).  
  
-   Pascal, Fabian: *SQL e le nozioni di base relazionali* (M & T Books, 1990).  
  
-   Trimble, J. Harvey, Jr. e Cuccu, David: *a Visual Introduction to SQL* (Wiley, 1989).  
  
-   Van der Lans, Rick F.: *Introduzione a SQL* (Addison-Wesley, 1988).  
  
-   Vang, Soren: *SQL e database relazionali* (libri di microtendenza, 1990).  
  
-   Viescas, John: *Guida di riferimento rapido a SQL* (Microsoft Corp., 1989).  
  
 Per ulteriori informazioni sull'elaborazione delle transazioni, vedere:  
  
-   Grigio, J. N. e Reuter, Andreas: *Transaction Processing: Concepts and Techniques* (Morgan Kaufmann publishers, 1993).  
  
-   Hackathorn, Richard D.: *Enterprise Database Connectivity* (Wiley & Sons, 1993).  
  
 Per ulteriori informazioni sulle interfacce a livello di chiamata, sono disponibili gli standard seguenti:  
  
-   Aprire il gruppo *Gestione dati: interfaccia della riga di comando di SQL (CLI), C451* (open group, 1995).  
  
-   ISO/IEC 9075-3:1995, interfaccia a livello di chiamata (SQL/CLI).  
  
 Per ulteriori informazioni su ODBC, sono disponibili diversi libri, tra cui:  
  
-   Geiger, Kyle: *all'interno di ODBC* (Microsoft Press®, 1995).  
  
-   Grifone, Robert, Charpentier, Luc, Oelschlager, Jon, calzolaio, Andrew, Cross, Jim e Lilley, Albert W.: *uso di ODBC 2* (Que, 1994).  
  
-   Johnston, Tom e Osborne, Mark: *Guida per sviluppatori ODBC* (Howard W. Sams & Company, 1994).  
  
-   Nord, Ken: *programmazione Windows a più DBMS: uso di C++, Visual Basic, ODBC, OLE 2 e strumenti per i progetti DBMS* (John Wiley & Sons, Inc., 1995).  
  
-   Steger, Michael O., Signore, Robert e Creamer, John: *la soluzione ODBC Open Database Connectivity in ambienti distribuiti* (McGraw-Hill, 1995).  
  
-   Welch, Keith: *con ODBC 2* (Que, 1994).  
  
-   Whiting, fattura: *Teach Yourself ODBC in venti giorni* (Howard W. Sams & Company, 1994).
