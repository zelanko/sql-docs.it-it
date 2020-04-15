---
title: 'Funzione SQLDrivers : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDrivers
helpviewer_keywords:
- SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2496e7cd5f2abe0831c72484bed374d7aa1513ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302762"
---
# <a name="sqldrivers-function"></a>Funzione SQLDrivers
**Conformità**  
 Versione introdotta: ODBC 2.0 Standards Compliance: ODBC  
  
 **Riepilogo**  
 **SQLDrivers** elenca le descrizioni dei driver e le parole chiave degli attributi del driver. Questa funzione viene implementata solo da Gestione Driver.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>Argomenti  
 *EnvironmentHandle*  
 [Ingresso] Maniglia dell'ambiente.  
  
 *Direzione*  
 [Ingresso] Determina se Gestione Driver recupera la descrizione del driver successivo nell'elenco (SQL_FETCH_NEXT) o se la ricerca inizia dall'inizio dell'elenco (SQL_FETCH_FIRST).  
  
 *DriverDescription*  
 [Uscita] Puntatore a un buffer in cui restituire la descrizione del driver.  
  
 Se *DriverDescription* è NULL, *DescriptionLengthPtr* restituirà comunque il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *DriverDescription*.  
  
 *BufferLength1*  
 [Ingresso] Lunghezza del buffer*Di tipo DriverDescription,* in caratteri.  
  
 *DescriptionLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per la restituzione in \* *DriverDescription*. Se il numero di caratteri disponibili per la restituzione è maggiore \*o uguale a *BufferLength1*, la descrizione del driver in *DriverDescription* viene troncata a *BufferLength1* meno la lunghezza di un carattere di terminazione null.  
  
 *DriverAttributi*  
 [Uscita] Puntatore a un buffer in cui restituire l'elenco di coppie di valori di attributo driver (vedere "Commenti").  
  
 Se *DriverAttributes* è NULL, *AttributesLengthPtr* restituirà comunque il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile per la restituzione nel buffer a cui punta *DriverAttributes*.  
  
 *BufferLength2*  
 [Ingresso] Lunghezza del \*buffer *DriverAttributes,* in caratteri. Se * \*il DriverDescription* valore è una stringa Unicode (quando si chiama **SQLDriversW**), il *BufferLength* argomento deve essere un numero pari.  
  
 *AttributesLengthPtr*  
 [Uscita] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il byte di terminazione null) disponibile per la restituzione in \* *DriverAttributes*. Se il numero di byte disponibili da restituire è maggiore o uguale \*a *BufferLength2*, l'elenco delle coppie di valori di attributo in *DriverAttributes* viene troncato a *BufferLength2* meno la lunghezza del carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDrivers** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, è possibile ottenere un valore SQLSTATE associato chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_ENV e un *handle* di *EnvironmentHandle*. Nella tabella seguente sono elencati i valori SQLSTATE in genere restituiti da **SQLDrivers** e ognuno di essi viene illustrato nel contesto di questa funzione. la notazione "(DM)" precede le descrizioni di SQLSTATEs restituite da Gestione Driver. Il codice restituito associato a ogni valore SQLSTATE viene SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avvertenza generale|(DM) messaggio informativo specifico di Gestione Driver. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|01004|Dati stringa troncati a destra|(DM) il \*buffer *DriverDescription* non era sufficientemente grande per restituire la descrizione completa del driver. Pertanto, la descrizione è stata troncata. La lunghezza della descrizione completa del \*driver viene restituita in *DescriptionLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) il \*buffer *DriverAttributes* non era sufficientemente grande per restituire l'elenco completo delle coppie di valori di attributo. Pertanto, l'elenco è stato troncato. La lunghezza dell'elenco non troncato di coppie di valori di attributo viene restituita in :*AttributesLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO.)|  
