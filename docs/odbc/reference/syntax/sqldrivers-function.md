---
title: Funzione SQLDrivers | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 181d3aea0b2c756abc0dc603348cc9cfd728ac4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538158"
---
# <a name="sqldrivers-function"></a>Funzione SQLDrivers
**Conformità**  
 Versione introdotta: Conformità agli standard 2.0 ODBC: ODBC  
  
 **Riepilogo**  
 **SQLDrivers** Elenca le descrizioni di driver e parole chiave di attributo del driver. Questa funzione è implementata solo da Gestione Driver.  
  
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
 [Input] Handle di ambiente.  
  
 *Direzione*  
 [Input] Determina se il Driver Manager recupera la descrizione del driver successiva dell'elenco (SQL_FETCH_NEXT) o se viene avviata la ricerca dall'inizio dell'elenco (SQL_FETCH_FIRST).  
  
 *DriverDescription*  
 [Output] Puntatore a un buffer in cui restituire la descrizione del driver.  
  
 Se *DriverDescription* sia impostato su NULL *DescriptionLengthPtr* continuerà a restituire il numero totale di caratteri (escluso il carattere di terminazione null per i dati di tipo carattere) disponibili per restituire il buffer a cui punta *DriverDescription*.  
  
 *BufferLength1*  
 [Input] Lunghezza di **DriverDescription* buffer, in caratteri.  
  
 *DescriptionLengthPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di caratteri (escluso il carattere di terminazione null) disponibili per restituire \* *DriverDescription*. Se il numero di caratteri disponibili da restituire è maggiore o uguale a *BufferLength1*, la descrizione di driver in \* *DriverDescription* viene troncato a  *BufferLength1* meno la lunghezza di un carattere di terminazione null.  
  
 *DriverAttributes*  
 [Output] Puntatore a un buffer in cui restituire l'elenco di coppie di valore dell'attributo del driver (vedere "Commenti").  
  
 Se *DriverAttributes* sia impostato su NULL *AttributesLengthPtr* continuerà a restituire il numero totale di byte (escluso il carattere di terminazione null per i dati di tipo carattere) disponibile da restituire nel buffer a cui punta *DriverAttributes*.  
  
 *BufferLength2*  
 [Input] Lunghezza del \* *DriverAttributes* buffer, in caratteri. Se il  *\*DriverDescription* valore è una stringa Unicode (quando si chiama **SQLDriversW**), il *BufferLength* argomento deve essere un numero pari.  
  
 *AttributesLengthPtr*  
 [Output] Puntatore a un buffer in cui restituire il numero totale di byte (escluso il byte di terminazione null) disponibili per restituire \* *DriverAttributes*. Se il numero di byte disponibili da restituire è maggiore o uguale a *BufferLength2*, l'elenco di coppie di valore di attributo nella \* *DriverAttributes* viene troncato a  *BufferLength2* meno la lunghezza del carattere di terminazione null.  
  
## <a name="returns"></a>Valori di codice restituiti  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLDrivers** restituisce SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valore SQLSTATE associato può essere ottenuto chiamando **SQLGetDiagRec** con un *HandleType* di SQL_HANDLE_ENV e un *gestiscono* dei *EnvironmentHandle*. Nella tabella seguente sono elencati i valori SQLSTATE normalmente restituiti dal **SQLDrivers** e illustra ognuna nel contesto di questa funzione; la notazione "(DM)" precede le descrizioni di SQLSTATE restituiti da Gestione Driver. Il codice restituito a ogni valore SQLSTATE è SQL_ERROR, se non specificato diversamente.  
  
