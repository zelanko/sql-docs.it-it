---
title: ODBCCONF. PROPRIETÀ EXE . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d771f01d292312f8a0f0060c16e3c348bf2e009e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307532"
---
# <a name="odbcconfexe"></a>ODBCCONF. FILE EXE
ODBCCONF.exe è uno strumento della riga di comando che consente di configurare i driver ODBC e i nomi delle origini dati.  
  
> [!NOTE]  
>  ODBCCONF.exe verrà rimosso in una versione futura dei componenti di accesso ai dati di Windows. Evitare di utilizzare questa funzionalità e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. È possibile usare i comandi di PowerShell per gestire i driver e le origini dati. Per ulteriori informazioni su questi comandi di PowerShell, vedere Cmdlet per i componenti di [accesso ai dati](/powershell/module/wdac)di Windows.  
  
## <a name="syntax"></a>Sintassi  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argomenti  
 *Interruttori*  
 zero o più opzioni di commutazione. Per l'elenco delle opzioni disponibili, vedere la sezione Osservazioni più avanti in questo argomento.  
  
 *Azione*  
 Un'azione da eseguire. Per l'elenco delle opzioni disponibili, vedere la sezione Osservazioni.  
  
## <a name="remarks"></a>Osservazioni  
 Sono disponibili i seguenti interruttori:  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|/A :*azione*|Specificare un'azione.<br /><br /> /A è facoltativo se viene specificata una sola azione.|  
|/?|Visualizzare l'utilizzo per ODBCCONF. NELL'ESEMPIO, AD esempio ,|  
|/C|L'elaborazione continua se un'azione non riesce.|  
|/E|Cancellare il file di risposta specificato con /F al termine dell'elaborazione.|  
|/F|Utilizzare un file di `odbcconf /F my.rsp`risposta, ad esempio .<br /><br /> my.rsp potrebbe essere simile al seguente:`REGSVR c:\my.dll`<br /><br /> /A non viene utilizzato in un file di risposta.|  
|/H|Visualizza utilizzo (Aiuto). Questa opzione è uguale a /?.|  
|/L[*mode*] *nomefile*|Inviare l'output del programma a un file in una delle tre modalità seguenti: normale (n), dettagliato (v) e debug (d). La modalità di debug registra le DLL caricate da odbcconf.exe.<br /><br /> Se si specifica /L senza modalità, il file di registro sarà vuoto.<br /><br /> Ad esempio, **/Lv log.txt**.|  
|/R|L'azione verrà eseguita dopo un riavvio.|  
|/S|Modalità invisibile all'utente. Non visualizzare messaggi di errore.|  
  
 Sono disponibili le azioni seguenti:  
  
|Azione|Descrizione|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name: parametri* di configurazione specifici del driver|Carica la DLL di installazione del driver appropriata e chiama la funzione **ConfigDriver.**<br /><br /> Equivalente alla [funzione SQLConfigDriver](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Ad esempio:<br /><br /> /A : "Nome del driver" "CPTimeout<br /><br /> /A : CONFIGDRIVER " Nome driver" "DriverODBCVer- 03.80"|  
|*Attributi* di &#124; del*nome* CONFIGDSN *driver_name* DSN|Aggiunge o modifica un'origine dati di sistema.<br /><br /> Equivalente alla [funzione SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Ad esempio:<br /><br /> /A "CONFIGDSN "SQL Server" "DSN- nome &#124; Server srv"|  
|Attributi di *&#124;* nome configSYSDSN *attributes* *driver_name* DSN|Aggiunge o modifica un'origine dati di sistema.<br /><br /> Equivalente alla [funzione SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Ad esempio:<br /><br /> /A :CONFIGSYSDSN "SQL Server" "DSN-name &#124; Server srv"|  
|INSTALLDRIVER|Equivalente alla funzione [SQLInstallDriverEx](../odbc/reference/syntax/sqlinstalldriverex-function.md).<br /><br /> Per informazioni sulla sintassi delle coppie parola chiave-valore passata a INSTALLDRIVER, vedere [Sottochiavi di specifica del driver](../odbc/reference/install/driver-specification-subkeys.md).<br /><br /> Ad esempio:<br /><br /> /A : "Driver per il driver &#124; driver c:'.dll &#124;'installazione &#124;'istruzione APILevel di sistema c:".dll &#124; 2 &#124; ConnectFunctions,AAA &#124; DriverODBCVer, 03,50 &#124; FileUsage,0 &#124; SQLLevel, 1"|  
|INSTALLTRANSLATOR configurazione del *traduttore: percorso del driver*|Aggiunge le informazioni su un traduttore **all'HKEY_LOCAL_MACHINE SOFTWARE ODBC.ODBCINST. Chiave** del Registro di sistema INI-ODBC Translators.<br /><br /> Equivalente alla [funzione SQLInstallTranslatorEx](../odbc/reference/syntax/sqlinstalltranslatorex-function.md).<br /><br /> Per informazioni sulla sintassi delle coppie parola chiave-valore passata a INSTALLDRIVER, consultate [Sottochiavi di specifiche traduttori](../odbc/reference/install/translator-specification-subkeys.md).<br /><br /> Ad esempio:<br /><br /> /A : INSTALLTRANSLATOR "Il traduttore &#124; Traduttore c:"my.dll &#124; Setup|  
|DLL *REGSVR*|Registra una DLL.<br /><br /> Equivalente a regsvr32.exe.<br /><br /> Ad esempio:<br /><br /> /A : REGSVR c:|  
|SETFILEDSNDIR (diTER)|Quando HKEY_LOCAL_MACHINE SOFTWARE ODBC ODBC. DSN del file INI-ODBC non esiste, l'azione SETFILEDSNDIR lo creerà e le assegnerà il valore in HKEY_LOCAL_MACHINE, SOFTWARE, Microsoft Windows,CurrentVersion, CommonFilesDir, aggiunto con l'opzione di origine dati .<br /><br /> Il valore in HKEY_LOCAL_MACHINE SOFTWARE ODBC ODBC. DSN file INI-ODBC specifica il percorso predefinito utilizzato da Amministratore origine dati ODBC durante la creazione di un'origine dati basata su file.<br /><br /> Ad esempio:<br /><br /> /A : SETFILEDSNDIR|  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Open Database Connectivity (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
