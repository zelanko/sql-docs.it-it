---
title: SQLManageDataSources | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLManageDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLManageDataSources
helpviewer_keywords:
- SQLManageDataSources [ODBC]
ms.assetid: ac6d186f-b394-406c-94c4-c6331d1ca468
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 819856a584c6133e28e222a704b720337f99cd9c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018960"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLManageDataSources** Visualizza una finestra di dialogo con cui gli utenti possono configurare, aggiungere ed eliminare origini dati in informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>Argomenti  
 *hwnd*  
 [Input] Handle della finestra padre.  
  
## <a name="returns"></a>Valori di codice restituiti  
 **SQLManageDataSources** restituisce FALSE se *hwnd* non è un handle della finestra valida. In caso contrario, restituisce TRUE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLManageDataSources** FALSO, restituisce un oggetto associato  *\*pfErrorCode* valore può essere ottenuto chiamando **SQLInstallerError**. La tabella seguente elenca i  *\*pfErrorCode* i valori che possono essere restituiti da **SQLInstallerError** e illustra ognuna nel contesto di questa funzione.  
  
|*\*pfErrorCode*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore di programma di installazione generale|Errore per cui si è verificato alcun errore di programma di installazione specifico.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiedere* non è riuscita|La chiamata a **ConfigDSN** non è riuscita.|  
|ODBC_ERROR_INVALID__HWND|Handle della finestra valida|Il *hwnd* argomento era NULL o non valido.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è stato possibile eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="managing-data-sources"></a>Gestione delle origini dati  
 **SQLManageDataSources** inizialmente visualizzata la **Amministrazione origine dati ODBC** finestra di dialogo, come illustrato nella figura seguente.  
  
 ![Finestra di dialogo Amministrazione origine dati ODBC](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 La finestra di dialogo consente di visualizzare le origini dati elencate nelle informazioni di sistema in tre schede: **Utente a DSN**, **DSN di sistema**, e **File DSN**. Se l'utente fa doppio clic su un'origine dati o seleziona un'origine dati e sceglie **Configure**, **SQLManageDataSources** chiamate **ConfigDSN** nel programma di installazione DLL con il ODBC_CONFIG_ Opzione DSN.  
  
 Se l'utente fa clic **Add**, **SQLManageDataSources** consente di visualizzare il **Crea nuova origine dati** dialogo illustrata nella figura seguente.  
  
 ![Creare la finestra di dialogo Nuova origine dati](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 La finestra di dialogo Visualizza un elenco di driver installati. Se l'utente fa doppio clic su un driver o seleziona un driver e fa clic su **OK**, **SQLManageDataSources** chiamate **ConfigDSN** nel programma di installazione DLL e lo passa l'opzione ODBC_ADD_DSN.  
  
 Se l'utente seleziona un'origine dati e sceglie **rimuovere**, **SQLManageDataSources** chiede se l'utente vuole eliminare l'origine dati. Se l'utente sceglie **Yes**, **SQLManageDataSources** chiamate **ConfigDSN** nel programma di installazione DLL con l'opzione ODBC_REMOVE_DSN.  
  
 Il **Crea nuova origine dati** nella finestra di dialogo consente di aggiungere o eliminare un'origine dati utente, un'origine dati di sistema o un'origine dati file.  
  
## <a name="user-dsns"></a>DSN utente  
 DSN creato per i singoli utenti verranno chiamati i DSN utente, per distinguerli dai DSN di sistema. I DSN utente vengono registrati come indicato di seguito le informazioni di sistema:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>DSN di sistema  
 Il **Crea nuova origine dati** nella finestra di dialogo consente di aggiungere un'origine dati di sistema nel computer locale o eliminare una o impostare la configurazione per un'origine dati di sistema.  
  
 Un'origine dati impostato con un nome di origine dati (DSN) di sistema può essere usata da più di un utente nello stesso computer. Può anche essere utilizzato da un servizio a livello di sistema, che possa quindi ottenere l'accesso all'origine dati anche se nessun utente è connesso al computer.  
  
 Un DSN di sistema viene registrato nella voce HKEY_LOCAL_MACHINE nelle informazioni di sistema anziché nella voce HKEY_CURRENT_USER. Non è associato a un utente che esegue l'accesso con il proprio nome utente specifico e la password, ma può essere usato da qualsiasi utente del computer o da un servizio automatico a livello di sistema. Il DSN di sistema è, tuttavia, associato a un solo computer. Non supporta la funzionalità di utilizzo remoto DSN tra computer. DSN di sistema sono registrate come indicato di seguito le informazioni di sistema:  
  
 HKEY_LOCAL_MACHINE SOFTWARE ODBC ini  
  
## <a name="file-dsns"></a>DSN file  
 Un'origine dati file non è un nome dell'origine dati, perché esegue un'origine dati di computer e non è registrato per qualsiasi utente o computer. Le informazioni di connessione per l'origine dati sono contenute in un file DSN che può essere copiato in tutti i computer. Un'origine dati file può essere condivisibile, nel qual caso il file DSN si trova in una rete e può essere usata contemporaneamente da più utenti nella rete, purché l'utente abbia il driver appropriato installato. Un'origine dati file può anche essere condivisibile, nel qual caso può essere utilizzato solo in un singolo computer.  
  
 Per altre informazioni sulle origini dati di file, vedere [ci si connette tramite File Zdroje dat](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md), oppure vedere [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="managing-drivers"></a>La gestione dei driver  
 Se l'utente fa clic il **driver** scheda le **Amministrazione origine dati ODBC** della finestra di dialogo **SQLManageDataSources** Visualizza un elenco di driver ODBC installati nel sistema, Oltre a informazioni sui driver. La data visualizzata è la data di creazione del driver, come illustrato nella figura seguente.  
  
 ![Scheda Amministrazione origine dati ODBC driver](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>Opzioni di traccia  
 Se l'utente fa clic il **traccia** scheda le **Amministrazione origine dati ODBC** della finestra di dialogo **SQLManageDataSources** consente di visualizzare le opzioni di traccia, come illustrato nell'esempio seguente Nella figura.  
  
 ![Scheda Tracing Amministrazione origine dati ODBC](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 Se l'utente sceglie **Avvia ora traccia** e quindi fa clic su **OK**, **SQLManageDataSources** abilita la traccia manualmente per tutte le applicazioni attualmente in esecuzione nel computer.  
  
 Se l'utente specifica il nome di un file di traccia nel **percorso file di Log** casella di testo e quindi fa clic su **OK**, **SQLManageDataSources** imposta il **TraceFile** parola chiave nella sezione [ODBC] le informazioni di sistema per il nome specificato.  
  
> [!IMPORTANT]  
>  Supporto per Visual Studio Analyzer è stata rimossa a partire da Windows 8 (Visual Studio Analyzer è stato incluso solo nelle versioni precedenti di Visual Studio). Per una meccanismo di risoluzione dei problemi in alternativa, usare l'analisi BID.  
  
 Se l'utente sceglie **avviare Visual Studio Analyzer** e quindi fa clic su **OK**, Visual Studio Analyzer è abilitata. Rimane abilitata fino alla **arrestare Visual Studio Analyzer** si fa clic.  
  
 Per altre informazioni sulla traccia, vedere [traccia](../../../odbc/reference/develop-app/tracing.md). Per altre informazioni sul **traccia** e **TraceFile** parole chiave, vedere [sottochiave ODBC](../../../odbc/reference/install/odbc-subkey.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Creazione di origini dati|[SQLCreateDataSource](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
