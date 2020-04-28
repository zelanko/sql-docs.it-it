---
title: Scrittura di applicazioni ODBC 3. x | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], about upgrading
- ODBC drivers [ODBC], backward compatibility
- upgrading applications [ODBC]
- compatibility [ODBC], upgrading applications
- application upgrades [ODBC]
- upgrading applications [ODBC], about upgrading
- backward compatibility [ODBC], upgrading applications
ms.assetid: 19c54fc5-9dd6-49b6-8c9f-a38961b40a65
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ba48d76babcaa5fcc49a541088f7c4cc349b569
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81288989"
---
# <a name="writing-odbc-3x-applications"></a>Scrittura di applicazioni ODBC 3. x
Quando un'applicazione ODBC *2. x* viene aggiornata a ODBC *3. x*, deve essere scritta in modo che funzioni con i driver ODBC *2. x* e *3. x* . L'applicazione deve incorporare il codice condizionale per sfruttare appieno le funzionalità di ODBC *3. x* .  
  
 L'attributo SQL_ATTR_ODBC_VERSION Environment deve essere impostato su SQL_OV_ODBC2. In questo modo, il driver si comporta come un driver ODBC *2. x* rispetto alle modifiche descritte nella sezione [modifiche comportamentali](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Se l'applicazione utilizzerà le funzionalità descritte nella sezione [nuove funzionalità](../../../odbc/reference/develop-app/new-features.md), è necessario utilizzare il codice condizionale per determinare se il driver è un driver ODBC *3. x* o ODBC *2. x* . L'applicazione utilizza **SQLGetDiagField** e **SQLGETDIAGREC** per ottenere ODBC *3. x* sqlstates durante l'elaborazione degli errori in questi frammenti di codice condizionale. È necessario considerare i seguenti punti relativi alla nuova funzionalità:  
  
-   Un'applicazione interessata dalla modifica del comportamento delle dimensioni del set di righe deve prestare attenzione a non chiamare **SQLFetch** quando la dimensione della matrice è maggiore di 1. Queste applicazioni devono sostituire le chiamate a **SQLExtendedFetch** con le chiamate a **SQLSetStmtAttr** per impostare l'attributo dell'istruzione SQL_ATTR_ARRAY_STATUS_PTR e su **SQLFetchScroll**, in modo che dispongano di codice comune che funziona con i driver ODBC *3. x* e ODBC *2. x* . Poiché **SQLSetStmtAttr** con SQL_ATTR_ROW_ARRAY_SIZE verrà mappato a **SQLSetStmtAttr** con SQL_ROWSET_SIZE per i driver ODBC *2. x* , le applicazioni possono semplicemente impostare SQL_ATTR_ROW_ARRAY_SIZE per le operazioni di recupero più righe.  
  
-   La maggior parte delle applicazioni che eseguono l'aggiornamento non sono effettivamente interessate dalle modifiche apportate ai codici SQLSTATE. Per le applicazioni interessate, è possibile eseguire una ricerca meccanica e sostituire nella maggior parte dei casi utilizzando la tabella di conversione degli errori nella sezione "mapping SQLSTATE" per convertire i codici di errore ODBC *3. x* in codici ODBC *2. x* . Poiché la gestione driver ODBC *3. x* eseguirà il mapping da ODBC *2. x* sqlstates a ODBC *3. x* sqlstates, questi writer di applicazioni devono solo controllare la presenza di sqlstates ODBC *3. x* e non preoccuparsi di includere sqlstates ODBC *2. x* nel codice condizionale.  
  
-   Se un'applicazione utilizza i tipi di dati data, ora e timestamp, l'applicazione può dichiararsi come un'applicazione ODBC *2. x* e utilizzare il codice esistente anziché utilizzare il codice condizionale.  
  
 L'aggiornamento deve includere anche i passaggi seguenti:  
  
-   Chiamare **SQLSetEnvAttr** prima di allocare una connessione per impostare l'attributo dell'ambiente SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC2.  
  
