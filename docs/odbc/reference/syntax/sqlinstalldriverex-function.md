---
title: SQLInstallDriverEx (funzione) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 054e8b6b9eae26bd5f973f3d46d7ef37363a8e79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302123"
---
# <a name="sqlinstalldriverex-function"></a>Funzione SQLInstallDriverEx
**Conformità**  
 Versione introdotta: ODBC 3.0  
  
 **Riepilogo**  
 **SQLInstallDriverEx** aggiunge informazioni sul driver per il Odbcinst.ini voce nelle informazioni di sistema e incrementa *UsageCount* del driver di 1. Tuttavia, se esiste già una versione del driver ma il valore *UsageCount* per il driver non esiste, il nuovo valore *UsageCount* è impostato su 2.  
  
 Questa funzione non copia effettivamente alcun file. È responsabilità del programma chiamante copiare correttamente i file del driver nella directory di destinazione.  
  
 La funzionalità di **SQLInstallDriverEx** è accessibile anche con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
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
 [Ingresso] La descrizione del driver (in genere il nome del DBMS associato) viene presentata agli utenti anziché il nome del driver fisico. L'argomento *lpszDriver* deve contenere un elenco doppiamente con terminazione null di coppie parola chiave-valore che descrivono il driver. Per ulteriori informazioni sulle coppie parola chiave-valore, vedere [Driver Specification Subkeys](../../../odbc/reference/install/driver-specification-subkeys.md). Per ulteriori informazioni sulla stringa doppiamente con terminazione null, vedere [Funzione ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn (informazioni in questo stati in due)*  
 [Ingresso] Percorso completo della directory di destinazione dell'installazione oppure un puntatore null. Se *lpszPathIn* è un puntatore null, i driver verranno installati nella directory di sistema.  
  
 *lpszPathOut (informazioni in base a un'autorizzazione a*  
 [Uscita] Percorso della directory di destinazione in cui deve essere installato il driver. Se il driver non è stato installato in precedenza, *lpszPathOut* deve essere uguale a *lpszPathIn*. Se il driver è stato installato in precedenza, *lpszPathOut* è il percorso dell'installazione precedente.  
  
 *cbPathOutMax*  
 [Ingresso] Lunghezza di *lpszPathOut*.  
  
 *pcbPathOut (informazioni in questo modo in stato di insta*  
 [Uscita] Numero totale di byte (escluso il carattere di terminazione null) disponibili per la restituzione in *lpszPathOut*. Se il numero di byte disponibili da restituire è maggiore o uguale a *cbPathOutMax*, il percorso di output in *lpszPathOut* viene troncato a *cbPathOutMax* meno il carattere di terminazione null. L'argomento *pcbPathOut* può essere un puntatore null.  
  
 *fRichiesta*  
 [Ingresso] Tipo di richiesta. L'argomento *fRequest* deve contenere uno dei valori seguenti:  
  
 ODBC_INSTALL_INQUIRY: informarsi sulla posizione in cui è possibile installare un driver.  
  
 ODBC_INSTALL_COMPLETE: completare la richiesta di installazione.  
  
 *lpdwUsageCount (conteggio informazioni in lingua lingua instato)*  
 [Uscita] Il conteggio di utilizzo del driver dopo la chiamata a questa funzione.  
  
 Le applicazioni non devono impostare il conteggio di utilizzo. ODBC manterrà questo conteggio.  
  
## <a name="returns"></a>Valori di codice restituiti  
 La funzione restituisce TRUE se ha esito positivo, FALSE se ha esito negativo.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLInstallDriverEx** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Lunghezza buffer non valida|L'argomento *lpszPathOut* non è sufficientemente grande per contenere il percorso di output. Il buffer contiene il percorso troncato.<br /><br /> L'argomento *cbPathOutMax* era 0 e *fRequest* era ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo di richiesta non valido|L'argomento *fRequest* non è uno dei seguenti:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Coppie parola chiave-valore non valide|L'argomento *lpszDriver* contiene un errore di sintassi.|  
|ODBC_ERROR_INVALID_PATH|Percorso di installazione non valido|L'argomento *lpszPathIn* contiene un percorso non valido.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|Impossibile caricare il driver o la libreria di installazione del convertitore|Impossibile caricare la libreria di installazione del driver.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Sequenza di parametri non valida|L'argomento *lpszDriver* non contiene un elenco di coppie parola chiave-valore.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|Impossibile incrementare o diminuire il conteggio di utilizzo del componente|Il programma di installazione non è riuscito a incrementare il numero di utilizzo del driver.|  
  
## <a name="comments"></a>Commenti  
 L'argomento *lpszDriver* è un elenco di attributi sotto forma di coppie parola chiave-valore. Ogni coppia viene terminata con un byte null e l'intero elenco viene terminato con un byte null. (Ovvero, due byte null segnano la fine dell'elenco.) Il formato di questo elenco è il seguente:  
  
 _driver-desc_ **\\****=** 0Driver_driver-DLL-nomefile_**\\**0[Setup-DLL-nomefile**=**_setup-DLL-filename_<b>\\</b>0]  
  
 [_driver-attr-keyword1_**=**_value1_<b>\\</b>0] [_driver-attr-keyword2_**=**_value2_<b>\\</b>0]... <b>\\</b>0 (in vie  
  
 dove "0" è un byte null e *driver-attr-keywordn* è qualsiasi parola chiave dell'attributo driver. Le parole chiave devono essere visualizzate nell'ordine specificato. Si supponga, ad esempio, che un driver per i file di testo formattati disponga di driver separati e DLL di installazione e di poter utilizzare file con estensione txt e csv. L'argomento lpszDriver per questo driver potrebbe essere il seguente:The *lpszDriver* argument for this driver might be as follows:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Si supponga che un driver per SQL Server non dispone di una DLL di installazione separata e non dispone di alcuna parola chiave di attributo driver. L'argomento lpszDriver per questo driver potrebbe essere il seguente:The *lpszDriver* argument for this driver might be as follows:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Dopo **che SQLInstallDriverEx** recupera informazioni sul driver dall'argomento *lpszDriver,* aggiunge la descrizione del driver alla sezione [ODBC Drivers] della voce Odbcinst.ini nelle informazioni di sistema. Viene quindi creata una sezione denominata con la descrizione del driver e vengono aggiunti i percorsi completi della DLL del driver e della DLL di installazione. Infine, restituisce il percorso della directory di destinazione dell'installazione, ma non copia i file del driver. Il programma chiamante deve effettivamente copiare i file del driver nella directory di destinazione.  
  
 **SQLInstallDriverEx** incrementa di 1 il conteggio di utilizzo del componente per il driver installato. Se esiste già una versione del driver ma il conteggio di utilizzo del componente per il driver non esiste, il nuovo valore del conteggio di utilizzo del componente è impostato su 2.  
  
 Il programma di installazione dell'applicazione è responsabile della copia fisica del file del driver e della gestione del conteggio dell'utilizzo dei file. Se il file del driver non è stato installato in precedenza, il programma di installazione dell'applicazione deve copiare il file nel percorso *lpszPathIn* e creare il conteggio di utilizzo del file. Se il file è stato installato in precedenza, il programma di installazione incrementa semplicemente il conteggio di utilizzo del file e restituisce il percorso dell'installazione precedente nell'argomento *lpszPathOut.*  
  
> [!NOTE]  
>  Per ulteriori informazioni sui conteggi di utilizzo dei componenti e sui conteggi di utilizzo dei file, vedere [Conteggio utilizzo](../../../odbc/reference/install/usage-counting.md).  
  
 Se una versione precedente del file del driver è stata installata in precedenza dall'applicazione, il driver deve essere disinstallato e quindi reinstallato, in modo che il numero di utilizzo del componente driver sia valido. **SQLConfigDriver** (con un *fRequest* di ODBC_REMOVE_DRIVER) deve prima essere chiamato e quindi **SQLRemoveDriver** deve essere chiamato per diminuire il conteggio di utilizzo del componente. **SQLInstallDriverEx** deve quindi essere chiamato per reinstallare il driver, incrementando il conteggio di utilizzo del componente. Il programma di installazione dell'applicazione deve sostituire il file precedente con il nuovo file. Il conteggio di utilizzo del file rimarrà invariato e qualsiasi altra applicazione che ha utilizzato il file della versione precedente utilizzerà ora la versione più recente.  
  
> [!NOTE]  
>  Se il driver è stato installato in precedenza e **SQLInstallDriverEx** viene chiamato per installare il driver in una directory diversa, la funzione restituirà TRUE, ma *lpszPathOut* includerà la directory in cui il driver è già stato installato. Non includerà la directory immessa nell'argomento *lpszDriver.*  
  
 La lunghezza del percorso in *lpszPathOut* in **SQLInstallDriverEx** consente un processo di installazione a due fasi, pertanto un'applicazione può determinare quale *cbPathOutMax* deve essere chiamando **SQLInstallDriverEx** con *una modalità fRequest* di ODBC_INSTALL_INQUIRY. Verrà restituito il numero totale di byte disponibili nel buffer *pcbPathOut.* **SQLInstallDriverEx** può quindi essere chiamato con *un fRequest* di ODBC_INSTALL_COMPLETE e l'argomento *cbPathOutMax* impostato sul valore nel buffer *pcbPathOut,* più il carattere di terminazione null.  
  
 Se si sceglie di non utilizzare il modello a due fasi per **SQLInstallDriverEx**, è necessario impostare *cbPathOutMax*, che definisce la dimensione dell'archiviazione per il percorso della directory di destinazione, sul valore _MAX_PATH, come definito in Stdlib.h, per impedire il troncamento.  
  
 Quando *fRequest* è ODBC_INSTALL_COMPLETE, **SQLInstallDriverEx** non consente a *lpszPathOut* di essere NULL (o *cbPathOutMax* 0). Se *fRequest* è ODBC_INSTALL_COMPLETE, VIENE restituito FALSE quando il numero di byte disponibili da restituire è maggiore o uguale a *cbPathOutMax*, con il risultato che si verifica il troncamento.  
  
 Dopo **che SQLInstallDriverEx** è stato chiamato e il programma di installazione dell'applicazione ha copiato il file del driver (se necessario), la DLL di installazione del driver deve chiamare **SQLConfigDriver** per impostare la configurazione per il driver.  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Installazione di Gestione driver|[SQLInstallDriverManager (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
