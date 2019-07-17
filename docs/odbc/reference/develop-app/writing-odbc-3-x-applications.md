---
title: Scrivere le applicazioni ODBC 3.x | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 9939d11e3a779cc25d7faeb4950783353947f140
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081452"
---
# <a name="writing-odbc-3x-applications"></a>Scrittura di applicazioni ODBC 3. x
Quando un'applicazione ODBC *2.x* dell'applicazione viene aggiornata a ODBC *3.x*, deve essere scritta in modo che funziona con entrambi ODBC *2.x* e *3.x* driver . L'applicazione deve incorporare il codice condizionale per sfruttare appieno ODBC *3.x* funzionalità.  
  
 L'attributo di ambiente SQL_ATTR_ODBC_VERSION deve essere impostato su SQL_OV_ODBC2. Ciò garantisce che il driver si comporta come un database ODBC *2.x* driver per quanto riguarda le modifiche descritte nella sezione [modifiche del comportamento](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Se l'applicazione utilizzerà le funzionalità descritte nella sezione [nuove funzionalità](../../../odbc/reference/develop-app/new-features.md), codice condizionale deve essere utilizzato per determinare se il driver è un database ODBC *3.x* ODBC o *2.x* driver. L'applicazione utilizza **SQLGetDiagField** e **SQLGetDiagRec** ottenere ODBC *3.x* SQLSTATEs durante questa operazione di errore durante l'elaborazione su questi frammenti di codice condizionale. È necessario considerare quanto riportato di seguito sulla nuova funzionalità:  
  
-   Un'applicazione interessata dalla modifica del comportamento delle dimensioni del set di righe deve prestare attenzione a non chiamare **SQLFetch** quando le dimensioni della matrice sono maggiore di 1. Queste applicazioni devono sostituire le chiamate a **SQLExtendedFetch** con chiamate al **SQLSetStmtAttr** impostare l'attributo di istruzione SQL_ATTR_ARRAY_STATUS_PTR e a **SQLFetchScroll**, in modo da disporre di codice comune che funziona con entrambi ODBC *3.x* e ODBC *2.x* driver. In quanto **SQLSetStmtAttr** con SQL_ATTR_ROW_ARRAY_SIZE verrà mappato **SQLSetStmtAttr** con SQL_ROWSET_SIZE per ODBC *2.x* driver, le applicazioni possono impostare solo SQL _ATTR_ROW_ARRAY_SIZE per le operazioni di recupero con più righe.  
  
-   La maggior parte delle applicazioni che esegue l'aggiornamento non vengono effettivamente interessate dalle modifiche apportate ai codici di errore SQLSTATE. Per le applicazioni interessate, possono eseguire una ricerca meccanica e sostituisci nella maggior parte dei casi di utilizzo della tabella di conversione errore nella sezione "Mapping di SQLSTATE" per convertire ODBC *3.x* codici di errore ODBC *2.x* codici. Poiché ODBC *3.x* Driver Manager eseguirà il mapping da ODBC *2.x* SQLSTATEs a ODBC *3.x* SQLSTATEs, gli autori di queste applicazioni solo controllo necessario per ODBC  *3.x* SQLSTATE, non preoccuparti incluso ODBC *2.x* SQLSTATEs nel codice condizionale.  
  
-   Se un'applicazione esegue ottimo uso data, ora e tipi di dati timestamp, l'applicazione può dichiarare in modo da essere un database ODBC *2.x* applicazione e usare codice invece di usare codice condizionata relativo esistente.  
  
 L'aggiornamento deve includere anche i passaggi seguenti:  
  
-   Chiamare **SQLSetEnvAttr** prima dell'allocazione di una connessione per impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION SQL_OV_ODBC2.  
  
