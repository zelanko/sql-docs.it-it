---
title: Le applicazioni | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dc655740701822d8c6ff9595327b906ee9a67026
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62734997"
---
# <a name="applications"></a>Applicazioni
Un' *applicazione* è un programma che chiama l'API ODBC per accedere ai dati. Anche se sono possibili molti tipi di applicazioni, la maggior parte rientrano in tre categorie, che vengono usate come esempi in questa Guida.  
  
-   **Applicazioni generiche** questi sono anche denominati per le applicazioni già pronti o disponibili sul mercato. Applicazioni generiche sono progettate per funzionare con un'ampia gamma di DBMS diverso. Ad esempio un foglio di calcolo o pacchetto di statistiche che usa ODBC per importare i dati per un'ulteriore analisi e un elaboratore di testo che usa ODBC per ottenere una lista di distribuzione da un database.  
  
     Un'importante sottocategoria di applicazioni generiche è ambienti di sviluppo dell'applicazione, ad esempio PowerBuilder o Microsoft® Visual Basic®. Anche se le applicazioni costruite con questi ambienti probabilmente funzionerà solo con un singolo DBMS, l'ambiente deve essere utilizzato con più DBMS.  
  
     Ciò che tutte le applicazioni generiche hanno in comune è che sono estremamente interoperativi tra DBMS e che devono usare ODBC in modo relativamente generico. Per ulteriori informazioni sull'interoperabilità, vedere [scegliendo un livello di interoperabilità](../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md).  
  
-   **Applicazioni verticali** applicazioni verticali eseguire un singolo tipo di attività, quali la registrazione degli ordini o i dati di produzione, di rilevamento e di lavoro con uno schema di database che viene controllato dallo sviluppatore dell'applicazione. Per un determinato cliente, l'applicazione funziona con un singolo DBMS. Ad esempio, una piccola azienda può usare l'applicazione con dBASE o FoxPro, mentre potrebbe essere usata da un'azienda di grandi dimensioni con Oracle.  
  
     L'applicazione utilizza ODBC in modo che l'applicazione non è associata a qualsiasi un DBMS, anche se potrebbe essere associato a un numero limitato di DBMS che offrono funzionalità simili. Di conseguenza, lo sviluppatore dell'applicazione può vendere l'applicazione in modo indipendente dal sistema DBMS. Applicazioni verticali sono interoperative quando vengono sviluppati, ma in alcuni casi vengono modificate per includere codice noninteroperable dopo che il cliente ha scelto un DBMS.  
  
-   **Le applicazioni personalizzate** applicazioni personalizzate vengono usate per eseguire un'attività specifica in un'unica azienda. Ad esempio, un'applicazione in una grande azienda potrebbe essere raccogliere i dati di vendita da diverse divisioni (ognuno dei quali utilizza un sistema DBMS diverso) e creare un singolo report. ODBC viene utilizzato perché è un'interfaccia comune e Salva i programmatori di dover apprendere più interfacce. Tali applicazioni in genere non sono interoperabili e vengono scritti in specifici dei DBMS e i driver.  
  
 Un numero di attività è comune a tutte le applicazioni, indipendentemente dal modo in cui usano ODBC. Nel loro insieme, in gran parte definiscono il flusso di qualsiasi applicazione ODBC. Le attività sono:  
  
-   Selezione un'origine dati e la connessione ad esso.  
  
-   Invio di un'istruzione SQL per l'esecuzione.  
  
-   Recupero dei risultati (se presente).  
  
-   Errori di elaborazione.  
  
-   Eseguire il commit o rollback della transazione che racchiude l'istruzione SQL.  
  
-   Disconnessione dall'origine dati.  
  
 Poiché la maggior parte delle operazioni di accesso ai dati viene eseguita con SQL, l'attività primaria per il quale le applicazioni usano ODBC è per inviare istruzioni SQL e recuperare i risultati (se presente) generati da tali istruzioni. Altre attività per cui le applicazioni usano ODBC includono determinazione e la regolazione per le funzionalità del driver e il catalogo del database di esplorazione.