|SQLSTATE|Errore|Descrizione|  
|--------------|-----------|-----------------|  
|01000|Avviso generale|(DM) messaggio informativo di gestione Driver specifico. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|01004|Stringa troncati di dati a destra|(DM) il buffer \* *DriverDescription* non era sufficientemente grande per restituire la descrizione completa del driver. Pertanto, la descrizione sono stata troncata. Viene restituita la lunghezza della descrizione del driver completo nella \* *DescriptionLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).<br /><br /> (DM) il buffer \* *DriverAttributes* non era sufficientemente grande per restituire l'elenco completo delle coppie di valore di attributo. Pertanto, l'elenco è stato troncato. Viene restituita la lunghezza dell'elenco di coppie valore dell'attributo non troncato **AttributesLengthPtr*. (Funzione restituisce SQL_SUCCESS_WITH_INFO).|  
|HY000|Errore generale|Si è verificato un errore per cui si è verificato alcun errore SQLSTATE specifico e per cui è stato definito alcun SQLSTATE specifici dell'implementazione. Il messaggio di errore restituito da **SQLGetDiagRec** nel  *\*MessageText* buffer viene descritto l'errore e la relativa causa.|  
|HY001|Errore di allocazione della memoria|(DM) The Driver Manager: Impossibile allocare la memoria che è necessario per supportare l'esecuzione o il completamento della funzione.|  
|HY010|Errore nella sequenza della funzione|(DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** è stato chiamato per il *StatementHandle* e restituito SQL_PARAM_DATA_ È DISPONIBILE. Questa funzione è stata chiamata prima per tutti i parametri trasmessi sono stati recuperati i dati.|  
|HY013|Errore di gestione della memoria|La chiamata di funzione non è stato possibile elaborare perché gli oggetti di memoria sottostante non sono accessibile, probabilmente a causa di condizioni di memoria insufficiente.|  
|HY090|Lunghezza della stringa o buffer non valido|(DM) il valore specificato per l'argomento *BufferLength1* era minore di 0.<br /><br /> (DM) il valore specificato per l'argomento *BufferLength2* era minore di 0 o uguale a 1.|  
|HY103|Codice di recupero non valido|(DM) il valore specificato per l'argomento *direzione* non è uguale a SQL_FETCH_FIRST o SQL_FETCH_NEXT.|  
|HY117|Connessione viene sospesa a causa dello stato di transazione sconosciuto. Solo disconnettere e le funzioni di sola lettura sono consentite.|(DM) per altre informazioni sullo stato sospeso, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Commenti  
 **SQLDrivers** restituisce la descrizione del driver nel \* *DriverDescription* buffer. Restituisce informazioni aggiuntive sul driver nel \* *DriverAttributes* buffer come un elenco di coppie parola chiave / valore. Tutte le parole chiave elencate nelle informazioni di sistema per i driver verranno restituiti per tutti i driver, ad eccezione di **CreateDSN**, che viene usato per richiedere la creazione di origini dati e pertanto è facoltativo. Ogni coppia viene terminata con un byte null e l'elenco completo è terminata con un byte null (vale a dire, due byte null contrassegnano la fine dell'elenco). Ad esempio, un driver basati su file usando la sintassi C potrebbe restituire l'elenco seguente di attributi ("\0" rappresenta un carattere null):  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 Se \* *DriverAttributes* è non sufficientemente grande da contenere l'elenco completo, l'elenco viene troncato, **SQLDrivers** restituisce SQLSTATE 01004 (dati troncati) e la lunghezza dell'elenco (escluse le byte finale di terminazione null) viene restituito in **AttributesLengthPtr*.  
  
 Parole chiave di attributo del driver vengono aggiunti dalle informazioni di sistema quando il driver è installato. Per altre informazioni, vedere [installazione dei componenti ODBC](../../../odbc/reference/install/installing-odbc-components.md).  
  
 Un'applicazione può chiamare **SQLDrivers** più volte per recuperare tutte le descrizioni dei driver. Gestione Driver recupera queste informazioni dalle informazioni di sistema. Quando non sono presenti alcun più descrizioni dei driver, **SQLDrivers** restituisce SQL_NO_DATA. Se **SQLDrivers** viene chiamato con SQL_FETCH_NEXT immediatamente dopo che viene restituito SQL_NO_DATA, restituisce la descrizione del driver prima. Per informazioni su come un'applicazione usa le informazioni restituite da **SQLDrivers**, vedere [scegliere un'origine dati o Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Se viene passato SQL_FETCH_NEXT **SQLDrivers** la prima volta che viene chiamato, **SQLDrivers** restituisce il primo nome dell'origine dati.  
  
 In quanto **SQLDrivers** viene implementato in Gestione Driver, è supportata per tutti i driver indipendentemente dalla conformità agli standard di un driver specifico.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|L'individuazione e visualizzazione di un elenco i valori necessari per connettersi a un'origine dati|[Funzione SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Connessione a un'origine dati|[Funzione SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Restituzione di nomi delle origini dati|[Funzione SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|La connessione a un'origine dati tramite una finestra di dialogo o stringa di connessione|[Funzione SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Riferimento all'API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [File di intestazione ODBC](../../../odbc/reference/install/odbc-header-files.md)
