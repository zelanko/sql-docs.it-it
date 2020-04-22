---
title: Requisiti di sistema, installazione e file del driver | Microsoft Docs
description: Questo articolo descrive i requisiti di sistema per Microsoft ODBC Driver for SQL Server.
ms.custom: ''
ms.date: 03/18/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e2b56528a369d58238a545afc20b35787003b6b1
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484451"
---
# <a name="system-requirements-installation-and-driver-files"></a>Requisiti di sistema, installazione e file del driver

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Questo articolo illustra i driver ODBC che si connettono a SQL Server.

## <a name="sql-version-compatibility"></a>Compatibilità tra versioni SQL

Il termine compatibilità indica che un driver è stato testato per la compatibilità con le versioni esistenti di SQL al momento del rilascio del driver. Nelle varie versioni SQL Server si prova in genere a mantenere la compatibilità con le versioni precedenti dei driver client esistenti. Tuttavia, le nuove funzionalità nelle versioni di SQL Server potrebbero non essere disponibili con i driver client meno recenti.

|Versione driver|database SQL di Azure|Azure SQL DW|Istanza gestita di SQL di Azure|SQL Server 2019|SQL Server 2017|SQL Server 2016|SQL Server 2014|SQL Server 2012|SQL Server 2008 R2|SQL Server 2008|SQL Server 2005|
|-|-|-|-|-|-|-|-|-|-|-|-|
|17.5|S|S|S|S|S|S|S|S| | | |
|17.4|S|S|S|S|S|S|S|S| | | |
|17.3|S|S|S|S|S|S|S|S|S|S| |
|17.2|S|S|S| |S|S|S|S|S|S| |
|17.1|S|S|S| |S|S|S|S|S|S| |
|17.0|S|S|S| |S|S|S|S|S|S| |
|13.1| | | | |S|S|S|S|S|S| |
|13  | | | | | |S|S|S|S|S| |
|11  | | | | | | |S|S|S|S|S|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>Informazioni dettagliate sulla stringa di connessione

Il nome del driver specificato in una stringa di connessione è `ODBC Driver 11 for SQL Server` o `ODBC Driver 13 for SQL Server` (sia per la versione 13 che per la versione 13.1) oppure `ODBC Driver 17 for SQL Server`.

## <a name="supported-operating-systems"></a>Sistemi operativi supportati

La matrice seguente indica il supporto della versione del driver per le versioni del sistema operativo Windows:

|Versione driver|Windows Server 2019|Windows Server 2016|Windows Server 2012 R2|Windows Server 2012|Windows Server 2008 R2|Windows 10|Windows 8.1|Windows 7|Windows Vista SP2|
|-|-|-|-|-|-|-|-|-|-|
|17.5|S|S|S|S| |S|S| | |
|17.4|S|S|S|S|S|S|S|S| |
|17.3|S|S|S|S|S|S|S|S| |
|17.2| |S|S|S|S|S|S|S| |
|17.1| |S|S|S|S|S|S|S| |
|17.0| |S|S|S|S|S|S|S| |
|13.1| |S|S|S|S|S|S|S| |
|13  | | | |S|S| |S|S| |
|11  | | | |S|S| | |S|S|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Installazione di Microsoft ODBC Driver for SQL Server

