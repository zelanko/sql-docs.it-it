---
title: Sottochiavi di specifica di driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], driver specification subkeys
- driver specification subkeys [ODBC]
- registry entries for components [ODBC], driver specification subkeys
- drivers subkey [ODBC]
ms.assetid: b4d802ef-b199-4e64-b7a5-6f2b3e5e2c80
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8f5523c54286ed2e7cc554745dc269599115793e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094171"
---
# <a name="driver-specification-subkeys"></a>Sottochiavi di specifica del driver
Ogni driver elencate nella sottochiave del driver ODBC ha una sottochiave propri. Questa sottochiave ha lo stesso nome come valore corrispondente nella sottochiave ODBC driver. I valori sotto questa sottochiave elencare i percorsi completi dei driver e file DLL, i valori delle parole chiave del driver restituite da di installazione di driver **SQLDrivers**e il conteggio di utilizzo. I formati dei valori vengono visualizzati nella tabella seguente.  
  
|Name|Tipo di dati|Data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**N**}{**Y**&#124;**N**}{**Y**&#124;**N**}|  
|CreateDSN|REG_SZ|*driver-description*|  
|Driver|REG_SZ|*driver-DLL-path*|  
|DriverODBCVer|REG_SZ|*nn.nn*|  
|FileExtns|REG_SZ|**\*.** *file-extension1*[ **,\*.** *file-extension2*]...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Configurazione|REG_SZ|*il programma di installazione-DLL-path*|  
|SQLLevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*count*|  
  
 Nella tabella seguente viene illustrato l'utilizzo di ogni parola chiave.  
  
|Parola chiave|Uso|  
|-------------|-----------|  
|**APILevel**|Numero che indica ODBC interfaccia livello di conformità è supportata dal driver:<br /><br /> 0 = Nessuno<br /><br /> 1 = supportati da livello 1<br /><br /> 2 = livello 2 è supportato<br /><br /> Questo deve essere uguale al valore restituito per l'opzione di SQL_ODBC_INTERFACE_CONFORMANCE **SQLGetInfo**.|  
|**CreateDSN**|Il nome di uno o più origini dati da creare quando il driver è installato. Le informazioni di sistema devono includere una sezione specifica di origine di dati per ogni origine di dati elencati con il **CreateDSN** (parola chiave). Queste sezioni non devono includere il **Driver** parola chiave, perché questo è specificato nella sezione specifica di driver, ma deve includere le informazioni necessarie per il **ConfigDSN** nel driver (funzione) DLL per creare una specifica origine dati senza visualizzare alcuna finestra di dialogo di installazione. Per il formato di una sezione specifica di origine dati, vedere [sottochiavi di specifica origine dati](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Una stringa di tre caratteri che indica se il driver supporta **SQLConnect**, **SQLDriverConnect**, e **SQLBrowseConnect**. Se il driver supporta **SQLConnect**, il primo carattere è "Y", in caso contrario, ovvero "N". Se il driver supporta **SQLDriverConnect**, il secondo carattere è "Y", in caso contrario, ovvero "N". Se il driver supporta **SQLBrowseConnect**, il terzo carattere è "Y", in caso contrario, ovvero "N". Se, ad esempio, un driver supporta **SQLConnect** e **SQLDriverConnect** ma non **SQLBrowseConnect**, la stringa di tre caratteri è "YYN".|  
|**DriverODBCVer**|Una stringa di caratteri con la versione di ODBC supportate dal driver. La versione è nel formato *nn.nn*, in cui le prime due cifre sono la versione principale e le due cifre sono la versione secondaria. Per la versione di ODBC, descritta in questo manuale, il driver deve restituire "03.00".<br /><br /> Questo deve essere uguale al valore restituito per l'opzione di SQL_DRIVER_ODBC_VER **SQLGetInfo**.|  
|**FileExtns**|Per i driver basati su file, un elenco delimitato da virgole di estensioni dei file il driver può utilizzare. Ad esempio, è necessario specificare un driver dBASE \*può specificare file con estensione dbf e un driver del file di testo formattato \*file con estensione txt,\*con estensione csv. Per un esempio di come un'applicazione può usare queste informazioni, vedere la **FileUsage** (parola chiave).|  
|**FileUsage**|Numero che indica il modo in cui un driver basati su file considera direttamente i file in un'origine dati.<br /><br /> 0 = il driver non è un driver basati su file. Ad esempio, un driver ORACLE è un driver basati su DBMS.<br /><br /> 1 = un file di driver basati su file considera in un'origine dati come tabelle. Ad esempio, un driver Xbase considera ogni file Xbase come una tabella.<br /><br /> 2 = un file in cui viene trattato driver basati su file in un'origine dati come un catalogo. Ad esempio, un driver Microsoft® Access considera ogni file di Microsoft Access come un database completo.<br /><br /> Un'applicazione può utilizzare per determinare come gli utenti la selezione dei dati. Ad esempio, gli utenti Xbase e Paradox considerare spesso i dati archiviati in file, mentre gli utenti di ORACLE e Microsoft Access in genere considerare i dati come archiviati nelle tabelle.<br /><br /> Quando un utente seleziona **Apri File di dati** dal **File** dal menu, un'applicazione è stato possibile visualizzare il **Windows File Open** finestra di dialogo comune. L'elenco dei tipi di file utilizza le estensioni di file specificate con il **FileExtns** parola chiave per i driver che specificano un **FileUsage** pari a 1 e "Y", come il secondo carattere del valore della  **ConnectFunctions** (parola chiave). Dopo che l'utente seleziona un file, l'applicazione chiamerebbe **SQLDriverConnect** con il **DRIVER** (parola chiave) e quindi eseguire una **selezionare \* FROM *-nome della tabella***   istruzione.<br /><br /> Quando l'utente seleziona **Import Data** dalle **File** menu, un'applicazione potrebbe visualizzare un elenco di descrizioni per i driver che specificano un **FileUsage** pari a 0 o 2 e "Y" come il secondo carattere del valore della **ConnectFunctions** (parola chiave). Dopo che l'utente seleziona un driver, l'applicazione chiamerebbe **SQLDriverConnect** con il **DRIVER** (parola chiave) e visualizzare un oggetto personalizzato **Seleziona tabella** nella finestra di dialogo.|  
|**SQLLevel**|Numero che indica la grammatica SQL-92 supportata dal driver:<br /><br /> 0 = voce SQL-92<br /><br /> 1 = transizione FIPS127-2<br /><br /> 2 = SQL-92 intermedio<br /><br /> 3 = Full SQL-92<br /><br /> Questo deve essere uguale al valore restituito per l'opzione di SQL_SQL_CONFORMANCE **SQLGetInfo**.|  
  
 Per informazioni su conteggi dell'utilizzo, vedere [Conteggio utilizzi](../../../odbc/reference/install/usage-counting.md) più indietro in questa sezione.  
  
 Le applicazioni non devono impostare il conteggio di utilizzo. ODBC manterrà questo conteggio.  
  
 Ad esempio, si supponga che un driver per i file di testo formattato dispone di un DLL denominata Text.dll driver, un programma di installazione di driver separato DLL denominata Txtsetup.dll e sia stata installata per tre volte. Se il driver supporta il livello di conformità API di livello 1, supporta il livello di conformità di grammatica SQL minima, considera i file in tabelle e può usare i file con le estensioni di file con estensione txt e. csv, i valori nella sottochiave del testo potrebbero essere come segue:  
  
```  
APILevel : REG_SZ : 1  
ConnectFunctions : REG_SZ : YYN  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\TEXT.DLL  
DriverODBCVer : REG_SZ : 03.00.00  
FileExtns : REG_SZ : *.txt,*.csv  
FileUsage : REG_SZ : 1  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\TXTSETUP.DLL  
SQLLevel : REG_SZ : 0  
UsageCount : REG_DWORD : 0x3  
```