|HY000|Errore generale:|Si è verificato un errore per il quale non è stato definito alcun SQLSTATE specifico e per il quale non è stato definito alcun SQLSTATE specifico dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel buffer * \*MessageText* descrive l'errore e la relativa causa.|  
|I001|Errore di allocazione della memoria|(DM) Gestione Driver non è stato in grado di allocare la memoria necessaria per supportare l'esecuzione o il completamento della funzione.|  
|HY010 (Informazioni in stati incomMIino in|Errore della sequenza di funzioni|(DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** è stato chiamato per *il StatementHandle* e restituito SQL_PARAM_DATA_AVAILABLE. Questa funzione è stata chiamata prima del recupero dei dati per tutti i parametri trasmessi.|  
|HY013|Errore di gestione della memoria|Impossibile elaborare la chiamata di funzione perché non è stato possibile accedere agli oggetti di memoria sottostante, probabilmente a causa di condizioni di memoria insufficiente.|  
|I090|Stringa o lunghezza del buffer non valida|(DM) il valore specificato per l'argomento *BufferLength1* è minore di 0.<br /><br /> (DM) il valore specificato per l'argomento *BufferLength2* è minore di 0 o uguale a 1.|  
|I103|Codice di recupero non valido|(DM) il valore specificato per l'argomento *Direzione* non è uguale a SQL_FETCH_FIRST o SQL_FETCH_NEXT.|  
|HY117|La connessione è sospesa a causa di uno stato di transazione sconosciuto. Sono consentite solo funzioni di disconnessione e di sola lettura.|(DM) Per ulteriori informazioni sullo stato sospeso, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Commenti  
 **SQLDrivers** restituisce la \*descrizione del driver nel Buffer *DriverDescription.* Restituisce informazioni aggiuntive sul \*driver nel buffer *DriverAttributes* come un elenco di coppie parola chiave-valore. Tutte le parole chiave elencate nelle informazioni di sistema per i driver verranno restituite per tutti i driver, ad eccezione di **CreateDSN**, che viene utilizzato per richiedere la creazione di origini dati e pertanto è facoltativo. Ogni coppia viene terminata con un byte null e l'elenco completo viene terminato con un byte null (ovvero, due byte null contrassegnano la fine dell'elenco). Ad esempio, un driver basato su file che utilizza la sintassi C potrebbe restituire il seguente elenco di attributi (Sezione 0" rappresenta un carattere null):  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 Se \* *DriverAttributes* non è sufficientemente grande per contenere l'intero elenco, l'elenco viene troncato, **SQLDrivers** restituisce SQLSTATE 01004 (dati troncati) e la lunghezza dell'elenco (escluso il byte di terminazione null finale) viene restituita in *, AttributesLengthPtr*.  
  
 Le parole chiave degli attributi del driver vengono aggiunte dalle informazioni di sistema quando viene installato il driver. Per ulteriori informazioni, vedere [Installazione di componenti ODBC](../../../odbc/reference/install/installing-odbc-components.md).  
  
 Un'applicazione può chiamare **SQLDrivers** più volte per recuperare tutte le descrizioni dei driver. Gestione Driver recupera queste informazioni dalle informazioni di sistema. Quando non sono presenti altre descrizioni dei driver, **SQLDrivers** restituisce SQL_NO_DATA. Se **SQLDrivers** viene chiamato con SQL_FETCH_NEXT immediatamente dopo restituisce SQL_NO_DATA, restituisce la prima descrizione del driver. Per informazioni sull'utilizzo delle informazioni restituite da **SQLDrivers**da SQLDrivers da parte di un'applicazione , vedere [Scelta di un'origine dati o di un driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se SQL_FETCH_NEXT viene passato a **SQLDrivers** la prima volta che viene chiamato, **SQLDrivers** restituisce il primo nome dell'origine dati.  
  
 Poiché **SQLDrivers** è implementato in Gestione Driver, è supportato per tutti i driver indipendentemente dalla conformità agli standard di un driver specifico.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Individuazione ed elenco dei valori necessari per connettersi a un'origine dati|[Funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnectSQLConnect Function](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Restituzione di nomi di origini datiReturning data source names|[Funzione SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|Connessione a un'origine dati tramite una stringa di connessione o una finestra di dialogoConnecting to a data source using a connection string or dialog box|[SQLDriverConnect Function](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento all'API ODBCODBC API Reference](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
