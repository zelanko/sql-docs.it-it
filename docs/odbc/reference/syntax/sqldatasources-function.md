---
title: Funzione SQLDataSources | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9207dde54a14e345e99d3c04d4cb66622d85972e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537642"
---
# <a name="sqldatasources-function"></a>Funzione SQLDataSources
**Conformità**  
 Versione introdotta: Conformità agli standard 1.0 ODBC: ISO 92  
  
 **Riepilogo**  
 **SQLDataSources** restituisce informazioni su un'origine dati. Questa funzione è implementata solo da Gestione Driver.  
  
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
 [Input] Handle di ambiente.  
  
 *Direzione*  
 [Input] Determina l'origine dati in Gestione Driver restituisce informazioni su. I possibili valori sono i seguenti:  
  
 SQL_FETCH_NEXT (per recuperare il nome dell'origine dati successivo nell'elenco), SQL_FETCH_FIRST (per il recupero dall'inizio dell'elenco), SQL_FETCH_FIRST_USER (per il DSN utente fetch il primo) o SQL_FETCH_FIRST_SYSTEM (per recuperare il primo sistema DSN).  
  
 Quando *direzione* è impostata su SQL_FETCH_FIRST, le chiamate successive a **SQLDataSources** con *direzione* impostato su SQL_FETCH_NEXT restituire i DSN utente e di sistema. Quando *direzione* è impostata su SQL_FETCH_FIRST_USER, tutte le chiamate successive a **SQLDataSources** con *direzione* impostato su SQL_FETCH_NEXT restituire solo i DSN utente. Quando *direzione* è impostata su SQL_FETCH_FIRST_SYSTEM, tutte le chiamate successive a **SQLDataSources** con *direzione* impostato su SQL_FETCH_NEXT restituire solo i DSN di sistema.  
  
 *ServerName*  
 [Output] Puntatore a un buffer in cui restituire il nome dell'origine dati.  
  
 Se *ServerName* sia impostato su NULL *NameLength1Ptr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui fa riferimento *ServerName*.  
  
 *BufferLength1*  
 [Input] Lunghezza del **ServerName* memorizzare nel buffer, in caratteri; ciò non è necessario superare SQL_MAX_DSN_LENGTH più il carattere di terminazione null.  
  
 *NameLength1Ptr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per restituire \* *ServerName*. Se il numero di caratteri disponibili da restituire è maggiore o uguale a *BufferLength1*, il nome dell'origine dati in \* *ServerName* viene troncato a *BufferLength1* meno la lunghezza di un carattere di terminazione null.  
  
 *Descrizione*  
 [Output] Puntatore a un buffer in cui restituire la descrizione del driver associato all'origine dati. Ad esempio, file dBASE o SQL Server.  
  
 Se *Description* sia impostato su NULL *NameLength2Ptr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui fa riferimento *Descrizione*.  
  
 *BufferLength2*  
 [Input] Lunghezza in caratteri del **descrizione* buffer.  
  
 *NameLength2Ptr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per restituire \* *descrizione*. Se il numero di caratteri disponibili da restituire è maggiore o uguale a *BufferLength2*, la descrizione di driver in \* *descrizione* viene troncato a *BufferLength2*  meno la lunghezza di un carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDataSources** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType*SQL_HANDLE_ENV e una *gestiscono* dei *EnvironmentHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLDataSources** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|(DM) messaggio informativo di gestione Driver specifico. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|(DM) il buffer \* *ServerName* non era sufficientemente grande per restituire il nome dell'origine dati completa. Pertanto, il nome è stato troncato. Viene restituita la lunghezza del nome dell'origine dati intera \* *NameLength1Ptr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).<br /><br /> (DM) il buffer \* *descrizione* non era sufficientemente grande per restituire la descrizione completa del driver. Pertanto, la descrizione sono stata troncata. Viene restituita la lunghezza della descrizione dell'origine dati non troncato **NameLength2Ptr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|HY000|Errore generale|(DM) di un errore per cui si è verificato alcun errore SQLSTATE specifico per il quale è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|(DM) The Driver Manager: Impossibile allocare la memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato per l'argomento *BufferLength1* era minore di 0.<br /><br /> (DM) il valore specificato per l'argomento *BufferLength2* era minore di 0.|  
|HY103|Codice di recupero non valido|(DM) il valore specificato per l'argomento *direzione* non è uguale a SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM o SQL_FETCH_NEXT.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Commenti  
 In quanto **SQLDataSources** viene implementato in Gestione Driver, è supportata per tutti i driver indipendentemente dalla conformità agli standard di un driver specifico.  
  
 Un'applicazione può chiamare **SQLDataSources** più volte per recuperare tutti i nomi delle origini dati. Gestione Driver recupera queste informazioni dalle informazioni di sistema. Quando non sono presenti più nomi di origine dati, gestione Driver restituisce SQL_NO_DATA. Se **SQLDataSources** viene chiamato con SQL_FETCH_NEXT immediatamente dopo che viene restituito SQL_NO_DATA, verrà restituito il primo nome dell'origine dati. Per informazioni su come un'applicazione usa le informazioni restituite da **SQLDataSources**, vedere [scegliere un'origine dati o Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se viene passato SQL_FETCH_NEXT **SQLDataSources** la prima volta che viene chiamato, verrà restituito il primo nome dell'origine dati.  
  
 Il driver determina la modalità di mapping dei nomi delle origini dati alle origini dei dati effettivi.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|L'individuazione e visualizzazione di un elenco i valori necessari per connettersi a un'origine dati|[Funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|La connessione a un'origine dati tramite una finestra di dialogo o stringa di connessione|[Funzione SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Restituzione di attributi e le descrizioni di driver|[Funzione SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
