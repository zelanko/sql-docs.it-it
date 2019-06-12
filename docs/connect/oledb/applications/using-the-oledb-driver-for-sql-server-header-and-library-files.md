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
manager: jroth
ms.openlocfilehash: b188649e138dddfc7dd4fd9fe974d6ccf28cc904
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66777963"
---
# <a name="using-the-ole-db-driver-for-sql-server-header-and-library-files"></a>Uso dei file di intestazione e di libreria del driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il Driver OLE DB per intestazione SQL Server e i file di libreria vengono installati quando il Driver OLE DB per l'opzione di SQL Server SDK viene selezionato durante il processo di installazione. Quando si sviluppa un'applicazione, è importante copiare e installare nell'ambiente di sviluppo tutti i file necessari per lo sviluppo. Per altre informazioni sull'installazione e la ridistribuzione del Driver OLE DB per SQL Server, vedere [installazione di Driver OLE DB per SQL Server](../../oledb/applications/installing-oledb-driver-for-sql-server.md).  
  
 Il Driver OLE DB per intestazione SQL Server e i file di libreria vengono installati nel percorso seguente:  
  
 *%PROGRAM FILES%* \Microsoft SQL Server\Client SDK\OLEDB\182\SDK  
  
 Il Driver OLE DB per il file di intestazione di SQL Server (msoledbsql.h) utilizzabile per aggiungere Driver OLE DB per funzionalità di accesso ai dati di SQL Server alle applicazioni personalizzate. Il file di intestazione del driver OLE DB per SQL Server contiene tutte le definizioni, gli attributi, le proprietà e le interfacce necessari per usare le nuove funzionalità di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  
  
 Oltre il Driver OLE DB per il file di intestazione di SQL Server, è inoltre disponibile un file di libreria msoledbsql.lib, che rappresenta la libreria di esportazione per [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) funzionalità.  
  
 Il file di intestazione del driver OLE DB per SQL Server è compatibile con le versioni precedenti del file di intestazione sqloledb.h usato con Microsoft Data Access Components (MDAC) ma non contiene i CLSID per SQLOLEDB (il provider OLE DB per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incluso con MDAC) o simboli per la funzionalità XML (non supportata dal driver OLE DB per SQL Server).    
  
 Le applicazioni OLE DB che utilizzano il Driver OLE DB per SQL Server è necessario solo fare riferimento a msoledbsql.h. Se un'applicazione usa sia MDAC (SQLOLEDB) sia il driver OLE DB per SQL Server, può fare riferimento sia a sqloledb.h sia amsoledbsql.h, ma il primo riferimento deve essere a sqloledb.h.  
  
## <a name="using-the-ole-db-driver-for-sql-server-header-file"></a>Usa il Driver OLE DB per il file di intestazione di SQL Server  
 Per usare il Driver OLE DB per il file di intestazione di SQL Server, è necessario usare un **includere** istruzione all'interno del codice di programmazione C/C++. Le sezioni seguenti descrivono come eseguire questa operazione nelle applicazioni OLE DB.  
  
> [!NOTE]  
>  Il Driver OLE DB per i file di intestazione e di libreria di SQL Server può essere solo compilati usando Visual Studio C++ 2012 o versione successiva.  
  
### <a name="ole-db"></a>OLE DB  
 Per usare il Driver OLE DB per file di intestazione di SQL Server in un'applicazione OLE DB tramite le righe di codice di programmazione seguenti:  
  
```    
include "msoledbsql.h";  
```  
  
> [!NOTE]  
>  Se l'applicazione ha un **includono** istruzione per SQLOLEDB. h, il **includono** informativa per msoledbsql.h deve essere successiva.  
  
 Quando si crea una connessione a un'origine dati tramite il Driver OLE DB per SQL Server, usare "MSOLEDBSQL" come stringa del nome del provider.  

  
## <a name="component-names-and-properties-by-version"></a>Proprietà e nomi dei componenti per versione  

|Proprietà|Driver OLE DB per SQL Server|MDAC|  
|--------|----------------------------|----|   
|OLE DB PROGID|MSOLEDBSQL|SQLOLEDB|  
|Nome file di intestazione OLE DB|msoledbsql.h|Sqloledb.h|  
|DLL del provider OLE DB|msoledbsql.dll|Sqloledb.dll| 
  
  
## <a name="static-linking-and-bcp-functions"></a>Collegamento statico e funzioni BCP  
 Quando in un'applicazione vengono utilizzate funzioni BCP, è importante specificare nella stringa di connessione il driver della stessa versione fornita con il file di intestazione e la libreria utilizzati per compilare l'applicazione.  
  
 Per altre informazioni, vedere Performing [esecuzione di operazioni di copia Bulk](../../oledb/features/performing-bulk-copy-operations.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con il driver OLE DB per SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
