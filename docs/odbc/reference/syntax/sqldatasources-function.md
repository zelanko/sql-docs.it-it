---
title: Funzione SQLDataSources . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b56a6c25e54897e67beaf39d3b7797ac45391d7b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301181"
---
# <a name="sqldatasources-function"></a>Funzione SQLDataSources
**Conformità**  
 Versione introdotta: ODBC 1.0 Standards Compliance: ISO 92  
  
 **Riepilogo**  
 **SQLDataSources** restituisce informazioni su un'origine dati. Questa funzione viene implementata solo da Gestione Driver.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *EnvironmentHandle*  
 [Ingresso] Maniglia dell'ambiente.  
  
 *Direzione*  
 [Ingresso] Determina su quale origine dati vengono restituite le informazioni. I possibili valori sono i seguenti:  
  
 SQL_FETCH_NEXT (per recuperare il nome dell'origine dati successiva nell'elenco), SQL_FETCH_FIRST (per recuperare dall'inizio dell'elenco), SQL_FETCH_FIRST_USER (per recuperare il primo DSN utente) o SQL_FETCH_FIRST_SYSTEM (per recuperare il primo DSN di sistema).  
  
 Quando *Direction* è impostato su SQL_FETCH_FIRST, le chiamate successive a **SQLDataSources** con *Direction* impostato su SQL_FETCH_NEXT restituiscono DSN sia dell'utente che di sistema. Quando *Direction* è impostato su SQL_FETCH_FIRST_USER, tutte le chiamate successive a **SQLDataSources** con *Direction* impostato su SQL_FETCH_NEXT restituiscono solo DSN utente. Quando *Direction* è impostato su SQL_FETCH_FIRST_SYSTEM, tutte le chiamate successive a **SQLDataSources** con *Direction* impostato su SQL_FETCH_NEXT restituiscono solo DSN di sistema.  
  
 *ServerName*  
 [Uscita] Puntatore a un buffer in cui restituire il nome dell'origine dati.  
  
 Se *ServerName* è NULL, *NameLength1Ptr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *ServerName*.  
  
 *BufferLength1*  
 [Ingresso] Lunghezza del buffer*NomeServer,* in caratteri; non è necessario che sia più lungo di SQL_MAX_DSN_LENGTH più il carattere di terminazione null.  
  
 *NameLength1Ptr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per la restituzione in \* *ServerName*. Se il numero di caratteri disponibili per la restituzione è maggiore \*o uguale a *BufferLength1*, il nome dell'origine dati in *ServerName* verrà troncato a *BufferLength1* meno la lunghezza di un carattere di terminazione null.  
  
 *Descrizione*  
 [Uscita] Puntatore a un buffer in cui restituire la descrizione del driver associato all'origine dati. Ad esempio, dBASE o SQL Server.  
  
 Se *Description* è NULL, *NameLength2Ptr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *Descrizione*.  
  
 *BufferLength2*  
 [Ingresso] Lunghezza in caratteri del buffer di*descrizione.*  
  
 *NameLength2Ptr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per la restituzione in \* *Descrizione*. Se il numero di caratteri disponibili per la restituzione è maggiore o uguale a *BufferLength2*, la descrizione del driver in \* *Description* verrà troncata a *BufferLength2* meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDataSources** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_ENV e un *handle* di *EnvironmentHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLDataSources** e vengono illustrati ognuno di essi nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|(DM) messaggio informativo specifico di Gestione Driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|(DM) il \*buffer *ServerName* non era sufficientemente grande per restituire il nome completo dell'origine dati. Pertanto, il nome è stato troncato. La lunghezza dell'intero nome dell'origine dati viene restituita in \* *NameLength1Ptr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) La \* *descrizione* del buffer non era sufficientemente grande per restituire la descrizione completa del driver. Pertanto, la descrizione è stata troncata. La lunghezza della descrizione dell'origine dati non troncata viene restituita in*NameLength2Ptr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|(DM) Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|(DM) Gestione Driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *BufferLength1* è minore di 0.<br /><br /> (DM) il valore specificato per l'argomento *BufferLength2* è minore di 0.|  
|I103|Codice di recupero non valido|(DM) il valore specificato per l'argomento *Direzione* non è uguale a SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM o SQL_FETCH_NEXT.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Commenti  
 Poiché **SQLDataSources** è implementato in Gestione Driver, è supportato per tutti i driver indipendentemente dalla conformità agli standard di un driver specifico.  
  
 Un'applicazione può chiamare **SQLDataSources** più volte per recuperare tutti i nomi delle origini dati. Gestione Driver recupera queste informazioni dalle informazioni di sistema. Quando non sono presenti più nomi di origini dati, Gestione Driver restituisce SQL_NO_DATA. Se **SQLDataSources** viene chiamato con SQL_FETCH_NEXT immediatamente dopo SQL_NO_DATA, restituirà il primo nome dell'origine dati. Per informazioni sull'utilizzo delle informazioni restituite da **SQLDataSources da sqlDataSources**, vedere [Scelta di un'origine dati o di un driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se SQL_FETCH_NEXT viene passato a **SQLDataSources** la prima volta che viene chiamato, restituirà il primo nome dell'origine dati.  
  
 Il driver determina la modalità di mapping dei nomi delle origini dati alle origini dati effettive.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Individuazione ed elenco dei valori necessari per connettersi a un'origine dati|[Funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnectSQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Connessione a un'origine dati tramite una stringa di connessione o una finestra di dialogoConnecting to a data source using a connection string or dialog box|[SQLDriverConnect Function](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Restituzione delle descrizioni e degli attributi dei driver|[Funzione SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
