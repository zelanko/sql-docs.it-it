---
title: Requisiti di sistema, installazione e file del driver | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6ab9a4035e3a714e6725f28f7e4e370bf3fd0119
ms.sourcegitcommit: 82b70c39550402a2b0b327db32bf5ecf88b50d3c
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 10/29/2019
ms.locfileid: "73032992"
---
# <a name="system-requirements-installation-and-driver-files"></a>Requisiti di sistema, installazione e file del driver

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

In questo articolo vengono illustrati i driver ODBC che si connettono a SQL Server.

## <a name="driver-versions"></a>Versioni dei driver

| Versione driver | Descrizione del supporto |
| :------------- | :--------------------- |
| Driver ODBC 11 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | Supporta le connessioni a SQL Server 2014, SQL Server 2012, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]e [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. |
| Driver ODBC 11 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows | Può essere installato in un computer che dispone anche di una o più versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. |
| ODBC driver 13 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | Supporta le connessioni a SQL Server 2016, SQL Server 2014, SQL Server 2012, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)]e [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)]. |
| Driver ODBC 13,1 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], <br/> Oltre ai precedenti per 13 | Supporta SQL Server 2017. |
| Driver ODBC 17 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] | Supporta le stesse versioni di database di 13,1. |
| ODBC Driver 17 for SQL Server | Supporta SQL Server 2019 a partire dalla versione del driver 17,3. |
| &nbsp; | &nbsp; |

### <a name="connection-string-details"></a>Dettagli stringa di connessione

Il nome del driver specificato in una stringa di connessione è `ODBC Driver 11 for SQL Server` o `ODBC Driver 13 for SQL Server` (sia per 13 che per 13,1) o `ODBC Driver 17 for SQL Server`.

## <a name="supported-operating-systems"></a>Sistemi operativi supportati

È possibile eseguire applicazioni con il driver nei sistemi operativi Windows seguenti:  

- Windows Server 2008 R2
- Windows Server 2012
- Windows Server 2012 R2
- Windows Server 2016
- Windows Vista SP2 &nbsp; _(solo driver ODBC 11)._
- Windows 7
- Windows 8
- Windows 8.1
- Windows 10

## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Installazione di Microsoft ODBC Driver for SQL Server

Il driver viene installato quando si esegue `msodbcsql.msi` da uno dei collegamenti seguenti:

- [Download di Microsoft ODBC Driver 17 for SQL Server in Windows](https://www.microsoft.com/download/details.aspx?id=56567)
- [Download di Microsoft ODBC Driver 13.1 for SQL Server in Windows](https://www.microsoft.com/download/details.aspx?id=53339)
- [Download di Microsoft ODBC Driver 13 for SQL Server in Windows](https://www.microsoft.com/download/details.aspx?id=50420)
- [Download di Microsoft ODBC Driver 11 for SQL Server in Windows](https://www.microsoft.com/download/details.aspx?id=36434)

> [!NOTE]
> Per coloro che hanno installato driver 17.1.0.1 o versione successiva, è consigliabile disinstallarli manualmente prima di installare la versione più recente del driver.

### <a name="side-by-side-with-native-client"></a>Side-by-side con Native Client

Il driver ODBC può essere installato side-by-side con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.

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

Nell'esempio seguente viene illustrato come eseguire una disinstallazione invisibile all'utente.
  
```console
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  

### <a name="indicate-dependency"></a>Indicare la dipendenza

Quando un'applicazione usa il driver, deve indicare che dipende da questo tramite l'opzione di installazione `APPGUID`. Questa indicazione consente al programma di installazione del driver di segnalare le applicazioni dipendenti prima della disinstallazione. Per specificare una dipendenza dal driver, impostare il parametro della riga di comando `APPGUID` sul codice prodotto al momento di eseguire l'installazione invisibile all'utente del driver. Quando si utilizza Microsoft Installer per aggregare il programma di installazione dell'applicazione, è necessario creare un codice prodotto. Ecco un esempio.
  
```console
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Strumenti da riga di comando: sqlcmd.exe e bcp.exe

È possibile scaricare gli strumenti `bcp.exe` e `sqlcmd.exe` per l'utilizzo con il driver [microsoft Command line utilities 11 per SQL Server](https://www.microsoft.com/download/details.aspx?id=36433), [Microsoft Command Line Utilities 13 per SQL Server](https://www.microsoft.com/download/details.aspx?id=52680)o [Microsoft Command line utilities 13,1 per SQL Server ](https://www.microsoft.com/download/details.aspx?id=53591). Il driver è un prerequisito per l'installazione di `sqlcmd.exe` e `bcp.exe`.
  
`bcp.exe` e `sqlcmd.exe` sono installati nella sottocartella `110\Tools` di `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` per la versione 11 e `130\Tools` per 13 e 13,1.

Il driver specificato in un'applicazione che usa funzioni BCP deve essere della stessa versione fornita con il file di intestazione e la libreria usati per compilare l'applicazione stessa.  

Ad esempio, quando si compila un'applicazione ODBC con `msodbcsql11.lib` e `msodbcsql.h`, utilizzare "DRIVER = {ODBC driver 11 for SQL Server}" nella stringa di connessione.

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Componenti di Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows

Il driver ODBC in Windows contiene i componenti seguenti:

| Componente | Descrizione |
| :-------- | :---------- |
|msodbcsql17.dll o <br/> msodbcsql13.dll o <br/> msodbcsql11.dll|File della DLL (Dynamic-Link Library, libreria di collegamento dinamico) che contiene tutte le funzionalità del driver. Questo file è installato in%SYSTEMROOT%\System32.|  
|msodbcdiag17. dll o <br/> msodbcdiag13. dll o <br/> msodbcdiag11.dll|File DLL (Dynamic-Link Library) che contiene l'interfaccia di diagnostica (traccia) del driver. Questo file è installato in%SYSTEMROOT%\System32.|
|msodbcsqlr17.rll o <br/> msodbcsqlr13.rll o <br/> msodbcsqlr11.rll|File di risorse associato per la libreria del driver. Questo file è installato in%SYSTEMROOT%\System32\1033.| 
|s13ch_msodbcsql.chm o <br/> s11ch_msodbcsql.chm |File della Guida della Creazione guidata origine dati che illustra come creare un'origine dati per il driver. Questo file è installato in%SYSTEMROOT%\System32\1033 <br /> <br /> **Nota:** Nessun file chm per il driver ODBC 17. |  
|msodbcsql.h|File di intestazione che contiene tutte le nuove definizioni necessarie per usare il driver.<br /><br /> **Nota:**  non è possibile fare riferimento a msodbcsql.h e odbcss.h nello stesso programma.<br /><br /> msodbcsql.h per ODBC Driver 17 o 13 viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK. <br /> msodbcsql.h per ODBC Driver 11 viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.| 
|msodbcsql17.lib o <br/> msodbcsql13.lib o <br/> msodbcsql11.lib|File di libreria necessario per chiamare le funzioni dell'utilità **bcp** che fanno parte del driver.<br /><br /> **Nota:** se si fa riferimento a questo file di libreria nel programma, assicurarsi che questo sia presente nel percorso di sistema e in quello degli utenti che usano l'applicazione.<br /><br /> msodbcsql17.lib o msodbcsql13.lib viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK.<br /> msodbcsql11.lib viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.|
| &nbsp; | &nbsp; |

## <a name="see-also"></a>Vedere anche

[Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
