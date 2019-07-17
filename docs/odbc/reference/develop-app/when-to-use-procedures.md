---
title: Quando usare le procedure | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f25b629372bbe089489cccdbfa0258dafef3dd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078965"
---
# <a name="when-to-use-procedures"></a>Quando usare le procedure
Esistono numerosi vantaggi rispetto all'utilizzo delle procedure; tutti basata sul fatto che tramite le procedure passa istruzioni SQL dall'applicazione per l'origine dati. Ciò che resta nell'applicazione è una chiamata di procedura interoperativa. Tali vantaggi includono:  
  
-   **Prestazioni** procedure vengono in genere il modo più rapido per eseguire istruzioni SQL. Come preparare l'esecuzione, l'istruzione viene compilato ed eseguito in due passaggi distinti. A differenza di esecuzione preparata, procedure vengono eseguite solo in fase di esecuzione. Vengono compilati in un momento diverso.  
  
-   **Le regole di business** un' *regola business* è una regola sul modo in cui un'azienda intrattiene relazioni commerciali. Ad esempio, solo gli utenti con il titolo del venditore potrebbe essere consentito aggiungere nuovi ordini di vendita. L'inserimento di queste regole nelle procedure consente alle aziende singoli personalizzare le applicazioni verticali riscrivendo le procedure chiamate dall'applicazione senza dover modificare il codice dell'applicazione. Ad esempio, un'applicazione di immissione dell'ordine potrebbe chiamare la routine **InsertOrder** con un numero fisso di parametri; esattamente come **InsertOrder** viene implementato possono variare dalla società.  
  
-   **Replaceability** strettamente correlati all'inserimento di regole di business nelle procedure è dovuto al fatto che le procedure possono essere sostituite senza ricompilare l'applicazione. Se una regola business viene modificata dopo che una società ha acquistato e ha installato un'applicazione, la società può sostituire la routine contenente tale regola. Dal punto di vista dell'applicazione, è cambiato nulla; viene chiamato comunque una particolare procedura per portare a termine una determinata attività.  
  
-   **SQL specifici del DBMS** procedure forniscono un modo per le applicazioni dagli exploit specifici del DBMS SQL e sono tuttora disponibili interoperativa. Ad esempio, una procedura in un sistema DBMS che supporta le istruzioni di controllo di flusso in SQL potrebbe intercettare e correggere gli errori, mentre una procedura in un sistema DBMS che non supporta le istruzioni di controllo di flusso può semplicemente restituire un errore.  
  
-   **Le procedure sopravvivono transazioni** alcune origini dati, i piani di accesso per le istruzioni preparate tutti su una connessione verranno eliminati quando una transazione viene eseguito il commit o rollback. Inserendo istruzioni SQL in procedure che sono archiviate in modo permanente nell'origine dati, le istruzioni di sopravvivono alla transazione. Se le procedure di sopravvivono in un preparata, parzialmente preparata, o non preparato lo stato è specifici del DBMS.  
  
-   **Separare sviluppo** procedure possono essere sviluppate separatamente dal resto dell'applicazione. In grandi aziende, questo potrebbe fornire un modo per sfruttare ulteriormente le competenze degli sviluppatori altamente specializzati. In altre parole, i programmatori di applicazioni possono scrivere il codice dell'interfaccia utente e ai programmatori di database possono scrivere procedure.  
  
 Procedure vengono in genere usate da applicazioni personalizzate e verticale. Queste applicazioni tendono a eseguire attività fissa, ed è possibile per le chiamate di procedura a livello di codice in essi contenuti. Ad esempio, un'applicazione di immissione dell'ordine può chiamare le procedure descritte **InsertOrder**, **DeleteOrder**, **UpdateOrder**, e **GetOrders** .  
  
 Non si ha a chiamare le procedure da applicazioni generiche. Le procedure vengono in genere scritti per eseguire un'attività nel contesto di una determinata applicazione e pertanto non sono utili per applicazioni generiche. Ad esempio, un foglio di calcolo non ha motivo di chiamare il **InsertOrder** procedure descritti in precedenza. Inoltre, le applicazioni generiche non devono costruire le procedure in fase di esecuzione nella speranza di lasciare che fornisce un'esecuzione più rapida istruzione; non solo è probabilmente da risultare più lenta dell'esecuzione diretta o preparata, richiede anche le istruzioni SQL specifici del DBMS.  
  
 Un'eccezione è ambienti di sviluppo delle applicazioni, che offrono spesso un modo per i programmatori di creare istruzioni SQL che eseguono le procedure e possono fornire un modo per i programmatori a procedure di test. Chiamata di questo tipo ambienti **SQLProcedures** per le procedure disponibili di elenco e **SQLProcedureColumns** per elencare i parametri di input, input/output e output, la procedura di valore restituito e le colonne di qualsiasi set di risultati creati da una procedura. Tuttavia, tali procedure devono essere sviluppate in anticipo su ogni origine dati. Questa operazione richiede le istruzioni SQL specifici del DBMS.  
  
 Esistono tre principali svantaggi all'utilizzo delle procedure. Il primo è che le procedure devono essere scritte e compilate per ogni sistema DBMS con cui l'applicazione deve essere eseguita. Anche se ciò non costituisce un problema per le applicazioni personalizzate, è possibile aumentare significativamente lo sviluppo e l'ora di manutenzione per applicazioni verticali progettato per essere eseguito con un numero di DBMS.  
  
 Il secondo svantaggio è che maggior parte dei DBMS non supportano le procedure. Anche in questo caso, la più probabile è un problema per le applicazioni verticali progettato per essere eseguito con un numero di DBMS. Per determinare se le procedure sono supportate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_PROCEDURES.  
  
 Lo svantaggio di terzo, che è applicabile in particolar modo per gli ambienti di sviluppo dell'applicazione, è che ODBC non viene definita una grammatica di standard per la creazione di procedure. Vale a dire, anche se le applicazioni possono chiamare interoperably procedure, essi non può crearli interoperably.