Il driver viene installato quando si esegue `msodbcsql.msi` da uno dei [download per Windows](../download-odbc-driver-for-sql-server.md#download-for-windows).

> [!NOTE]
> A coloro che hanno installato Driver 17.1.0.1 o versioni successive, è consigliabile disinstallare questa versione manualmente prima di installare la versione più recente del driver.

### <a name="side-by-side-with-native-client"></a>Installazione side-by-side con Native Client

Il driver ODBC può essere installato side-by-side con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. È possibile installare side-by-side anche le versioni principali del driver (11, 13, 17).

Quando si chiama `msodbcsql.msi`, solo i componenti client vengono installati per impostazione predefinita. I componenti client sono file che supportano l'esecuzione di un'applicazione sviluppata tramite il driver. Per installare i componenti dell'SDK, specificare `ADDLOCAL=ALL` nella riga di comando. Ecco un esempio.
  
```console
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  

### <a name="end-user-license"></a>Licenza per l'utente finale

Specificare `IACCEPTMSODBCSQLLICENSETERMS=YES` per accettare le condizioni di licenza per l'utente finale se si usa l'opzione di installazione `/passive`, `/qn`, `/qb` o `/qr`. È necessario specificare questa opzione in lettere maiuscole. Ecco un esempio.
  
```console
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  

### <a name="silent-uninstall"></a>Disinstallazione invisibile all'utente

L'esempio riportato di seguito illustra come eseguire una disinstallazione invisibile all'utente.
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>Indicare la dipendenza

Quando un'applicazione usa il driver, deve indicare che dipende da questo tramite l'opzione di installazione `APPGUID`. Questa indicazione consente al programma di installazione del driver di segnalare le applicazioni dipendenti prima della disinstallazione. Per specificare una dipendenza dal driver, impostare il parametro della riga di comando `APPGUID` sul codice prodotto al momento di eseguire l'installazione invisibile all'utente del driver. Quando si utilizza Microsoft Installer per aggregare il programma di installazione dell'applicazione, è necessario creare un codice prodotto. Ecco un esempio.
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Strumenti da riga di comando: sqlcmd.exe e bcp.exe

Gli strumenti `bcp.exe` e `sqlcmd.exe` da usare con il driver possono essere scaricati in [Microsoft Command Line Utilities 11 for SQL Server](https://www.microsoft.com/download/details.aspx?id=36433), [Microsoft Command Line Utilities 13 for SQL Server](https://www.microsoft.com/download/details.aspx?id=52680) o [Microsoft Command Line Utilities 13.1 for SQL Server](https://www.microsoft.com/download/details.aspx?id=53591). Il driver è un prerequisito per l'installazione di `sqlcmd.exe` e `bcp.exe`.
  
`bcp.exe` e `sqlcmd.exe` vengono installati nella sottocartella `110\Tools` di `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` per la versione 11 e in `130\Tools` per le versioni 13 e 13.1.

Il driver specificato in un'applicazione che usa funzioni BCP deve essere della stessa versione fornita con il file di intestazione e la libreria usati per compilare l'applicazione stessa.  

Ad esempio, quando si compila un'applicazione ODBC con `msodbcsql11.lib` e `msodbcsql.h`, usare "DRIVER={ODBC Driver 11 for SQL Server}" nella stringa di connessione.

## <a name="components-of-the-microsoft-odbc-driver-for-ssnoversion-on-windows"></a>Componenti di Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows

Il driver ODBC in Windows contiene i componenti seguenti:

| Componente | Descrizione |
| :-------- | :---------- |
|msodbcsql17.dll o <br/> msodbcsql13.dll o <br/> msodbcsql11.dll|File della DLL (Dynamic-Link Library, libreria di collegamento dinamico) che contiene tutte le funzionalità del driver. Il file viene installato in %SYSTEMROOT%\System32.|  
|msodbcdiag17.dll o <br/> msodbcdiag13.dll o <br/> msodbcdiag11.dll|File DLL che contiene l'interfaccia di diagnostica (traccia) del driver. Il file viene installato in %SYSTEMROOT%\System32.|
|msodbcsqlr17.rll o <br/> msodbcsqlr13.rll o <br/> msodbcsqlr11.rll|File di risorse associato per la libreria del driver. Il file viene installato in %SYSTEMROOT%\System32\1033.| 
|s13ch_msodbcsql.chm o <br/> s11ch_msodbcsql.chm |File della Guida della Creazione guidata origine dati che illustra come creare un'origine dati per il driver. Il file viene installato in %SYSTEMROOT%\System32\1033 <br /> <br /> **NOTA** Non esistono file chm per ODBC Driver 17. |  
|msodbcsql.h|File di intestazione che contiene tutte le nuove definizioni necessarie per usare il driver.<br /><br /> **Nota:**  non è possibile fare riferimento a msodbcsql.h e a odbcss.h nello stesso programma.<br /><br /> msodbcsql.h per ODBC Driver 17 o 13 viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK. <br /> msodbcsql.h per ODBC Driver 11 viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.| 
|msodbcsql17.lib o <br/> msodbcsql13.lib o <br/> msodbcsql11.lib|File di libreria necessario per chiamare le funzioni dell'utilità **bcp** che fanno parte del driver.<br /><br /> **Nota:**  se si fa riferimento a questo file di libreria nel programma, assicurarsi che il file sia presente nel percorso di sistema e in quello degli utenti che usano l'applicazione.<br /><br /> msodbcsql17.lib o msodbcsql13.lib viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK.<br /> msodbcsql11.lib viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vedere anche

[Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
