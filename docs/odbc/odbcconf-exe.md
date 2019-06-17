---
title: ODBCCONF. FILE EXE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2b4d7b20c690a1f4d7f3b445afb8348549309e5c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538204"
---
# <a name="odbcconfexe"></a>ODBCCONF.EXE
ODBCCONF.exe è uno strumento da riga di comando che consente di configurare i nomi delle origini dati e i driver ODBC.  
  
> [!NOTE]  
>  ODBCCONF.exe verrà rimossa in una versione futura di Windows Data Access Components. Evitare di utilizzarla e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. È possibile usare i comandi di PowerShell per gestire i driver e origini dati. Per altre informazioni su questi comandi di PowerShell, vedere [i cmdlet di Windows Data Access Components](https://technet.microsoft.com/library/hh771019.aspx).  
  
## <a name="syntax"></a>Sintassi  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argomenti  
 *switches*  
 Zero o più parametri facoltativi. Per l'elenco di opzioni disponibili, vedere la sezione Osservazioni più avanti in questo argomento.  
  
 *action*  
 Un'azione da eseguire. Per l'elenco delle opzioni disponibili, vedere la sezione Osservazioni.  
  
## <a name="remarks"></a>Note  
 Sono disponibili le opzioni seguenti:  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|/A {*action*}|Specificare un'azione.<br /><br /> /A è facoltativa se viene specificata un'azione.|  
|/?|Visualizzare l'utilizzo per ODBCCONF. FILE EXE.|  
|/C|L'elaborazione continua se un'azione ha esito negativo.|  
|/E|Cancellare il file di risposta specificato con /F al termine dell'elaborazione.|  
|/F|Usare un file di risposta, ad esempio `odbcconf /F my.rsp`.<br /><br /> My.rsp potrebbe essere simile al seguente: `REGSVR c:\my.dll`<br /><br /> /A non viene usato in un file di risposta.|  
|/H|Visualizzare l'utilizzo (Guida). Questa opzione equivale a /?.|  
|/L[*mode*] *filename*|Inviare l'output del programma in un file in una delle tre modalità: normale (n), dettagliato (v) e debug (d). Le DLL che vengono caricati da odbcconf.exe i record delle modalità di debug.<br /><br /> Se si specifica /L senza una modalità, il file di log sarà vuoto.<br /><br /> Ad esempio, **txt /Lv**.|  
|/R|L'azione verrà eseguita dopo un riavvio.|  
|/S|Modalità invisibile all'utente. Non vengono visualizzati i messaggi di errore.|  
  
 Sono disponibili le seguenti azioni:  
  
|Azione|Descrizione|  
|------------|-----------------|  
|CONFIGDRIVER *nome_driver * * i parametri di configurazione specifici del driver*|Carica la DLL di installazione di driver appropriato e chiama il **ConfigDriver** (funzione).<br /><br /> Equivalente per la [funzione SQLConfigDriver](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Ad esempio:<br /><br /> /A {CONFIGDRIVER "Nome Driver" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "Nome Driver" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *nome_driver* DSN =*name* &#124; *attributi*|Aggiunge o modifica un'origine dati di sistema.<br /><br /> Equivalente per la [funzione SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Ad esempio:<br /><br /> /A {CONFIGDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|CONFIGSYSDSN *nome_driver* DSN =*name* &#124; *attributi*|Aggiunge o modifica un'origine dati di sistema.<br /><br /> Equivalente per la [funzione SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Ad esempio:<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|/INSTALLDRIVER|Equivalente a [funzione SQLInstallDriverEx](../odbc/reference/syntax/sqlinstalldriverex-function.md).<br /><br /> Per informazioni sulla sintassi delle coppie parola chiave / valore passata a /INSTALLDRIVER, vedere [sottochiavi di specifica di Driver](../odbc/reference/install/driver-specification-subkeys.md).<br /><br /> Ad esempio:<br /><br /> /A {INSTALLDRIVER  "Your Driver &#124; Driver=c:\your.dll &#124; Setup=c:\your.dll &#124; APILevel=2 &#124; ConnectFunctions=YYY &#124; DriverODBCVer=03.50 &#124; FileUsage=0 &#124; SQLLevel=1"}|  
|INSTALLTRANSLATOR *configurazione di Microsoft translator * * percorso del driver*|Aggiunge informazioni su una funzione di conversione per la **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. I traduttori INI\ODBC** chiave del Registro di sistema.<br /><br /> Equivalente a [funzione SQLInstallTranslatorEx](../odbc/reference/syntax/sqlinstalltranslatorex-function.md).<br /><br /> Per informazioni sulla sintassi delle coppie parola chiave / valore passata a /INSTALLDRIVER, vedere [sottochiavi di specifica di Microsoft Translator](../odbc/reference/install/translator-specification-subkeys.md).<br /><br /> Ad esempio:<br /><br /> /A {INSTALLTRANSLATOR  "My Translator &#124; Translator=c:\my.dll &#124; Setup=c:\my.dll"}|  
|REGSVR *dll*|Registra una DLL.<br /><br /> Equivalente allo regsvr32.exe.<br /><br /> Ad esempio:<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|Quando HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. INI\ODBC File DSN\DefaultDSNDir non esiste, l'azione SETFILEDSNDIR crearlo e assegnare il valore in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir, aggiungendovi \ODBC\Data origini.<br /><br /> Il valore in corrispondenza di HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. INI\ODBC File DSN\DefaultDSNDir specifica il percorso predefinito usato dall'amministratore origine dati ODBC quando si crea un'origine dati basata su file.<br /><br /> Ad esempio:<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>Vedere anche  
 [Microsoft Open Database Connectivity (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
