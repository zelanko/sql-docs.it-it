---
title: Requisiti di sistema, installazione e file del driver | Microsoft Docs
ms.custom: ''
ms.date: 02/14/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: d90fa182-1dab-4d6f-bd85-a04dd1479986
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dd37c097873b104f3f53e9ca92e50b6f7c1acafe
ms.sourcegitcommit: 4cf0fafe565b31262e4148b572efd72c2a632241
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/21/2019
ms.locfileid: "56464767"
---
# <a name="system-requirements-installation-and-driver-files"></a>Requisiti di sistema, installazione e file del driver
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta connessioni a SQL Server 2014, SQL Server 2012, [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai_md.md)] e [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
In Windows è possibile installare ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in un computer che dispone anche di una o più versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  
  
ODBC Driver 13 e 13.1 per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], inoltre, supporta SQL Server 2016. 

ODBC Driver 17 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta tutti quelli precedenti e anche SQL Server 2017.
  
È il nome del driver specificato nella stringa di connessione `ODBC Driver 11 for SQL Server` oppure `ODBC Driver 13 for SQL Server` (per i 13 e 13.1) o `ODBC Driver 17 for SQL Server`.
  
## <a name="supported-operating-systems"></a>Sistemi operativi supportati

È possibile eseguire applicazioni con il driver nei sistemi operativi Windows seguenti:  

-   Windows Server 2008 R2 
-   Windows Server 2012
-   Windows Server 2012 R2    
-   Windows Vista SP2 *(Driver ODBC 11 solo)*  
-   Windows 7  
-   Windows 8
-   Windows 8.1
-   Windows 10
  
## <a name="installing-microsoft-odbc-driver-for-sql-server"></a>Installazione di Microsoft ODBC Driver for SQL Server

Il driver è installato quando si esegue `msodbcsql.msi` da uno dei collegamenti seguenti:

