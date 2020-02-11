---
title: Uso dei file di intestazione e di libreria SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- header files [SQL Server Native Client]
- SQLNCLI, header files
- OLE DB, header files
- library files [SQL Server Native Client]
- SQL Server Native Client, header files
- data access [SQL Server Native Client], header files
- SQL Server Native Client ODBC driver,header files
- data access [SQL Server Native Client], library files
- SQL Server Native Client, library files
- ODBC applications, header files
- SQLNCLI, library files
ms.assetid: 69889a98-7740-4667-aecd-adfc0b37f6f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 800b3e43129bba36db0836f9a58a3ad1e47b40c1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63046288"
---
# <a name="using-the-sql-server-native-client-header-and-library-files"></a>Utilizzo dei file di intestazione e della libreria di SQL Server Native Client
  I file di intestazione e di libreria di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono installati con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Quando si sviluppa un'applicazione, è importante copiare e installare nell'ambiente di sviluppo tutti i file necessari per lo sviluppo. Per ulteriori informazioni sull'installazione e la ridistribuzione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di Native client, vedere [installazione di SQL Server Native Client](installing-sql-server-native-client.md).  
  
 I file di intestazione e di libreria di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client vengono installati nel percorso seguente:  
  
 *% Programmi%* \Microsoft SQL Server\110\SDK  
  
 Il file di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h) può essere utilizzato per aggiungere alle applicazioni personalizzate funzionalità di accesso ai dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Il file di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client contiene tutte le definizioni, gli attributi, le proprietà e le interfacce necessari per sfruttare le nuove caratteristiche introdotte in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Oltre al file di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, è presente anche un file di libreria sqlncli11.lib, che rappresenta la libreria di esportazione per la funzionalità del programma per la copia bulk (BCP, Bulk Copy Program) di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per ODBC.  
  
 Il file di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è compatibile con le versioni precedenti per i file di intestazione sqloledb.h e odbcss.h utilizzati con Microsoft Data Access Components (MDAC) ma non contiene i CLSID per SQLOLEDB (il provider OLE DB per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluso con MDAC) o simboli per la funzionalità XML (non supportata da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client).  
  
 Le applicazioni ODBC non possono fare riferimento all'intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (sqlncli.h) e a odbcss.h nello stesso programma. Anche se non si utilizzano le caratteristiche introdotte in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], potrà essere utilizzato il file di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in sostituzione del più obsoleto odbcss.h.@@@  
  
 Le applicazioni OLE DB che utilizzano il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client devono fare riferimento solo a sqlncli.h. Se un'applicazione utilizza sia MDAC (SQLOLEDB) sia il provider OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, può fare riferimento sia a sqloledb.h sia a sqlncli.h, ma il primo riferimento deve essere a sqloledb.h.  
  
## <a name="using-the-sql-server-native-client-header-file"></a>Utilizzo del file di intestazione di SQL Server Native Client  
 Per utilizzare il file di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, è necessario utilizzare un'istruzione `include` all'interno del codice di programmazione C/C++. Nelle sezioni seguenti viene descritto come eseguire questa operazione sia per le applicazioni OLE DB sia per le applicazioni ODBC.  
  
> [!NOTE]  
>  I file di intestazione e di libreria di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client possono essere compilati solo utilizzando Visual Studio C++ 2002 o versione successiva.  
  
### <a name="ole-db"></a>OLE DB  
 Per utilizzare i file di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in un'applicazione OLE DB utilizzando le righe di codice di programmazione seguenti:@@@  
  
```  
#define _SQLNCLI_OLEDB_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  La prima riga di codice sopra mostrata deve essere omessa se nell'applicazione vengono utilizzate API sia OLE DB che ODBC. Se inoltre nell'applicazione è presente un'istruzione `include` per sqloledb.h, l'istruzione `include` per sqlncli.h deve essere successiva.  
  
 Quando si crea una connessione a un'origine dati mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, utilizzare "SQLNCLI11" come stringa del nome del provider.  
  
### <a name="odbc"></a>ODBC  
 Per utilizzare il file di intestazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in un'applicazione ODBC, utilizzare le righe di codice di programmazione seguenti:  
  
```  
#define _SQLNCLI_ODBC_  
include "sqlncli.h";  
```  
  
> [!NOTE]  
>  La prima riga di codice sopra mostrata deve essere omessa se nell'applicazione vengono utilizzate sia le API OLE DB che ODBC. Se inoltre nell'applicazione è presente un'istruzione `#include` per odbcss.h, deve essere rimossa.  
  
 Quando si crea una connessione a un'origine dati mediante [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, utilizzare "SQL Server Native Client 11.0" come stringa del nome del driver.  
  
## <a name="component-names-and-properties-by-version"></a>Proprietà e nomi dei componenti per versione  
  
|Proprietà|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 10.0<br /><br /> SQL Server 2008|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]|MDAC|  
|--------------|--------------------------------------------------|-------------------------------------------------------|---------------------------------------------------------------|----------|  
|Nome driver ODBC|SQL Native Client|SQL Server Native Client 10.0|SQL Server Native Client 11.0|SQL Server|  
|Nome file di intestazione ODBC|Sqlncli.h|Sqlncli.h|Sqlncli.h|Odbcss.h|  
|DLL del driver ODBC|Sqlncli.dll|Sqlncl10.dll|Sqlncl11.dll|sqlsrv32.dll|  
|File di libreria ODBC per le API BCP|Sqlncli.lib|Sqlncli10.lib|Sqlncli11.lib|Odbcbcp.lib|  
|DLL ODBC per le API BCP|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Odbcbcp.dll|  
|OLE DB PROGID|SQLNCLI|SQLNCLI10|SQLNCLI11|SQLOLEDB|  
|Nome file di intestazione OLE DB|Sqlncli.h|Sqlncli.h|Sqlncli.h|Sqloledb.h|  
|DLL del provider OLE DB|Sqlncli.dll|Sqlncli10.dll|Sqlncli11.dll|Sqloledb.dll|  
  
 sqlncli.h supporta più versioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client grazie alla macro SQLNCLI_VER. Per impostazione predefinita, tramite SQLNCLI_VER viene utilizzata la versione più recente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Per compilare un'applicazione che utilizza sqlncli10.dll anziché sqlncli11.dll, impostare SQLNCLI_VER su 10.  
  
## <a name="static-linking-and-bcp-functions"></a>Collegamento statico e funzioni BCP  
 Quando in un'applicazione vengono utilizzate funzioni BCP, è importante specificare nella stringa di connessione il driver della stessa versione fornita con il file di intestazione e la libreria utilizzati per compilare l'applicazione.  
  
 Se ad esempio si compila un'applicazione utilizzando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, nonché il file di libreria (sqlncli11.lib) e il file di intestazione (sqlncli.h) associati presenti in \Programmi\Microsoft SQL Server\110\SDK, assicurarsi di specificare (utilizzando ODBC come esempio) "DRIVER={SQL Server Native Client 11.0}" nella stringa di connessione.  
  
 Per ulteriori informazioni, vedere esecuzione di [operazioni di copia bulk](../features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
