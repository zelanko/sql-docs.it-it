---
title: Funzione SQLInstallTranslatorEx | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57a2fb53226af9aeb6e546f6109a3e182ffc754f
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536562"
---
# <a name="sqlinstalltranslatorex-function"></a>Funzione SQLInstallTranslatorEx
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLInstallTranslatorEx** aggiunge informazioni su una funzione di conversione per la sezione Odbcinst. ini delle informazioni di sistema (HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC traduttori chiave Registro di sistema).  
  
 La funzionalità del **SQLInstallTranslatorEx** sono accessibili anche con [ODBCCONF. File EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [Input] Questo deve contenere un elenco di coppie parola chiave / valore che indica il traduttore doppia terminazione null. Per altre informazioni sulla sintassi di coppia valore-parola chiave, vedere [sottochiavi di specifica di Microsoft Translator](../../../odbc/reference/install/translator-specification-subkeys.md).  
  
 Il **traduttore** e **il programma di installazione** parole chiave devono essere incluso nel *lpszTranslator* stringa. La traduzione DLL sia elencata con il **traduttore** parola chiave e il programma di installazione di Microsoft translator DLL sia elencata con il **il programma di installazione** (parola chiave). Ogni coppia viene terminata con un byte NULL e l'intero elenco viene terminata con un byte NULL. (Vale a dire, due byte NULL contrassegnano la fine dell'elenco.) Il formato del *lpszTranslator* è come segue:  
  
 \0Translator=*traduttore-DLL-filename*\0[Setup=*il programma di installazione-DLL-filename*\0]\0  
  
 *lpszPathIn*  
 [Input] Percorso completo di in cui la funzione di conversione deve essere installato o un puntatore null. Se *lpszPath* è un puntatore null, i traduttori verranno installati nella directory di sistema.  
  
 *lpszPathOut*  
 [Output] Percorso della directory di destinazione in cui la funzione di conversione deve essere installato. Se la funzione di conversione non è mai stato installato, *lpszPathOut* equivale a *lpszPathIn*. Se è presente un'installazione precedente del traduttore *lpszPathOut* è il percorso dell'installazione precedente.  
  
 *cbPathOutMax*  
 [Input] Lunghezza di *lpszPathOut.*  
  
 *pcbPathOut*  
 [Output] Numero totale di byte disponibili per restituire *lpszPathOut*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbPathOutMax*, il percorso di output in *lpszPathOut* verrà troncato *pcbPathOutMax* meno di carattere di terminazione null. Il *pcbPathOut* argomento può essere un puntatore null.  
  
 *fRequest*  
 [Input] Tipo di richiesta. *trattano* deve contenere uno dei valori seguenti:  
  
 ODBC_INSTALL_INQUIRY: Richiedere informazioni su dove può essere installato uno strumento di conversione.  
  
 ODBC_INSTALL_COMPLETE: Completare la richiesta di installazione.  
  
 *lpdwUsageCount*  
 [Output] Il conteggio di utilizzo del convertitore dopo la chiamata a questa funzione.  
  
 Le applicazioni non devono impostare il conteggio di utilizzo. ODBC manterrà questo conteggio.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLInstallTranslatorEx** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza del buffer non valido|Il *lpszPathOut* argomento non era sufficientemente grande da contenere il percorso di output. Il buffer contiene il percorso troncato.<br /><br /> Il *cbPathOutMax* argomento era 0 e il *trattano* argomento era ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|Il *trattano* argomento non è uno dei seguenti:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave / valore non valido|Il *lpszTranslator* argomento contiene un errore di sintassi.|  
|ODBC_ERROR_INVALID_PATH|Percorso di installazione non è valido|Il *lpszPathIn* argomento contiene un percorso non valido.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequenza di parametri non validi|Il *lpszTranslator* argomento non contiene un elenco di coppie parola chiave / valore.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Non è stato possibile incrementare o decrementare conteggio di utilizzo di componente del Registro di sistema|Il programma di installazione non riuscita a incrementare il conteggio di utilizzo della funzione di conversione.|  
  
## <a name="comments"></a>Commenti  
 **SQLInstallTranslatorEx** fornisce un meccanismo per installare solo la funzione di conversione. Questa funzione non copia effettivamente tutti i file. Il programma chiama è responsabile per copiare i file di Microsoft translator.  
  
 **SQLInstallTranslatorEx** incrementa il conteggio di utilizzo del componente per il translator installati di 1. Se esiste già una versione del convertitore, ma il conteggio di utilizzo del componente per la funzione di conversione non esiste, il nuovo valore di conteggio dell'utilizzo di componente è impostato su 2.  
  
 Il programma di installazione dell'applicazione è responsabile per copiare fisicamente il file di Microsoft translator e mantenere il conteggio di utilizzo di file. Se il file di traduzione non è stato precedentemente installato, il programma di installazione dell'applicazione deve copiare i file e creare i file conteggio di utilizzo. Se il file è stato precedentemente installato, il programma di installazione viene semplicemente incrementato il conteggio di utilizzo di file.  
  
 Se in precedenza è stata installata una versione precedente del convertitore dall'applicazione, la funzione di conversione deve disinstallare e reinstallare, in modo che il conteggio di utilizzo del componente Microsoft translator è valido. **SQLRemoveTranslator** deve essere chiamato per diminuire il conteggio di utilizzo del componente, quindi **SQLInstallTranslatorEx** deve essere chiamato per incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione è necessario sostituire il vecchio file o i file con il nuovo file. Il conteggio di utilizzo file rimarranno invariati e altre applicazioni che utilizzavano il file versione precedenti useranno la versione più recente.  
  
 La lunghezza del percorso nella *lpszPathOut* nelle **SQLInstallTranslatorEx** consente un processo di installazione in due fasi, in modo che un'applicazione può determinare che cosa *cbPathOutMax* deve essere chiamando **SQLInstallTranslatorEx** con un *trattano* della modalità ODBC_INSTALL_INQUIRY. Verrà restituito il numero totale di byte disponibili nel *pcbPathOut* buffer. **SQLInstallTranslatorEx** può quindi essere chiamato con un *trattano* di ODBC_INSTALL_COMPLETE e il *cbPathOutMax* argomento impostato sul valore di *pcbPathOut* buffer, più il carattere di terminazione null.  
  
 Se si sceglie di non utilizzare il modello in due fasi per **SQLInstallTranslatorEx**, è necessario impostare *cbPathOutMax*, che definisce le dimensioni della risorsa di archiviazione per il percorso della directory di destinazione, per il valore di MAX_PATH valore, come definito in STDLIB. h, per evitare il troncamento.  
  
 Quando *trattano* ODBC_INSTALL_COMPLETE, viene **SQLInstallTranslatorEx** nepovoluje hodnotu *lpszPathOut* null (o *cbPathOutMax* da 0). Se *trattano* è ODBC_INSTALL_COMPLETE, viene restituito FALSE quando il numero di byte disponibili da restituire è maggiore o uguale a *cbPathOutMax*, fornendo il risultato se il troncamento si verifica.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Restituzione di un'opzione di conversione predefinita|[ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)|  
|Selezione di funzioni di conversione|[SQLGetTranslator](../../../odbc/reference/syntax/sqlgettranslator-function.md)|  
|Rimozione di funzioni di conversione|[SQLRemoveTranslator](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|