-   Sostituire tutte le chiamate a **SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt** con le chiamate a **SQLAllocHandle** con l'argomento *HandleType* appropriato di SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Sostituire tutte le chiamate a **SQLFreeEnv** o **SQLFreeConnect** con chiamate a **SQLFreeHandle** con l'argomento *HandleType* appropriato di SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Sostituire tutte le chiamate a **SQLSetConnectOption** con le chiamate a **SQLSetConnectAttr**. Se si imposta un attributo il cui valore è una stringa, impostare l'argomento *StringLength* in modo appropriato. Modificare l'argomento dell' *attributo* da SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLGetConnectOption** con le chiamate a **SQLGetConnectAttr**. Se si recupera un attributo stringa o binario, impostare *bufferLength* sul valore appropriato e passare un argomento *StringLength* . Modificare l'argomento dell' *attributo* da SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLSetStmtOption** con le chiamate a **SQLSetStmtAttr**. Se si imposta un attributo il cui valore è una stringa, impostare l'argomento *StringLength* in modo appropriato. Modificare l'argomento dell' *attributo* da SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLGetStmtOption** con le chiamate a **SQLGetStmtAttr**. Se si recupera un attributo stringa o binario, impostare *bufferLength* sul valore appropriato e passare un argomento *StringLength* . Modificare l'argomento dell' *attributo* da SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLTransact** con le chiamate a **SQLEndTran**. Se l'handle valido più a destra nella chiamata **SQLTransact** è un handle di ambiente, è necessario usare un argomento *HandleType* di SQL_HANDLE_ENV nella chiamata **SQLEndTran** con l'argomento *handle* appropriato. Se l'handle valido più a destra nella chiamata **SQLTransact** è un handle di connessione, è necessario usare un argomento *HandleType* di SQL_HANDLE_DBC nella chiamata **SQLEndTran** con l'argomento *handle* appropriato.  
  
-   Sostituire tutte le chiamate a **SQLColAttributes** con le chiamate a **SQLColAttribute**. Se l'argomento *FieldIdentifier* è SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE o SQL_COLUMN_LENGTH, non modificare un valore diverso dal nome della funzione. In caso contrario, modificare *FieldIdentifier* da SQL_COLUMN_XXXX a SQL_DESC_XXXX. Se *FieldIdentifier* è SQL_DESC_CONCISE_TYPE e il tipo di dati è un tipo di dati DateTime, modificare il tipo di dati ODBC *3. x* corrispondente.  
  
-   Se si utilizzano cursori a blocchi, cursori scorrevoli o entrambi, l'applicazione esegue le operazioni seguenti:  
  
    -   Imposta la dimensione del set di righe, il tipo di cursore e la concorrenza del cursore utilizzando **SQLSetStmtAttr**.  
  
    -   Chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR in modo che punti a una matrice di record di stato.  
  
    -   Chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROWS_FETCHED_PTR in modo che punti a un SQLINTEGER.  
  
    -   Esegue le associazioni necessarie ed esegue l'istruzione SQL.  
  
    -   Chiama **SQLFetchScroll** in un ciclo per recuperare le righe e spostarsi nel set di risultati.  
  
    -   Se desidera eseguire il recupero tramite segnalibro, l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_FETCH_BOOKMARK_PTR su una variabile che conterrà il segnalibro per la riga che desidera recuperare e chiama **SQLFetchScroll** con un argomento *FetchOrientation* di SQL_FETCH_BOOKMARK.  
  
-   Se si utilizzano matrici di parametri, l'applicazione esegue le operazioni seguenti:  
  
    -   Chiama **SQLSetStmtAttr** per impostare l'attributo SQL_ATTR_PARAMSET_SIZE sulla dimensione della matrice di parametri.  
  
    -   Chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROWS_PROCESSED_PTR in modo che punti a una variabile udword interna.  
  
    -   Esegue le operazioni di preparazione, associazione ed esecuzione nel modo appropriato.  
  
    -   Se l'esecuzione si interrompe per qualsiasi motivo (ad esempio SQL_NEED_DATA), è possibile trovare la riga "Current" di parametri controllando la posizione a cui punta SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti delle applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Chiamata di SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Chiamata di SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Chiamata di SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operazioni della libreria di cursori](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Mapping delle informazioni di tipo Cursor Attributes1](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