-   Sostituire tutte le chiamate a **SQLAllocEnv**, **SQLAllocConnect**, o **SQLAllocStmt** con chiamate a **SQLAllocHandle** con l'appropriato *HandleType* argomento SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Sostituire tutte le chiamate a **SQLFreeEnv** oppure **SQLFreeConnect** con le chiamate a **SQLFreeHandle** con l'appropriato *HandleType* argomento di SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Sostituire tutte le chiamate a **SQLSetConnectOption** con chiamate al **SQLSetConnectAttr**. Se l'impostazione di un attributo il cui valore è una stringa, impostare il *StringLength* argomento in modo appropriato. Change *attributo* argomento da SQL_XXXX SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLGetConnectOption** con chiamate al **SQLGetConnectAttr**. Se riceve una stringa o un attributo binario, impostare *BufferLength* sul valore appropriato e passare un *StringLength* argomento. Change *attributo* argomento da SQL_XXXX SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLSetStmtOption** con chiamate al **SQLSetStmtAttr**. Se l'impostazione di un attributo il cui valore è una stringa, impostare il *StringLength* argomento in modo appropriato. Change *attributo* argomento da SQL_XXXX SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLGetStmtOption** con chiamate al **SQLGetStmtAttr**. Se riceve una stringa o un attributo binario, impostare *BufferLength* sul valore appropriato e passare un *StringLength* argomento. Change *attributo* argomento da SQL_XXXX SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLTransact** con chiamate al **SQLEndTran**. Se l'handle valido più a destra nel **SQLTransact** chiamata è un handle di ambiente, una *HandleType* argomento SQL_HANDLE_ENV deve essere usato nel **SQLEndTran** chiamare con appropriato *gestire* argomento. Se l'handle valido più a destra nel **SQLTransact** chiamata è un handle di connessione, un *HandleType* argomento SQL_HANDLE_DBC deve essere usato nel **SQLEndTran** chiamare con appropriato *gestire* argomento.  
  
-   Sostituire tutte le chiamate a **SQLColAttributes** con chiamate al **SQLColAttribute**. Se il *FieldIdentifier* argomento è SQL_COLUMN_PRECISION SQL_COLUMN_SCALE oppure SQL_COLUMN_LENGTH, non modificare qualsiasi elemento diverso dal nome della funzione. In caso contrario, modificare *FieldIdentifier* da SQL_COLUMN_XXXX a SQL_DESC_XXXX. Se *FieldIdentifier* SQL_DESC_CONCISE_TYPE è e il tipo di dati è un tipo di dati datetime, modificare in ODBC corrispondente *3.x* tipo di dati.  
  
-   Se utilizza cursori rettangolari, cursori scorrevoli o entrambi, l'applicazione effettua quanto segue:  
  
    -   Imposta le dimensioni del set di righe, il tipo di cursore e concorrenza cursore utilizzando **SQLSetStmtAttr**.  
  
    -   Le chiamate **SQLSetStmtAttr** Impostare SQL_ATTR_ROW_STATUS_PTR affinché punti a una matrice di record di stato.  
  
    -   Le chiamate **SQLSetStmtAttr** impostare SQL_ATTR_ROWS_FETCHED_PTR in modo che punti a un' SQLINTEGER.  
  
    -   Esegue le associazioni necessarie ed esegue l'istruzione SQL.  
  
    -   Le chiamate **SQLFetchScroll** in un ciclo per recuperare righe e spostarsi nel risultato impostato.  
  
    -   Se desidera recuperare dal segnalibro, l'applicazione chiama **SQLSetStmtAttr** per impostare una variabile che conterrà il segnalibro per la riga di cui si vuole recuperare e chiama SQL_ATTR_FETCH_BOOKMARK_PTR **SQLFetchScroll** con un *FetchOrientation* argomento impostato su sql_fetch_bookmark.  
  
-   Se si usa matrici di parametri, l'applicazione effettua quanto segue:  
  
    -   Le chiamate **SQLSetStmtAttr** per impostare l'attributo SQL_ATTR_PARAMSET_SIZE alla dimensione della matrice di parametri.  
  
    -   Le chiamate **SQLSetStmtAttr** impostare SQL_ATTR_ROWS_PROCESSED_PTR in modo che punti a una variabile UDWORD interna.  
  
    -   Esegue la preparazione, associare ed eseguire operazioni in base alle esigenze.  
  
    -   Se l'esecuzione si arresta per qualche motivo (ad esempio SQL_NEED_DATA), è possibile trovare la riga "corrente" dei parametri controllando la posizione a cui punta SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti delle applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Chiamata di SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Chiamata di SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Chiamata di SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operazioni della libreria di cursori](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Mapping degli attributi del cursore1 Tipi di informazioni](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
