---
title: Uso dei file di intestazione e di libreria del driver OLE DB per SQL Server | Microsoft Docs
description: Uso dei file di intestazione e di libreria del driver OLE DB per SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- header files [OLE DB Driver for SQL Server]
- MSOLEDBSQL, header files
- OLE DB, header files
- library files [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, header files
- data access [OLE DB Driver for SQL Server], header files
- data access [OLE DB Driver for SQL Server], library files
- OLE DB Driver for SQL Server, library files
- MSOLEDBSQL, library files
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 93b906a0604772fe224b1e63eaf6eed9eb8af983
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989230"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Uso dei file di intestazione e di libreria del driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il driver OLE DB per SQL Server i file di intestazione e di libreria vengono installati quando si seleziona l'opzione driver OLE DB per SQL Server SDK durante il processo di installazione. Quando si sviluppa un'applicazione, è importante copiare e installare nell'ambiente di sviluppo tutti i file necessari per lo sviluppo. Per ulteriori informazioni sull'installazione e la ridistribuzione di OLE DB driver per SQL Server, vedere [installazione di OLE DB driver per SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 Il driver OLE DB per i file di intestazione e di libreria di SQL Server vengono installati nel percorso seguente:  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 Il driver OLE DB per il file di intestazione SQL Server (msoledbsql. h) può essere usato per aggiungere OLE DB driver per la funzionalità di accesso ai dati SQL Server alle applicazioni personalizzate. Il file di intestazione del driver OLE DB per SQL Server contiene tutte le definizioni, gli attributi, le proprietà e le interfacce necessari per usare le nuove funzionalità di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Oltre al driver OLE DB per SQL Server file di intestazione, è disponibile anche un file di libreria msoledbsql. lib, ovvero la libreria di esportazione per la funzionalità [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) .  
  
 Il file di intestazione del driver OLE DB per SQL Server è compatibile con le versioni precedenti del file di intestazione sqloledb.h usato con Microsoft Data Access Components (MDAC) ma non contiene i CLSID per SQLOLEDB (il provider OLE DB per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluso con MDAC) o simboli per la funzionalità XML (non supportata dal driver OLE DB per SQL Server).    
  
 OLE DB le applicazioni che utilizzano il driver OLE DB per SQL Server devono solo fare riferimento a msoledbsql. h. Se un'applicazione usa sia MDAC (SQLOLEDB) sia il driver OLE DB per SQL Server, può fare riferimento sia a sqloledb.h sia amsoledbsql.h, ma il primo riferimento deve essere a sqloledb.h.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Uso del driver OLE DB per SQL Server file di intestazione  
 Per utilizzare il driver OLE DB per SQL Server file di intestazione, è necessario utilizzare un'istruzione **include** all'interno delC++ codice di programmazione C/. Nelle sezioni seguenti viene descritto come eseguire questa operazione nelle applicazioni OLE DB.  
  
> [!NOTE]  
>  Il driver OLE DB per i file di intestazione e di libreria SQL Server può essere compilato solo C++ con Visual Studio 2012 o versione successiva.  
  
### <a name="ole-db"></a>OLE DB  
 Per usare il driver OLE DB per SQL Server file di intestazione in un'applicazione OLE DB, usando le righe di codice di programmazione seguenti:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Se l'applicazione dispone di un'istruzione di **inclusione** per SQLOLEDB. h, l'istruzione **include** per msoledbsql. h deve essere successiva.  
  
 Quando si crea una connessione a un'origine dati tramite OLE DB driver per SQL Server, utilizzare "MSOLEDBSQL" come stringa del nome del provider.  

  
## <a name="component-names-and-properties-by-version"></a>Proprietà e nomi dei componenti per versione  

|Proprietà|Driver OLE DB per SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|Nome file di intestazione OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL del provider OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Collegamento statico e funzioni BCP  
 Quando in un'applicazione vengono utilizzate funzioni BCP, è importante specificare nella stringa di connessione il driver della stessa versione fornita con il file di intestazione e la libreria utilizzati per compilare l'applicazione.  
  
 Per ulteriori informazioni, vedere esecuzione di [operazioni di copia bulk](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con il driver OLE DB per SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
