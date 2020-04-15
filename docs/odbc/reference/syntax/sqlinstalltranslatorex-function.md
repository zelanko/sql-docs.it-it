---
title: Funzione SQLInstallTranslatorEx . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallTranslatorEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallTranslatorEx
helpviewer_keywords:
- SQLInstallTranslatorEx function [ODBC]
ms.assetid: a0630602-53c1-4db0-98ce-70d160aedf8d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5cf52c26bf9e4a26f13a27a0e763fbaa30bd18ec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302092"
---
# <a name="sqlinstalltranslatorex-function"></a>Funzione SQLInstallTranslatorEx
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLInstallTranslatorEx** aggiunge informazioni su un traduttore alla sezione Odbcinst.ini delle informazioni di sistema (HKEY_LOCAL_MACHINE . inI-ODBC Translators (chiave del Registro di sistema) ).  
  
 La funzionalità di **SQLInstallTranslatorEx** è accessibile anche con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLInstallTranslatorEx(  
     LPCSTR    lpszTranslator,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszTranslator*  
 [Ingresso] Deve contenere un elenco doppiamente con terminazione null di coppie parola chiave-valore che descrivono il traduttore. Per ulteriori informazioni sulla sintassi delle coppie parola chiave-valore, consultate [Sottochiavi delle specifiche del traduttore](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 Le parole chiave **Translator** e **Setup** devono essere incluse nella stringa *lpszTranslator.* La DLL di conversione è elencata con la parola chiave **Translator** e la DLL di installazione del convertitore viene elencata con la parola chiave **Setup.** Ogni coppia viene terminata con un byte NULL e l'intero elenco viene terminato con un byte NULL. (Ovvero, due byte NULL segnano la fine dell'elenco.) Il formato di *lpszTranslator* è il seguente:  
  
 *Traduttore-nomefile DLL*0 [Setup-Nome-DLL-0]*setup-DLL-filename*  
  
 *lpszPathIn (informazioni in questo stati in due)*  
 [Ingresso] Percorso completo del punto in cui deve essere installato il traduttore o un puntatore null. Se *lpszPath* è un puntatore null, i traduttori verranno installati nella directory di sistema.  
  
 *lpszPathOut (informazioni in base a un'autorizzazione a*  
 [Uscita] Percorso della directory di destinazione in cui deve essere installato il traduttore. Se il traduttore non è mai stato installato, *lpszPathOut* è uguale a *lpszPathIn*. Se esiste un'installazione precedente del traduttore, *lpszPathOut* è il percorso dell'installazione precedente.  
  
 *cbPathOutMax*  
 [Ingresso] Lunghezza di *lpszPathOut.*  
  
 *pcbPathOut (informazioni in questo modo in stato di insta*  
 [Uscita] Numero totale di byte disponibili da restituire in *lpszPathOut*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbPathOutMax*, il percorso di output in *lpszPathOut* viene troncato a *pcbPathOutMax* meno il carattere di terminazione null. L'argomento *pcbPathOut* può essere un puntatore null.  
  
 *fRichiesta*  
 [Ingresso] Tipo di richiesta. *fRequest* deve contenere uno dei seguenti valori:  
  
 ODBC_INSTALL_INQUIRY: Informarsi su dove può essere installato un traduttore.  
  
 ODBC_INSTALL_COMPLETE: completare la richiesta di installazione.  
  
 *lpdwUsageCount (conteggio informazioni in lingua lingua instato)*  
 [Uscita] Conteggio di utilizzo del traduttore dopo la chiamata a questa funzione.  
  
 Le applicazioni non devono impostare il conteggio di utilizzo. ODBC manterrà questo conteggio.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLInstallTranslatorEx** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza buffer non valida|L'argomento *lpszPathOut* non è sufficientemente grande per contenere il percorso di output. Il buffer contiene il percorso troncato.<br /><br /> L'argomento *cbPathOutMax* era 0 e l'argomento *fRequest* è stato ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|L'argomento *fRequest* non è uno dei seguenti:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave-valore non valide|L'argomento *lpszTranslator* contiene un errore di sintassi.|  
|ODBC_ERROR_INVALID_PATH|Percorso di installazione non valido|L'argomento *lpszPathIn* contiene un percorso non valido.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequenza di parametri non valida|L'argomento *lpszTranslator* non contiene un elenco di coppie parola chiave-valore.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Impossibile incrementare o diminuire il conteggio di utilizzo dei componenti del Registro di sistema|Il programma di installazione non è riuscito a incrementare il conteggio di utilizzo del convertitore.|  
  
## <a name="comments"></a>Commenti  
 **SQLInstallTranslatorEx** fornisce un meccanismo per installare solo il traduttore. Questa funzione non copia effettivamente alcun file. Il programma chiamante è responsabile della copia dei file del traduttore.  
  
 **SQLInstallTranslatorEx** incrementa di 1 il conteggio di utilizzo del componente per il convertitore installato. Se esiste già una versione del traduttore ma il conteggio di utilizzo del componente per il traduttore non esiste, il nuovo valore del conteggio di utilizzo del componente è impostato su 2.  
  
 Il programma di installazione dell'applicazione è responsabile della copia fisica del file del traduttore e della gestione del conteggio di utilizzo dei file. Se il file del convertitore non è stato installato in precedenza, il programma di installazione dell'applicazione deve copiare il file o i file e creare il conteggio di utilizzo dei file o dei file. Se il file è stato installato in precedenza, il programma di installazione incrementa semplicemente il conteggio di utilizzo del file.  
  
 Se una versione precedente del traduttore è stata installata in precedenza dall'applicazione, il traduttore deve essere disinstallato e quindi reinstallato, in modo che il conteggio dell'utilizzo del componente del traduttore sia valido. **SQLRemoveTranslator** deve essere chiamato per diminuire il conteggio di utilizzo del componente e quindi **SQLInstallTranslatorEx** deve essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione deve sostituire il vecchio file o i file con il nuovo file. Il conteggio di utilizzo del file rimarrà invariato e le altre applicazioni che hanno utilizzato il file della versione precedente utilizzeranno ora la versione più recente.  
  
 La lunghezza del percorso in *lpszPathOut* in **SQLInstallTranslatorEx** consente un processo di installazione a due fasi, pertanto un'applicazione può determinare quale *cbPathOutMax* deve essere chiamando **SQLInstallTranslatorEx** con *una richiesta di* ODBC_INSTALL_INQUIRY modalità. Verrà restituito il numero totale di byte disponibili nel buffer *pcbPathOut.* **SQLInstallTranslatorEx** può quindi essere chiamato con *una richiesta* di ODBC_INSTALL_COMPLETE e l'argomento *cbPathOutMax* impostato sul valore nel buffer *pcbPathOut,* più il carattere di terminazione null.  
  
 Se si sceglie di non utilizzare il modello a due fasi per **SQLInstallTranslatorEx**, è necessario impostare *cbPathOutMax*, che definisce la dimensione dell'archiviazione per il percorso della directory di destinazione, sul valore _MAX_PATH, come definito in Stdlib.h, per impedire il troncamento.  
  
 Quando *fRequest* è ODBC_INSTALL_COMPLETE, **SQLInstallTranslatorEx** non consente a *lpszPathOut* di essere NULL (o *cbPathOutMax* 0). Se *fRequest* è ODBC_INSTALL_COMPLETE, VIENE restituito FALSE quando il numero di byte disponibili da restituire è maggiore o uguale a *cbPathOutMax*, con il risultato che si verifica il troncamento.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione di un'opzione di conversione predefinita|[Traduttore di configurazione](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Selezione dei traduttori|[SQLGetTranslator (Traduttore)](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Rimozione dei traduttori|[SQLRemoveTranslator (TraduttorediSQLRemoveTranslator)](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
