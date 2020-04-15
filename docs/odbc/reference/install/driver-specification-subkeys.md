---
title: Sottochiavi delle specifiche dei driver Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 47aa75f647e5fd8a88168611a3b21284962c70a4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280581"
---
# <a name="driver-specification-subkeys"></a>Sottochiavi di specifica del driver
Ogni driver elencato nella sottochiave Driver ODBC dispone di una sottochiave propria. Questa sottochiave ha lo stesso nome del valore corrispondente nella sottochiave Driver ODBC. I valori in questa sottochiave elencano i percorsi completi delle DLL di installazione del driver e del driver, i valori delle parole chiave del driver restituite da **SQLDrivers**e il conteggio di utilizzo. I formati dei valori sono come illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|Livello API|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions (Funzioni di connessione)|REG_SZ|Y**Y**&#124;&#124;**&#124;** **N** **N****Y** **N**|  
|CreazioneDSN|REG_SZ|*descrizione del conducente*|  
|Driver|REG_SZ|*driver-DLL-percorso*|  
|DriverODBCVer|REG_SZ|*nn.nn (informazioni in base al tano*|  
|FileExtns (Extns)|REG_SZ|**\*.** *estensione file1*[**\*, .** *estensione file2*] ...|  
|FileUsage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Configurazione|REG_SZ|*setup-DLL-percorso*|  
|Livello SQL|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*count*|  
  
 L'uso di ogni parola chiave è illustrato nella tabella seguente.  
  
|Parola chiave|Uso|  
|-------------|-----------|  
|**Livello API**|Numero che indica il livello di conformità dell'interfaccia ODBC supportato dal driver:<br /><br /> 0 = Nessuno<br /><br /> 1 - Livello 1 supportato<br /><br /> 2 - Livello 2 supportato<br /><br /> Deve essere uguale al valore restituito per l'opzione SQL_ODBC_INTERFACE_CONFORMANCE in **SQLGetInfo**.|  
|**CreazioneDSN**|Nome di una o più origini dati da creare durante l'installazione del driver. Le informazioni di sistema devono includere una sezione specifica dell'origine dati per ogni origine dati elencata con la parola **chiave CreateDSN.** Queste sezioni non devono includere la parola chiave **Driver,** poiché questa opzione è specificata nella sezione relativa alle specifiche del driver, ma devono includere informazioni sufficienti per la funzione **ConfigDSN** nella DLL di installazione del driver per creare una specifica dell'origine dati senza visualizzare alcuna finestra di dialogo. Per la sezione relativa al formato di una specifica dell'origine dati, vedere [Sottochiavi di specifica dell'origine dati](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions (Funzioni di connessione)**|Stringa di tre caratteri che indica se il driver supporta **SQLConnect**, **SQLDriverConnect**e **SQLBrowseConnect**. Se il driver supporta **SQLConnect**, il primo carattere è "Y"; in caso contrario, è "N". Se il driver supporta **SQLDriverConnect**, il secondo carattere è "Y"; in caso contrario, è "N". Se il driver supporta **SQLBrowseConnect**, il terzo carattere è "Y"; in caso contrario, è "N". Ad esempio, se un driver supporta **SQLConnect** e **SQLDriverConnect** ma non **SQLBrowseConnect**, la stringa di tre caratteri è "YYN".|  
|**DriverODBCVer**|Stringa di caratteri con la versione di ODBC supportata dal driver. La versione ha il formato *nn.nn*, dove le prime due cifre sono la versione principale e le due cifre successive sono la versione secondaria. Per la versione di ODBC descritta in questo manuale, il driver deve restituire "03.00".<br /><br /> Deve essere uguale al valore restituito per l'opzione SQL_DRIVER_ODBC_VER in **SQLGetInfo**.|  
|**FileExtns (Extns)**|Per i driver basati su file, un elenco separato da virgole delle estensioni dei file che il driver può utilizzare. Ad esempio, un driver \*dBASE potrebbe specificare .dbf \*e un\*driver di file di testo formattato potrebbe specificare .txt, .csv. Per un esempio di utilizzo di queste informazioni da parte di un'applicazione, vedere la parola chiave **FileUsage.For** an example of how an application might use this information, see the FileUsage keyword.|  
|**FileUsage**|Numero che indica il modo in cui un driver basato su file considera direttamente i file in un'origine dati.<br /><br /> 0 - Il driver non è un driver basato su file. Ad esempio, un driver ORACLE è un driver basato su DBMS.<br /><br /> 1 - Un driver basato su file considera i file in un'origine dati come tabelle. Ad esempio, un driver Xbase considera ogni file Xbase come una tabella.<br /><br /> 2 - Un driver basato su file considera i file in un'origine dati come un catalogo. Ad esempio, un driver di Microsoft® Access considera ogni file di Microsoft Access come un database completo.<br /><br /> Un'applicazione può utilizzare questo per determinare come gli utenti selezioneranno i dati. Ad esempio, gli utenti Xbase e Paradox spesso pensano ai dati come memorizzati nei file, mentre gli utenti di ORACLE e Microsoft Access generalmente pensano ai dati come memorizzati nelle tabelle.<br /><br /> Quando un utente seleziona **Apri file di dati** dal menu **File** , un'applicazione potrebbe visualizzare la finestra di dialogo comune Apri file di **Windows.** L'elenco dei tipi di file utilizzerebbe le estensioni di file specificate con la parola chiave **FileExtns** per i driver che specificano un valore **FileUsage** pari a 1 e "Y" come secondo carattere del valore della parola chiave **ConnectFunctions.** Dopo che l'utente seleziona un file, l'applicazione chiamerà **SQLDriverConnect** con la parola chiave **DRIVER** e quindi esegue un'istruzione ** \* SELECT FROM del *nome della tabella.* **<br /><br /> Quando l'utente seleziona **Importa dati** dal menu **File,** un'applicazione potrebbe visualizzare un elenco di descrizioni per i driver che specificano un valore **FileUsage** pari a 0 o 2 e "Y" come secondo carattere del valore della parola chiave **ConnectFunctions.** Dopo che l'utente seleziona un driver, l'applicazione chiamerà **SQLDriverConnect** con la parola chiave **DRIVER** e quindi visualizza una finestra di dialogo **personalizzata Seleziona tabella.**|  
|**Livello SQL**|Numero che indica la grammatica SQL-92 supportata dal driver:<br /><br /> 0 - Voce SQL-92<br /><br /> 1 - FIPS127-2 Transitorio<br /><br /> 2 - SQL-92 Intermedio<br /><br /> 3 - SQL-92 Completo<br /><br /> Deve essere uguale al valore restituito per l'opzione SQL_SQL_CONFORMANCE in **SQLGetInfo**.|  
  
 Per informazioni sui conteggi di utilizzo, vedere [Conteggio dati di utilizzo](../../../odbc/reference/install/usage-counting.md) più indietro in questa sezione.  
  
 Le applicazioni non devono impostare il conteggio di utilizzo. ODBC manterrà questo conteggio.  
  
 Si supponga, ad esempio, che un driver per i file di testo formattati disponga di una DLL di driver denominata Text.dll, di una DLL di installazione del driver separata denominata Txtsetup.dll ed è stata installata tre volte. Se il driver supporta il livello di conformità dell'API di livello 1, supporta il livello di conformità grammaticale SQL minimo, considera i file come tabelle e può utilizzare i file con le estensioni con estensione txt e csv, i valori della sottochiave Text potrebbero essere i seguenti:  
  
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
