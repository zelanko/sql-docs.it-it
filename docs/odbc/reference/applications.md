---
title: Proprietà Applications . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- off-the-shelf applications [ODBC]
- ODBC architecture [ODBC], applications
- shrink-wrapped applications [ODBC]
- application development [ODBC], types
- custom applications [ODBC]
- virtual applications [ODBC]
- generic applications [ODBC]
ms.assetid: 39d6461f-0d24-4b7d-a723-843ade15ad73
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9184986883f64bd082ca1db472d887609d3071bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306552"
---
# <a name="applications"></a>APPLICAZIONI
*Un'applicazione* è un programma che chiama l'API ODBC per accedere ai dati. Anche se molti tipi di applicazioni sono possibili, la maggior parte rientrano in tre categorie, che vengono utilizzate come esempi in tutta questa guida.  
  
-   **Applicazioni generiche** Queste sono anche chiamate applicazioni shrink-wrapped o applicazioni pronte all'uso. Le applicazioni generiche sono progettate per funzionare con una varietà di DBS diversi. Gli esempi includono un foglio di calcolo o un pacchetto di statistiche che utilizza ODBC per importare i dati per un'ulteriore analisi e un elaboratore di testi che utilizza ODBC per ottenere una lista di distribuzione da un database.  
  
     Un'importante sottocategoria di applicazioni generiche sono gli ambienti di sviluppo di applicazioni, ad esempio PowerBuilder o Microsoft® Visual Basic®. Anche se le applicazioni costruite con questi ambienti probabilmente funzioneranno solo con un singolo DBMS, l'ambiente stesso deve funzionare con più DBMS.  
  
     Ciò che tutte le applicazioni generiche hanno in comune è che sono altamente interoperabili tra DBS e devono utilizzare ODBC in modo relativamente generico. Per ulteriori informazioni sull'interoperabilità, vedere [Scelta di un livello di interoperabilità](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Applicazioni verticali** Le applicazioni verticali eseguono un singolo tipo di attività, ad esempio l'immissione di ordini o il rilevamento dei dati di produzione, e utilizzano uno schema di database controllato dallo sviluppatore dell'applicazione. Per un particolare cliente, l'applicazione funziona con un singolo DBMS. Ad esempio, una piccola azienda potrebbe utilizzare l'applicazione con dBase, mentre una grande azienda potrebbe usarla con Oracle.For example, a small business might use the application with dBase, while a large business might use it with Oracle.  
  
     L'applicazione utilizza ODBC in modo tale che l'applicazione non è legata a qualsiasi DBMS, anche se potrebbe essere legata a un numero limitato di DBMS che forniscono funzionalità simili. Pertanto, lo sviluppatore dell'applicazione può vendere l'applicazione indipendentemente dal DBMS. Le applicazioni verticali sono interoperabili quando vengono sviluppate, ma talvolta vengono modificate per includere codice non interoperabile dopo che il cliente ha scelto un DBMS.  
  
-   **Applicazioni personalizzate** Le applicazioni personalizzate vengono utilizzate per eseguire un'attività specifica in una singola società. Ad esempio, un'applicazione in una società di grandi dimensioni potrebbe raccogliere dati di vendita da diverse divisioni (ognuna delle quali utilizza un DBMS diverso) e creare un singolo report. ODBC viene utilizzato perché è un'interfaccia comune e salva i programmatori di dover imparare più interfacce. Tali applicazioni non sono generalmente interoperabili e sono scritte su DBS e driver specifici.  
  
 Un certo numero di attività sono comuni a tutte le applicazioni, indipendentemente da come utilizzano ODBC. Nel loro insieme, definiscono in gran parte il flusso di qualsiasi applicazione ODBC. I compiti sono:  
  
-   Selezione di un'origine dati e connessione ad essa.  
  
-   Invio di un'istruzione SQL per l'esecuzione.  
  
-   Recupero dei risultati (se presenti).  
  
-   Errori di elaborazione.  
  
-   Eseguire il commit o il rollback della transazione che racchiude l'istruzione SQL.  
  
-   Disconnessione dall'origine dati.  
  
 Poiché la maggior parte delle operazioni di accesso ai dati viene eseguita con SQL, l'attività principale per cui le applicazioni utilizzano ODBC consiste nell'inviare istruzioni SQL e recuperare i risultati (se presenti) generati da tali istruzioni. Altre attività per le quali le applicazioni utilizzano ODBC includono la determinazione e la regolazione delle funzionalità dei driver e l'esplorazione del catalogo del database.
