---
title: Quando utilizzare le procedure Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], about procedures
ms.assetid: 7dc9e327-dd54-4b10-9f66-9ef5c074f122
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31aeea226bc8c8aa41f748d1d9a97d55147c4d67
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289098"
---
# <a name="when-to-use-procedures"></a>Quando usare le procedure
L'utilizzo delle procedure presenta numerosi vantaggi, tutti basati sul fatto che l'utilizzo delle procedure sposta le istruzioni SQL dall'applicazione all'origine dati. Ciò che rimane nell'applicazione è una chiamata di procedura interoperabile. Questi vantaggi includono:  
  
-   **Prestazioni** Le procedure sono in genere il modo più rapido per eseguire istruzioni SQL. Analogamente all'esecuzione preparata, l'istruzione viene compilata ed eseguita in due passaggi distinti. A differenza dell'esecuzione preparata, le procedure vengono eseguite solo in fase di esecuzione. Essi sono compilati in un momento diverso.  
  
-   **Regole di business** Una *regola di business* è una regola sul modo in cui un'azienda fa affari. Ad esempio, solo una persona con il titolo Persona vendita potrebbe essere autorizzata ad aggiungere nuovi ordini cliente. L'inserimento di queste regole nelle procedure consente alle singole società di personalizzare le applicazioni verticali riscrivendo le procedure chiamate dall'applicazione senza dover modificare il codice dell'applicazione. Ad esempio, un'applicazione di immissione ordini potrebbe chiamare la routine **InsertOrder** con un numero fisso di parametri; esattamente come **InsertOrder** viene implementato può variare da azienda a azienda.  
  
-   **Sostituibilità** Strettamente legato all'inserimento di regole di business nelle procedure è il fatto che le procedure possono essere sostituite senza ricompilare la domanda. Se una regola business cambia dopo che una società ha acquistato e installato un'applicazione, la società può modificare la procedura contenente tale regola. Dal punto di vista dell'applicazione, nulla è cambiato; chiama ancora una particolare procedura per eseguire un particolare compito.  
  
-   **SQL specifico di DBMS** Le procedure consentono alle applicazioni di sfruttare SQL specifico di DBMS e rimangono comunque interoperabili. Ad esempio, una procedura in un DBMS che supporta le istruzioni di controllo del flusso in SQL potrebbe intercettare e ripristinare da errori, mentre una procedura in un DBMS che non supporta le istruzioni di controllo del flusso potrebbe semplicemente restituire un errore.  
  
-   **Le procedure sopravvivono alle transazioni** In alcune origini dati, i piani di accesso per tutte le istruzioni preparate in una connessione vengono eliminati quando viene eseguito il commit o il rollback di una transazione. Inserendo istruzioni SQL in procedure, che vengono archiviate in modo permanente nell'origine dati, le istruzioni sopravvivono alla transazione. Se le procedure sopravvivono in uno stato preparato, parzialmente preparato o impreparato è specifico del DBMS.  
  
-   **Sviluppo separato** Le procedure possono essere sviluppate separatamente dal resto dell'applicazione. Nelle grandi aziende, questo potrebbe fornire un modo per sfruttare ulteriormente le competenze di programmatori altamente specializzati. In altre parole, i programmatori di applicazioni possono scrivere codice dell'interfaccia utente e i programmatori di database possono scrivere procedure.  
  
 Le procedure vengono in genere utilizzate dalle applicazioni verticali e personalizzate. Queste applicazioni tendono a eseguire attività fisse ed è possibile hardcoded chiamate di procedura in essi. Ad esempio, un'applicazione per la registrazione degli ordini potrebbe chiamare le routine **InsertOrder**, **DeleteOrder**, **UpdateOrder**e **GetOrders**.  
  
 Non c'è motivo di chiamare procedure da applicazioni generiche. Le procedure vengono in genere scritte per eseguire un'attività nel contesto di una determinata applicazione e pertanto non devono essere utilizzate per le applicazioni generiche. Ad esempio, un foglio di calcolo non ha motivo di chiamare il **InsertOrder** procedura appena menzionata. Inoltre, le applicazioni generiche non devono costruire procedure in fase di esecuzione nella speranza di fornire un'esecuzione più rapida delle istruzioni; non solo è questo probabile che sia più lento rispetto all'esecuzione preparata o diretta, ma richiede anche istruzioni SQL specifiche di DBMS.  
  
 Un'eccezione è agli ambienti di sviluppo delle applicazioni, che spesso forniscono ai programmatori un modo per compilare istruzioni SQL che eseguono procedure e possono fornire ai programmatori un modo per testare le procedure. Tali ambienti chiamano **SQLProcedures** per elencare le procedure disponibili e **SQLProcedureColumns** per elencare i parametri di input, input/output e output, il valore restituito della procedura e le colonne di qualsiasi set di risultati creato da una procedura. Tuttavia, tali procedure devono essere sviluppate in anticipo su ogni origine dati; questa operazione richiede istruzioni SQL specifiche del DBMS.  
  
 L'utilizzo delle procedure presenta tre svantaggi principali. Il primo è che le procedure devono essere scritte e compilate per ogni DBMS con cui l'applicazione deve essere eseguita. Anche se questo non è un problema per le applicazioni personalizzate, può aumentare significativamente i tempi di sviluppo e manutenzione per le applicazioni verticali progettate per l'esecuzione con un numero di DBSMO.  
  
 Il secondo svantaggio è che molti DBSMO non supportano le procedure. Anche in questo caso, questo è più probabile che sia un problema per le applicazioni verticali progettate per l'esecuzione con un numero di DBSMO. Per determinare se le procedure sono supportate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_PROCEDURES.  
  
 Il terzo svantaggio, particolarmente applicabile agli ambienti di sviluppo di applicazioni, è che ODBC non definisce una grammatica standard per la creazione di procedure. In altri parole, sebbene le applicazioni possano chiamare le procedure in modo interoperabile, esse non possono crearle in modo interoperabile.
