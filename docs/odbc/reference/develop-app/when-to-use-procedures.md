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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078965"
---
# <a name="when-to-use-procedures"></a>Quando usare le procedure
L'utilizzo delle procedure comporta diversi vantaggi, in base al fatto che l'utilizzo di procedure consente di spostare istruzioni SQL dall'applicazione all'origine dati. Ciò che rimane nell'applicazione è una chiamata di procedura interoperativa. Questi vantaggi includono:  
  
-   **Prestazioni** Le procedure sono in genere il modo più rapido per eseguire istruzioni SQL. Analogamente all'esecuzione preparata, l'istruzione viene compilata ed eseguita in due passaggi distinti. Diversamente dall'esecuzione preparata, le procedure vengono eseguite solo in fase di esecuzione. Sono compilati in un momento diverso.  
  
-   **Regole business** Una *regola business* è una regola in merito al modo in cui un'azienda svolge le proprie attività. Ad esempio, solo un utente con il titolo Sales Person potrebbe essere autorizzato ad aggiungere nuovi ordini di vendita. L'inserimento di queste regole nelle procedure consente alle singole aziende di personalizzare le applicazioni verticali riscrivendo le procedure chiamate dall'applicazione senza dover modificare il codice dell'applicazione. Ad esempio, un'applicazione Order Entry può chiamare la stored procedure **InsertOrder** con un numero fisso di parametri; la modalità di implementazione di **InsertOrder** può variare esattamente da società a azienda.  
  
-   **Sostituzione** L'inserimento di regole business nelle procedure è strettamente correlato al fatto che le stored procedure possono essere sostituite senza ricompilare l'applicazione. Se una regola business viene modificata dopo che un'azienda ha acquistato e installato un'applicazione, l'azienda può modificare la procedura che contiene la regola. Dal punto di vista dell'applicazione, non è stato modificato nulla. chiama comunque una procedura specifica per eseguire un'attività specifica.  
  
-   **SQL specifico di DBMS** Le procedure consentono alle applicazioni di sfruttare SQL specifiche del sistema DBMS e rimangono comunque interoperativi. Ad esempio, una procedura in un sistema DBMS che supporta istruzioni per il controllo di flusso in SQL potrebbe intercettare e correggere gli errori, mentre una procedura in un sistema DBMS che non supporta istruzioni per il controllo di flusso potrebbe semplicemente restituire un errore.  
  
-   **Procedure che sopravvivono alle transazioni** In alcune origini dati, i piani di accesso per tutte le istruzioni preparate in una connessione vengono eliminati quando viene eseguito il commit o il rollback di una transazione. Inserendo istruzioni SQL nelle procedure, che vengono archiviate in modo permanente nell'origine dati, le istruzioni sopravvivono alla transazione. Il fatto che le procedure sopravvivano in uno stato preparato, Parzialmente preparato o non preparato sono specifiche del sistema DBMS.  
  
-   **Sviluppo separato** Le procedure possono essere sviluppate separatamente dal resto dell'applicazione. Nelle grandi aziende, questo potrebbe fornire un modo per sfruttare al meglio le competenze dei programmatori altamente specializzati. In altre parole, i programmatori di applicazioni possono scrivere codice dell'interfaccia utente e i programmatori di database possono scrivere procedure.  
  
 Le procedure vengono in genere utilizzate da applicazioni verticali e personalizzate. Queste applicazioni tendono a eseguire attività fisse ed è possibile eseguire chiamate a procedure hardcoded. Ad esempio, un'applicazione Order Entry può chiamare le procedure **InsertOrder**, **DeleteOrder**, **UpdateOrder**e **GetOrders**.  
  
 Non esiste un motivo per chiamare le routine dalle applicazioni generiche. Le stored procedure vengono in genere scritte per eseguire un'attività nel contesto di una particolare applicazione e pertanto non possono essere utilizzate nelle applicazioni generiche. Un foglio di calcolo, ad esempio, non ha motivo di chiamare la procedura **InsertOrder** appena citata. Inoltre, le applicazioni generiche non devono creare procedure in fase di esecuzione durante la speranza di fornire un'esecuzione più rapida delle istruzioni; non solo è probabile che sia più lenta dell'esecuzione preparata o diretta, ma richiede anche istruzioni SQL specifiche del sistema DBMS.  
  
 Un'eccezione è rappresentata dagli ambienti di sviluppo dell'applicazione, che spesso consentono ai programmatori di compilare istruzioni SQL che eseguono procedure e possono fornire un modo per i programmatori di testare le procedure. Tali ambienti chiamano **SqlProcedure** per elencare le procedure disponibili e **SQLProcedureColumns** per elencare i parametri di input, di input/output e di output, il valore restituito della procedura e le colonne di tutti i set di risultati creati da una procedura. Tuttavia, tali procedure devono essere sviluppate in anticipo in ogni origine dati. Questa operazione richiede istruzioni SQL specifiche del sistema DBMS.  
  
 Esistono tre svantaggi principali per l'utilizzo delle procedure. Il primo è che le procedure devono essere scritte e compilate per ogni DBMS con cui l'applicazione deve essere eseguita. Sebbene questo non sia un problema per le applicazioni personalizzate, può aumentare significativamente il tempo di sviluppo e di manutenzione per le applicazioni verticali progettate per l'esecuzione con diversi sistemi DBMS.  
  
 Il secondo svantaggio è che molti DBMS non supportano le procedure. Anche in questo caso, è più probabile che si tratta di un problema per le applicazioni verticali progettate per l'esecuzione con diversi sistemi DBMS. Per determinare se le procedure sono supportate, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_PROCEDURES.  
  
 Il terzo svantaggio, che è particolarmente applicabile agli ambienti di sviluppo delle applicazioni, è che ODBC non definisce una grammatica standard per la creazione di procedure. Ciò è dovuto al fatto che le applicazioni possono chiamare le routine in modo interoperativo, ma non possono crearle in modo interoperativo.
