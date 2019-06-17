---
title: Funzione SQLInstallDriverEx | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5664a4cb745a250aa8db6d98b92a275bb91c7a8d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536574"
---
# <a name="sqlinstalldriverex-function"></a>Funzione SQLInstallDriverEx
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLInstallDriverEx** aggiunge informazioni sul driver per la voce di Odbcinst. ini nelle informazioni di sistema e incrementa il driver *UsageCount* di 1. Tuttavia, se una versione del driver esiste già ma il *UsageCount* valore dell'indicatore per il driver non esiste, il nuovo *UsageCount* valore è impostato su 2.  
  
 Questa funzione non copia effettivamente tutti i file. È responsabilità del programma chiamante per copiare i file del driver nella directory di destinazione in modo corretto.  
  
 La funzionalità del **SQLInstallDriverEx** sono accessibili anche con [ODBCCONF. File EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argomenti  
 *lpszDriver*  
 [Input] Descrizione del driver (in genere il nome del sistema DBMS associati) presentata agli utenti anziché il nome del driver fisico. Il *lpszDriver* argomento deve contenere un elenco di coppie parola chiave / valore che descrivono i driver doppia terminazione null. Per altre informazioni sulle coppie parola chiave / valore, vedere [sottochiavi di specifica di Driver](../../../odbc/reference/install/driver-specification-subkeys.md). Per altre informazioni sulla stringa di terminazione null, vedere [funzione ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 [Input] Percorso completo della directory di destinazione dell'installazione, o un puntatore null. Se *lpszPathIn* è un puntatore null, il driver verranno installati nella directory di sistema.  
  
 *lpszPathOut*  
 [Output] Percorso della directory di destinazione in cui deve essere installato il driver. Se il driver non è stato precedentemente installato, *lpszPathOut* deve essere identico *lpszPathIn*. Se il driver è stato installato in precedenza, *lpszPathOut* è il percorso dell'installazione precedente.  
  
 *cbPathOutMax*  
 [Input] Lunghezza di *lpszPathOut*.  
  
 *pcbPathOut*  
 [Output] Numero totale di byte (escluso il carattere di terminazione null) disponibili per restituire *lpszPathOut*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbPathOutMax*, il percorso di output in *lpszPathOut* verrà troncato *cbPathOutMax* meno di carattere di terminazione null. Il *pcbPathOut* argomento può essere un puntatore null.  
  
 *fRequest*  
 [Input] Tipo di richiesta. Il *trattano* argomento deve essere uno dei valori seguenti:  
  
 ODBC_INSTALL_INQUIRY: Richiedere informazioni su dove può essere installato un driver.  
  
 ODBC_INSTALL_COMPLETE: Completare la richiesta di installazione.  
  
 *lpdwUsageCount*  
 [Output] Il conteggio di utilizzo del driver dopo la chiamata a questa funzione.  
  
 Le applicazioni non devono impostare il conteggio di utilizzo. ODBC manterrà questo conteggio.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE in caso di errore.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLInstallDriverEx** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza del buffer non valido|Il *lpszPathOut* argomento non era sufficientemente grande da contenere il percorso di output. Il buffer contiene il percorso troncato.<br /><br /> Il *cbPathOutMax* argomento era 0, e *trattano* era ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|Il *trattano* argomento non è uno dei seguenti:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave / valore non valido|Il *lpszDriver* argomento contiene un errore di sintassi.|  
|ODBC_ERROR_INVALID_PATH|Percorso di installazione non è valido|Il *lpszPathIn* argomento contiene un percorso non valido.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Non è riuscito a caricare la libreria di programma di installazione driver o del convertitore.|Non è stato possibile caricare la libreria dell'installazione di driver.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequenza di parametri non validi|Il *lpszDriver* argomento non contiene un elenco di coppie parola chiave / valore.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Non è stato possibile incrementare o decrementare il conteggio di utilizzo del componente|Il programma di installazione non riuscita a incrementare il conteggio di utilizzo del driver.|  
  
## <a name="comments"></a>Commenti  
 Il *lpszDriver* argomento è un elenco di attributi in forma di coppie parola chiave / valore. Ogni coppia viene terminata con un byte null e l'intero elenco viene terminata con un byte null. (Vale a dire, due byte null contrassegnano la fine dell'elenco.) Il formato di questo elenco è come segue:  
  
 _driver desc_ **\\** 0Driver **=** _driver-DLL-filename_ **\\** 0 [programma di installazione **=** _programma di installazione-DLL-filename_<b>\\</b>0]  
  
 [_driver-attr-keyword1_ **=** _value1_<b>\\</b>0][_driver-attr-keyword2_ **=** _value2_<b>\\</b>0]...<b>\\</b>0  
  
 dove \0 è un byte null e *driver-attr-keywordn* è qualsiasi parola chiave degli attributi del driver. Le parole chiave devono essere visualizzato nell'ordine specificato. Ad esempio, si supponga che un driver per i file di testo formattato dispone di driver separato e file DLL di installazione e possono usare i file con le estensioni di file con estensione txt e. csv. Il *lpszDriver* argomento per questo driver potrebbe essere come segue:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Si supponga che un driver per SQL Server non è una DLL di installazione separato e non ha tutte le parole chiave dell'attributo di driver. Il *lpszDriver* argomento per questo driver potrebbe essere come segue:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Dopo aver **SQLInstallDriverEx** recupera le informazioni riguardanti il driver dalle *lpszDriver* argomento, viene aggiunta la descrizione di driver alla sezione [ODBC Drivers] della voce Odbcinst. ini nel sistema informazioni. Quindi crea una sezione intitolata con la descrizione del driver e aggiunge i percorsi completi della DLL del driver e le DLL di installazione. Infine, restituisce il percorso della directory di destinazione dell'installazione, ma non copia i file di driver a esso. Il programma chiamante effettivamente necessario copiare i file dei driver nella directory di destinazione.  
  
 **SQLInstallDriverEx** incrementa il conteggio di utilizzo del componente per il driver installato di 1. Se esiste già una versione del driver, ma il conteggio di utilizzo del componente per il driver non esiste, il nuovo valore di conteggio dell'utilizzo di componente è impostato su 2.  
  
 Il programma di installazione dell'applicazione è responsabile per copiare fisicamente il file del driver e mantenere il conteggio di utilizzo di file. Se il file del driver non è stato precedentemente installato, il programma di installazione dell'applicazione deve copiare il file nei *lpszPathIn* path e creare il conteggio di utilizzo di file. Se il file è stato precedentemente installato, il programma di installazione semplicemente incrementa il conteggio di utilizzo di file e restituisce il percorso dell'installazione precedente nel *lpszPathOut* argomento.  
  
> [!NOTE]  
>  Per altre informazioni sui conteggi dell'utilizzo di componenti e conteggi dell'utilizzo di file, vedere [Conteggio utilizzi](../../../odbc/reference/install/usage-counting.md).  
  
 Se in precedenza è stata installata una versione precedente del file del driver dall'applicazione, il driver deve disinstallare e reinstallare, in modo che il conteggio di utilizzo del componente driver è valido. **SQLConfigDriver** (con un *trattano* di ODBC_REMOVE_DRIVER) deve essere anzitutto chiamata e quindi **SQLRemoveDriver** deve essere chiamato per diminuire il conteggio di utilizzo del componente. **SQLInstallDriverEx** deve quindi essere chiamato per reinstallare il driver, incrementare il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione è necessario sostituire il vecchio file con il nuovo file. Il conteggio di utilizzo file rimarranno invariati e qualsiasi altra applicazione che utilizzato il file versione precedenti useranno la versione più recente.  
  
> [!NOTE]  
>  Se il driver è stato installato precedentemente e **SQLInstallDriverEx** viene chiamato per installare il driver in una directory diversa, la funzione restituirà TRUE, ma *lpszPathOut* includerà le directory il driver in cui è già installato. Il servizio non include la directory immessa nella *lpszDriver* argomento.  
  
 La lunghezza del percorso nella *lpszPathOut* nelle **SQLInstallDriverEx** consente un processo di installazione in due fasi, in modo che un'applicazione può determinare che cosa *cbPathOutMax* deve essere da la chiamata **SQLInstallDriverEx** con un *trattano* della modalità ODBC_INSTALL_INQUIRY. Verrà restituito il numero totale di byte disponibili nel *pcbPathOut* buffer. **SQLInstallDriverEx** può quindi essere chiamato con un *trattano* di ODBC_INSTALL_COMPLETE e il *cbPathOutMax* argomento impostato sul valore di *pcbPathOut*buffer, più il carattere di terminazione null.  
  
 Se si sceglie di non utilizzare il modello in due fasi per **SQLInstallDriverEx**, è necessario impostare *cbPathOutMax*, che definisce le dimensioni della risorsa di archiviazione per il percorso della directory di destinazione, per il valore di MAX_PATH valore, come definito in STDLIB. h, per evitare il troncamento.  
  
 Quando *trattano* ODBC_INSTALL_COMPLETE, viene **SQLInstallDriverEx** nepovoluje hodnotu *lpszPathOut* null (o *cbPathOutMax* sia 0). Se *trattano* è ODBC_INSTALL_COMPLETE, viene restituito FALSE quando il numero di byte disponibili da restituire è maggiore o uguale a *cbPathOutMax*, fornendo il risultato se il troncamento si verifica.  
  
 Dopo aver **SQLInstallDriverEx** è stato chiamato e il programma di installazione dell'applicazione è copiato il file del driver (se necessario), il programma di installazione di driver in cui è necessario chiamare DLL **SQLConfigDriver** per impostare la configurazione per il driver.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Installazione di Gestione driver|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
