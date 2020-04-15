---
title: Scrittura di applicazioni ODBC 3.x Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288989"
---
# <a name="writing-odbc-3x-applications"></a>Scrittura di applicazioni ODBC 3. x
Quando un'applicazione ODBC *2.x* viene aggiornata a ODBC *3.x*, deve essere scritta in modo che funzioni con entrambi i driver ODBC *2.x* e *3.x.* L'applicazione deve incorporare codice condizionale per sfruttare appieno le funzionalità di ODBC *3.x.*  
  
 L'attributo di ambiente SQL_ATTR_ODBC_VERSION deve essere impostato su SQL_OV_ODBC2. In questo modo il driver si comporta come un driver ODBC *2.x* rispetto alle modifiche descritte nella sezione [Modifiche comportamentali](../../../odbc/reference/develop-app/behavioral-changes.md).  
  
 Se l'applicazione utilizzerà una delle funzionalità descritte nella sezione [Nuove funzionalità](../../../odbc/reference/develop-app/new-features.md), il codice condizionale deve essere utilizzato per determinare se il driver è un driver ODBC *3.x* o ODBC *2.x.* L'applicazione utilizza **SQLGetDiagField** e **SQLGetDiagRec** per ottenere ODBC *3.x* SQLSTATEs durante l'elaborazione degli errori su questi frammenti di codice condizionale. È necessario considerare i seguenti punti relativi alla nuova funzionalità:  
  
-   Un'applicazione interessata dalla modifica del comportamento delle dimensioni del set di righe deve prestare attenzione a non chiamare SQLFetch quando la dimensione della matrice è maggiore di 1.An application affected by the change in rowset size behavior should be careful not to call **SQLFetch** when the array size is greater than 1. Queste applicazioni devono sostituire le chiamate a **SQLExtendedFetch** con chiamate a **SQLSetStmtAttr** per impostare l'attributo dell'istruzione SQL_ATTR_ARRAY_STATUS_PTR e **su SQLFetchScroll**, in modo che dispongano di codice comune che funziona con i driver ODBC *3.x* e ODBC *2.x.* Poiché **SQLSetStmtAttr** con SQL_ATTR_ROW_ARRAY_SIZE verrà mappato a **SQLSetStmtAttr** con SQL_ROWSET_SIZE per i driver ODBC *2.x,* le applicazioni possono semplicemente impostare SQL_ATTR_ROW_ARRAY_SIZE per le operazioni di recupero multiriga.  
  
-   La maggior parte delle applicazioni che eseguono l'aggiornamento non sono effettivamente interessate dalle modifiche nei codici SQLSTATE. Per le applicazioni interessate, possono eseguire una ricerca meccanica e sostituire nella maggior parte dei casi utilizzando la tabella di conversione degli errori nella sezione "Mapping SQLSTATE" per convertire i codici di errore ODBC *3.x* in codici ODBC *2.x.* Poiché Gestione Driver ODBC *3.x* eseguirà il mapping da ODBC *2.x* SQLSTATEs a ODBC *3.x* SQLSTATEs, questi writer di applicazioni devono solo controllare le SQLSTATE ODBC *3.x* e non preoccuparsi di includere ODBC *2.x* SQLSTATEs nel codice condizionale.  
  
-   Se un'applicazione utilizza in modo eccezionale i tipi di dati di data, ora e timestamp, l'applicazione può dichiararsi un'applicazione ODBC *2.x* e utilizzare il codice esistente anziché utilizzare il codice di condizionamento.  
  
 L'aggiornamento deve includere anche i passaggi seguenti:The upgrade should also include the following steps:  
  
-   Chiamare **SQLSetEnvAttr** prima di allocare una connessione per impostare l'attributo di ambiente SQL_ATTR_ODBC_VERSION su SQL_OV_ODBC2.  
  
-   Sostituire tutte le chiamate a **SQLAllocEnv**, **SQLAllocConnect**o **SQLAllocStmt** con chiamate a **SQLAllocHandle** con l'argomento *HandleType* appropriato di SQL_HANDLE_ENV, SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Sostituire tutte le chiamate a **SQLFreeEnv** o **SQLFreeConnect** con chiamate a **SQLFreeHandle** con l'argomento *HandleType* appropriato di SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
-   Sostituire tutte le chiamate a **SQLSetConnectOption** con chiamate a **SQLSetConnectAttr**. Se si imposta un attributo il cui valore è una stringa, impostare il *StringLength* argomento in modo appropriato. Modificare l'argomento *Attributo* da SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLGetConnectOption** con chiamate a **SQLGetConnectAttr**. Se si ottiene una stringa o un attributo binario, impostare *BufferLength* sul valore appropriato e passare un *StringLength* argomento. Modificare l'argomento *Attributo* da SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLSetStmtOption** con chiamate a **SQLSetStmtAttr**. Se si imposta un attributo il cui valore è una stringa, impostare il *StringLength* argomento in modo appropriato. Modificare l'argomento *Attributo* da SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLGetStmtOption** con chiamate a **SQLGetStmtAttr**. Se si ottiene una stringa o un attributo binario, impostare *BufferLength* sul valore appropriato e passare un *StringLength* argomento. Modificare l'argomento *Attributo* da SQL_XXXX a SQL_ATTR_XXXX.  
  
