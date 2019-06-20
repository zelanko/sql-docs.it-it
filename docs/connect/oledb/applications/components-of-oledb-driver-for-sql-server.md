---
title: Componenti del driver OLE DB per SQL Server | Microsoft Docs
description: Componenti del driver OLE DB per SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 23b190bdeb478d5909ca235cf2801a98fb954e9c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800893"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componenti del driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Driver OLE DB per SQL Server contiene i componenti seguenti:  

|Componente|Descrizione|  
|---------------|-----------------|  
|msoledbsql.dll|Il file di libreria di collegamento dinamico (DLL) che contiene tutti i Driver OLE DB per la funzionalità di SQL Server.|  
|msoledbsqlr.rll|File di risorse associato per il Driver OLE DB per la libreria di SQL Server.|   
|msoledbsql.h|Il Driver OLE DB per il file di intestazione di SQL Server che contiene tutte le nuove definizioni necessarie per usare il Driver OLE DB per SQL Server. Questo file di intestazione sostituisce il file di intestazione SQLOLEDB. h.<br /><br /> Nota: È possibile fare riferimento msoledbsql.h e SQLOLEDB. h nello stesso programma, purché venga definito prima SQLOLEDB. h.|  
|msoledbsql.lib|Il file di libreria necessario per chiamare direttamente le [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) funzione che fa parte del Driver OLE DB per SQL Server.<br /><br /> Nota: se si fa riferimento al file msoledbsql.lib nel codice di programmazione, è necessario assicurarsi che il file msoledbsql.dll si trovi nel proprio percorso di sistema e in quello degli utenti che usano l'applicazione.|  

## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con il driver OLE DB per SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
