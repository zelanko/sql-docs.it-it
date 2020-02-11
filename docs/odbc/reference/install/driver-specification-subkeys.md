---
title: Sottochiavi di specifica driver | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68094171"
---
# <a name="driver-specification-subkeys"></a>Sottochiavi di specifica del driver
Ogni driver elencato nella sottochiave driver ODBC presenta una sottochiave. Questa sottochiave ha lo stesso nome del valore corrispondente nella sottochiave ODBC drivers. I valori in questa sottochiave elencano i percorsi completi delle DLL di installazione driver e driver, i valori delle parole chiave driver restituiti da **SQLDrivers**e il conteggio di utilizzo. I formati dei valori sono indicati nella tabella seguente.  
  
|Nome|Tipo di dati|data|  
|----------|---------------|----------|  
|APILevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|ConnectFunctions|REG_SZ|{**Y**&#124;**n**} {**y**&#124;**n**} {**y**&#124;**n**}|  
|CreateDSN|REG_SZ|*Driver-Descrizione*|  
|Driver|REG_SZ|*Driver-DLL-Path*|  
|DriverODBCVer|REG_SZ|*nn. nn*|  
|FileExtns|REG_SZ|**\*.** *file-extension1*[**,\*.** *file-extension2*] ...|  
|Fileusage|REG_SZ|**0** &#124; **1** &#124; **2**|  
|Installazione|REG_SZ|*programma di installazione-DLL-percorso*|  
|Sqllevel|REG_SZ|**0** &#124; **1** &#124; **2**|  
|UsageCount|REG_DWORD|*conteggio*|  
  
 La tabella seguente illustra l'uso di ogni parola chiave.  
  
|Parola chiave|Uso|  
|-------------|-----------|  
|**APILevel**|Numero che indica il livello di conformità dell'interfaccia ODBC supportato dal driver:<br /><br /> 0 = Nessuno<br /><br /> 1 = livello 1 supportato<br /><br /> 2 = livello 2 supportato<br /><br /> Deve corrispondere al valore restituito per l'opzione SQL_ODBC_INTERFACE_CONFORMANCE in **SQLGetInfo**.|  
|**CreateDSN**|Nome di una o più origini dati da creare durante l'installazione del driver. Le informazioni di sistema devono includere una sezione specifica dell'origine dati per ogni origine dati elencata con la parola chiave **CreateDSN** . Queste sezioni non devono includere la parola chiave **driver** , perché è specificata nella sezione relativa alla specifica del driver, ma devono includere informazioni sufficienti per la funzione **ConfigDSN** nella DLL di installazione del driver per creare una specifica dell'origine dati senza visualizzare le finestre di dialogo. Per il formato di una sezione specifica dell'origine dati, vedere [sottochiavi di specifica dell'origine dati](../../../odbc/reference/install/data-source-specification-subkeys.md).|  
|**ConnectFunctions**|Stringa di tre caratteri che indica se il driver supporta **SQLConnect**, **SQLDriverConnect**e **SQLBrowseConnect**. Se il driver supporta **SQLConnect**, il primo carattere è "Y"; in caso contrario, è "N". Se il driver supporta **SQLDriverConnect**, il secondo carattere è "Y"; in caso contrario, è "N". Se il driver supporta **SQLBrowseConnect**, il terzo carattere è "Y"; in caso contrario, è "N". Se, ad esempio, un driver supporta **SQLConnect** e **SQLDriverConnect** ma non **SQLBrowseConnect**, la stringa di tre caratteri sarà "YYN".|  
|**DriverODBCVer**|Stringa di caratteri con la versione di ODBC supportata dal driver. Il formato della versione è *nn. nn*, dove le prime due cifre sono la versione principale e le due cifre successive sono la versione secondaria. Per la versione di ODBC descritta in questo manuale, il driver deve restituire "03,00".<br /><br /> Deve corrispondere al valore restituito per l'opzione SQL_DRIVER_ODBC_VER in **SQLGetInfo**.|  
|**FileExtns**|Per i driver basati su file, un elenco delimitato da virgole di estensioni dei file che possono essere usati dal driver. Ad esempio, un driver dBASE potrebbe specificare \*. dbf e un driver di file di testo formattato potrebbe \*specificare\*. txt,. csv. Per un esempio di come un'applicazione può usare queste informazioni, vedere la parola chiave **fileusage** .|  
|**Fileusage**|Numero che indica il modo in cui un driver basato su file tratta direttamente i file in un'origine dati.<br /><br /> 0 = il driver non è un driver basato su file. Un driver ORACLE, ad esempio, è un driver basato su DBMS.<br /><br /> 1 = un driver basato su file considera i file in un'origine dati come tabelle. Un driver Xbase, ad esempio, considera ogni file Xbase come una tabella.<br /><br /> 2 = un driver basato su file considera i file in un'origine dati come un catalogo. Un driver Microsoft® Access, ad esempio, considera ogni file di Microsoft Access come un database completo.<br /><br /> Un'applicazione può utilizzare questa funzione per determinare la modalità di selezione dei dati da parte degli utenti. Ad esempio, gli utenti di Xbase e Paradox spesso considerano i dati archiviati nei file, mentre gli utenti di ORACLE e Microsoft Access generalmente pensano ai dati archiviati nelle tabelle.<br /><br /> Quando un utente seleziona **Apri file di dati** dal menu **file** , un'applicazione può visualizzare la finestra di dialogo Apri comune **file di Windows** . L'elenco dei tipi di file utilizzerà le estensioni di file specificate con la parola chiave **FileExtns** per i driver che specificano un valore **fileusage** pari a 1 e "Y" come secondo carattere del valore della parola chiave **ConnectFunctions** . Dopo che l'utente ha selezionato un file, l'applicazione chiama **SQLDriverConnect** con la parola chiave **driver** , quindi esegue un'istruzione **Select \* from *Table-Name* ** .<br /><br /> Quando l'utente seleziona **Importa dati** dal menu **file** , un'applicazione può visualizzare un elenco di descrizioni per i driver che specificano un valore **fileusage** pari a 0 o 2 e "Y" come secondo carattere del valore della parola chiave **ConnectFunctions** . Dopo che l'utente ha selezionato un driver, l'applicazione chiama **SQLDriverConnect** con la parola chiave **driver** e quindi Visualizza una finestra di dialogo **Seleziona tabella** personalizzata.|  
|**Sqllevel**|Numero che indica la grammatica SQL-92 supportata dal driver:<br /><br /> 0 = voce SQL-92<br /><br /> 1 = FIPS127-2 transizione<br /><br /> 2 = SQL-92 intermedio<br /><br /> 3 = SQL-92 completo<br /><br /> Deve corrispondere al valore restituito per l'opzione SQL_SQL_CONFORMANCE in **SQLGetInfo**.|  
  
 Per informazioni sui conteggi di utilizzo, vedere [conteggio di utilizzo](../../../odbc/reference/install/usage-counting.md) in precedenza in questa sezione.  
  
 Le applicazioni non devono impostare il conteggio dell'utilizzo. Il conteggio verrà mantenuto da ODBC.  
  
 Si supponga, ad esempio, che un driver per i file di testo formattati disponga di una DLL di driver denominata text. dll, una DLL di installazione del driver separata denominata file Txtsetup. dll e che sia stata installata tre volte. Se il driver supporta il livello di conformità dell'API di livello 1, supporta il livello di conformità minimo per la grammatica SQL, considera i file come tabelle e può usare i file con le estensioni. txt e. csv, i valori nella sottochiave di testo potrebbero essere i seguenti:  
  
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