- [Download di Microsoft ODBC Driver 17 for SQL Server in Windows](https://www.microsoft.com/download/details.aspx?id=56567)
- [Download di Microsoft ODBC Driver 13.1 for SQL Server in Windows](https://www.microsoft.com/download/details.aspx?id=53339)
- [Download di Microsoft ODBC Driver 13 for SQL Server in Windows](https://www.microsoft.com/download/details.aspx?id=50420)
- [Download di Microsoft ODBC Driver 11 for SQL Server in Windows](https://www.microsoft.com/download/details.aspx?id=36434). 

> [!NOTE]
> Per coloro che dispongono di Driver 17.1.0.1 o seguito installato, è consigliabile che essere disinstallata manualmente prima di installare la versione più recente del Driver

Può essere installato side-by-side con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.  

Quando si chiama `msodbcsql.msi`, solo i componenti client vengono installati per impostazione predefinita. I componenti client sono file che supportano l'esecuzione di un'applicazione sviluppata tramite il driver. Per installare i componenti dell'SDK, specificare `ADDLOCAL=ALL` nella riga di comando. Ad esempio  
  
```  
msiexec /i msodbcsql.msi ADDLOCAL=ALL  
```  
  
 Specificare `IACCEPTMSODBCSQLLICENSETERMS=YES` per accettare le condizioni di licenza per l'utente finale se si usa l'opzione di installazione `/passive`, `/qn`, `/qb` o `/qr`. È necessario specificare questa opzione in lettere maiuscole. Ad esempio  
  
```  
msiexec /quiet /passive /qn /i msodbcsql.msi IACCEPTMSODBCSQLLICENSETERMS=YES ADDLOCAL=ALL  
```  
  
 Per eseguire una disinstallazione invisibile all'utente:  
  
```  
msiexec /quiet /passive /qn /uninstall msodbcsql.msi  
```  
  
Quando un'applicazione usa il driver, deve indicare che dipende da questo tramite l'opzione di installazione `APPGUID`. In questo modo il programma di installazione del driver è in grado di segnalare le applicazioni dipendenti prima della disinstallazione. Per specificare una dipendenza dal driver, impostare il parametro della riga di comando `APPGUID` sul codice prodotto al momento di eseguire l'installazione invisibile all'utente del driver. Quando si usa Microsoft Installer per aggregare il programma di installazione dell'applicazione, è necessario creare un codice prodotto. Ad esempio  
  
```  
msiexec /i msodbcsql.msi APPGUID={ <Your dependent application's APPGUID> }  
```  

## <a name="command-line-tools-sqlcmdexe-and-bcpexe"></a>Strumenti da riga di comando: sqlcmd.exe e bcp.exe

Il `bcp.exe` e `sqlcmd.exe` gli strumenti per l'uso con il driver può essere scaricato da [Microsoft Command Line Utilities 11 for SQL Server](https://www.microsoft.com/download/details.aspx?id=36433), [13 utilità della riga di comando di Microsoft per SQL Server](https://www.microsoft.com/download/details.aspx?id=52680), o [Microsoft Command Line Utilities 13.1 per SQL Server](https://www.microsoft.com/download/details.aspx?id=53591). Il driver è un prerequisito per l'installazione `sqlcmd.exe` e `bcp.exe`.
  
`bcp.exe` e `sqlcmd.exe` installate nel `110\Tools` sottocartella della `%PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC` per la versione 11, e `130\Tools` per 13 e 13.1.

Il driver specificato in un'applicazione che usa funzioni BCP deve essere della stessa versione fornita con il file di intestazione e la libreria usati per compilare l'applicazione stessa.  

Ad esempio, quando si compila un'applicazione ODBC con `msodbcsql11.lib` e `msodbcsql.h`, usare "DRIVER = {ODBC Driver 11 for SQL Server}" nella stringa di connessione.

## <a name="components-of-the-microsoft-odbc-driver-for-includessnoversionincludesssnoversion-mdmd-on-windows"></a>Componenti di Microsoft ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in Windows 
 Il driver ODBC in Windows contiene i componenti seguenti:
 
|Componente|Descrizione|  
|---------------|-----------------|  
|msodbcsql17.dll o <br> msodbcsql13.dll o <br> msodbcsql11.dll|File della DLL (Dynamic-Link Library, libreria di collegamento dinamico) che contiene tutte le funzionalità del driver. Questo file viene installato in % SYSTEMROOT%\System32.|  
|msodbcdiag17.dll o <br> msodbcdiag13.dll o <br> msodbcdiag11.dll|Il file di libreria di collegamento dinamico (DLL) che contiene l'interfaccia di diagnostica (traccia) del driver. Questo file viene installato in % SYSTEMROOT%\System32.|
|msodbcsqlr17.rll o <br> msodbcsqlr13.rll o <br> msodbcsqlr11.rll|File di risorse associato per la libreria del driver. Questo file viene installato in % SYSTEMROOT%\System32\1033.| 
|s13ch_msodbcsql.chm o <br> s11ch_msodbcsql.chm |File della Guida della Creazione guidata origine dati che illustra come creare un'origine dati per il driver. Questo file viene installato in %SYSTEMROOT%\System32\1033 <br /> <br /> **Nota:** è presente alcun file chm per ODBC Driver 17. |  
|msodbcsql.h|File di intestazione che contiene tutte le nuove definizioni necessarie per usare il driver.<br /><br /> **Nota:**  non è possibile fare riferimento a msodbcsql.h e odbcss.h nello stesso programma.<br /><br /> msodbcsql.h per ODBC Driver 17 o 13 viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK. <br /> msodbcsql.h per ODBC Driver 11 viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.| 
|msodbcsql17.lib o <br> msodbcsql13.lib o <br> msodbcsql11.lib|File di libreria necessario per chiamare le funzioni dell'utilità **bcp** che fanno parte del driver.<br /><br /> **Nota:** se si fa riferimento a questo file di libreria nel programma, assicurarsi che questo sia presente nel percorso di sistema e in quello degli utenti che usano l'applicazione.<br /><br /> msodbcsql17.lib o msodbcsql13.lib viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\130\SDK.<br /> msodbcsql11.lib viene installato in %PROGRAMFILES%\Microsoft SQL Server\Client SDK\ODBC\110\SDK.|

  
## <a name="see-also"></a>Vedere anche  
 [Microsoft ODBC Driver for SQL Server in Windows](../../../connect/odbc/windows/microsoft-odbc-driver-for-sql-server-on-windows.md)  
  
  