-   Sostituire tutte le chiamate a **SQLTransact** con chiamate a **SQLEndTran**. Se l'handle valido più a destra nella chiamata **SQLTransact** è un handle di ambiente, un *HandleType* argomento di SQL_HANDLE_ENV deve essere utilizzato nel **SQLEndTran** chiamare con il appropriato *Handle* argomento. Se l'handle valido più a destra nella chiamata **SQLTransact** è un handle di connessione, un *HandleType* argomento di SQL_HANDLE_DBC deve essere utilizzato nel **SQLEndTran** chiamare con il appropriato *Handle* argomento.  
  
-   Sostituire tutte le chiamate a **SQLColAttributes** con chiamate a **SQLColAttribute**. Se l'argomento *FieldIdentifier* è SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE o SQL_COLUMN_LENGTH, non modificare nulla di diverso dal nome della funzione. In caso contrario, modificare *FieldIdentifier* da SQL_COLUMN_XXXX a SQL_DESC_XXXX. Se *FieldIdentifier* è SQL_DESC_CONCISE_TYPE e il tipo di dati è un tipo di dati datetime, passare al tipo di dati ODBC *3.x* corrispondente.  
  
-   Se si utilizzano cursori a blocchi, cursori scorrevoli o entrambi, l'applicazione esegue le operazioni seguenti:  
  
    -   Imposta le dimensioni del set di righe, il tipo di cursore e la concorrenza del cursore utilizzando **SQLSetStmtAttr**.  
  
    -   Chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROW_STATUS_PTR in modo che punti a una matrice di record di stato.  
  
    -   Chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROWS_FETCHED_PTR in modo che punti a un SQLINTEGER.  
  
    -   Esegue le associazioni necessarie ed esegue l'istruzione SQL.  
  
    -   Chiama **SQLFetchScroll** in un ciclo per recuperare le righe e spostarsi nel set di risultati.  
  
    -   Se si desidera recuperare dal segnalibro, l'applicazione chiama **SQLSetStmtAttr** per impostare SQL_ATTR_FETCH_BOOKMARK_PTR su una variabile che conterrà il segnalibro per la riga che si desidera recuperare e chiama **SQLFetchScroll** con un *FetchOrientation* argomento di SQL_FETCH_BOOKMARK.  
  
-   Se si utilizzano matrici di parametri, l'applicazione esegue le operazioni seguenti:  
  
    -   Chiama **SQLSetStmtAttr** per impostare l'attributo SQL_ATTR_PARAMSET_SIZE sulla dimensione della matrice di parametri.  
  
    -   Chiama **SQLSetStmtAttr** per impostare SQL_ATTR_ROWS_PROCESSED_PTR in modo che punti a una variabile UDWORD interna.  
  
    -   Esegue le operazioni di preparazione, associazione ed esecuzione in base alle esigenze.  
  
    -   Se l'esecuzione si interrompe per qualche motivo (ad esempio SQL_NEED_DATA), è possibile trovare la riga "corrente" di parametri controllando la posizione a cui fa riferimento SQL_ATTR_ROWS_PROCESSED_PTR.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Mapping di funzioni di sostituzione per la compatibilità con le versioni precedenti delle applicazioni](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md)  
  
-   [Chiamata di SQLCloseCursor](../../../odbc/reference/develop-app/calling-sqlclosecursor.md)  
  
-   [Chiamata di SQLGetDiagField](../../../odbc/reference/develop-app/calling-sqlgetdiagfield.md)  
  
-   [Chiamata di SQLSetPos](../../../odbc/reference/develop-app/calling-sqlsetpos.md)  
  
-   [Operazioni della libreria di cursori](../../../odbc/reference/develop-app/cursor-library-operations.md)  
  
-   [Mapping delle informazioni di tipo Cursor Attributes1](../../../odbc/reference/develop-app/mapping-the-cursor-attributes1-information-types.md)  
  
-   [SQL_NO_DATA](../../../odbc/reference/develop-app/sql-no-data.md)
