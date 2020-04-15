---
title: Proprietà SQLManageDataSources . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3b572a861af3479e1543be9fda9598cc7e25d36c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290219"
---
# <a name="sqlmanagedatasources"></a>SQLManageDataSources
**Conformità**  
 Versione introdotta: ODBC 2.0  
  
 **Riepilogo**  
 **SQLManageDataSources** visualizza una finestra di dialogo con cui gli utenti possono impostare, aggiungere ed eliminare origini dati nelle informazioni di sistema.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
  
BOOL SQLManageDataSources(  
     HWND     hwnd);  
```  
  
## <a name="arguments"></a>Argomenti  
 *Hwnd*  
 [Ingresso] Handle della finestra padre.  
  
## <a name="returns"></a>Valori di codice restituiti  
 **SQLManageDataSources** restituisce FALSE se *hwnd* non è un handle di finestra valido. In caso contrario, restituisce TRUE.  
  
## <a name="diagnostics"></a>Diagnostica  
 Quando **SQLManageDataSources** restituisce FALSE, è possibile ottenere un valore * \*pfErrorCode* associato chiamando **SQLInstallerError**. Nella tabella seguente * \** sono elencati i valori pfErrorCode che possono essere restituiti da **SQLInstallerError** e ognuno di essi illustra ognuno nel contesto di questa funzione.  
  
|*\*pfErrorCode (codice pfErrorCode)*|Errore|Descrizione|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Errore generale del programma di installazione|Si è verificato un errore per il quale non si è verificato alcun errore specifico del programma di installazione.|  
|ODBC_ERROR_REQUEST_FAILED|*Richiesta* non riuscita|La chiamata a **ConfigDSN** non è riuscita.|  
|ODBC_ERROR_INVALID__HWND|Handle di finestra non valido|L'argomento *hwnd* non è valido o NULL.|  
|ODBC_ERROR_OUT_OF_MEM|Memoria insufficiente|Il programma di installazione non è riuscito a eseguire la funzione a causa della mancanza di memoria.|  
  
## <a name="managing-data-sources"></a>Gestione delle origini dati  
 **SQLManageDataSources** visualizza inizialmente la finestra di dialogo **Amministratore origine dati ODBC,** come illustrato nella figura seguente.  
  
 ![Finestra di dialogo Amministratore origine dati ODBC](../../../odbc/reference/syntax/media/ch23e.gif "CH23E")  
  
 Nella finestra di dialogo vengono visualizzate le origini dati elencate nelle informazioni di sistema in tre schede: **DSN utente**, **DSN**di sistema e **DSN su file**. Se l'utente fa doppio clic su un'origine dati o seleziona un'origine dati e fa clic su **Configura**, **SQLManageDataSources** chiama **ConfigDSN** nella DLL di installazione con l'opzione ODBC_CONFIG_DSN .  
  
 Se l'utente fa clic su **Aggiungi**, **SQLManageDataSources** visualizza la finestra di dialogo **Crea nuova origine dati,** illustrata nella figura seguente.  
  
 ![Finestra di dialogo Crea nuova origine dati](../../../odbc/reference/syntax/media/ch23f.gif "CH23F")  
  
 Nella finestra di dialogo viene visualizzato un elenco dei driver installati. Se l'utente fa doppio clic su un driver o seleziona un driver e fa clic su **OK**, **SQLManageDataSources** chiama **ConfigDSN** nella DLL di installazione e lo passa l'opzione ODBC_ADD_DSN .  
  
 Se l'utente seleziona un'origine dati e fa clic su **Rimuovi**, **SQLManageDataSources** chiede se l'utente desidera eliminare l'origine dati. Se l'utente fa clic su **Sì**, **SQLManageDataSources** chiama **ConfigDSN** nella DLL di installazione con l'opzione ODBC_REMOVE_DSN.  
  
 La finestra di dialogo **Crea nuova origine dati** viene utilizzata per aggiungere o eliminare un'origine dati utente, un'origine dati di sistema o un'origine dati su file.  
  
## <a name="user-dsns"></a>DSN utente  
 DSN creati per singoli utenti verranno denominati DSN utente, per distinguerli dai DSN di sistema. I DSN utente vengono registrati come segue nelle informazioni di sistema:  
  
 `HKEY_CURRENT_USERS`  
  
 `SOFTWARE`  
  
 `ODBC`  
  
 `Odbc.ini`  
  
## <a name="system-dsns"></a>DSN di sistema  
 La finestra di dialogo **Crea nuova origine dati** consente di aggiungere un'origine dati di sistema al computer locale o di eliminarne una o di impostare la configurazione per un'origine dati di sistema.  
  
 Un'origine dati impostata con un nome origine dati di sistema (DSN) può essere utilizzata da più utenti sullo stesso computer. Può anche essere utilizzato da un servizio a livello di sistema, che può quindi accedere all'origine dati anche se nessun utente è connesso al computer.  
  
 Un DSN di sistema viene registrato nella voce HKEY_LOCAL_MACHINE nelle informazioni di sistema anziché nella voce HKEY_CURRENT_USER. Non è legato a un utente che accede con il proprio nome utente e password specifici, ma può essere utilizzato da qualsiasi utente di tale macchina o da un servizio automatico a livello di sistema. Il DSN di sistema è, tuttavia, legato a una macchina. Non supporta la capacità di utilizzare DSN remoti tra computer. I DSN di sistema vengono registrati come segue nelle informazioni di sistema:  
  
 HKEY_LOCAL_MACHINE SOFTWARE ODBC Odbc.ini  
  
## <a name="file-dsns"></a>DSN su file  
 Un'origine dati su file non dispone di un nome di origine dati, così come un'origine dati macchina, e non è registrata per un utente o un computer. Le informazioni di connessione per tale origine dati sono contenute in un file DSN che può essere copiato in qualsiasi computer. Un'origine dati su file può essere condissiva, nel qual caso il file DSN risiede in una rete e può essere utilizzato contemporaneamente da più utenti in rete, purché l'utente abbia installato il driver appropriato. Un'origine dati su file può anche non essere condivisibile, nel qual caso può essere utilizzata solo su un singolo computer.  
  
 Per ulteriori informazioni sulle origini dati su file, vedere [Connessione tramite origini dati file](../../../odbc/reference/develop-app/connecting-using-file-data-sources.md)o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md).  
  
## <a name="managing-drivers"></a>Gestione dei driver  
 Se l'utente fa clic sulla scheda **Driver** nella finestra di dialogo **Amministratore origine dati ODBC** , **SQLManageDataSources** visualizza un elenco di driver ODBC installati nel sistema, nonché informazioni sui driver. La data visualizzata è la data di creazione del driver, come illustrato nella figura seguente.  
  
 ![Scheda Driver della finestra di dialogo Amministratore origine dati ODBC](../../../odbc/reference/syntax/media/ch23g.gif "ch23g")  
  
## <a name="tracing-options"></a>Opzioni di traccia  
 Se l'utente fa clic sulla scheda **Traccia** nella finestra di dialogo **Amministratore origine dati ODBC,** **SQLManageDataSources** visualizza le opzioni di traccia, come illustrato nella figura seguente.  
  
 ![Scheda Analisi della finestra di dialogo Amministratore origine dati ODBC](../../../odbc/reference/syntax/media/ch23h.gif "Ch23h")  
  
 Se l'utente fa clic su **Avvia traccia ora** e quindi sceglie **OK**, **SQLManageDataSources** abilita la traccia manualmente per tutte le applicazioni attualmente in esecuzione nel computer.  
  
 Se l'utente specifica il nome di un file di traccia nella casella di testo Percorso file di **registro** e quindi fa clic **su OK**, **SQLManageDataSources** imposta la parola chiave **TraceFile** nella sezione [ODBC] delle informazioni di sistema sul nome specificato.  
  
> [!IMPORTANT]  
>  Il supporto per Visual Studio Analyzer è stato rimosso a partire da Windows 8 (Visual Studio Analyzer è stato incluso solo nelle versioni precedenti di Visual Studio.). Per un meccanismo di risoluzione dei problemi alternativo, usare la traccia BID.  
  
 Se l'utente fa clic su **Avvia Visual Studio Analyzer** e quindi su **OK**, Visual Studio Analyzer è abilitato. Rimane abilitato fino a quando non si fa clic su **Arresta Visual Studio Analyzer.**  
  
 Per ulteriori informazioni sull'analisi, vedere [Traccia](../../../odbc/reference/develop-app/tracing.md). Per ulteriori informazioni sulle parole chiave **Trace** e **TraceFile** , vedere [Subkey ODBC](../../../odbc/reference/install/odbc-subkey.md).  
  
## <a name="related-functions"></a>Funzioni correlate  
  
|Per informazioni su|Vedere|  
|---------------------------|---------|  
|Creazione di origini dati|[SQLCreateDataSource (origine SQLCreateDataSource)](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|
