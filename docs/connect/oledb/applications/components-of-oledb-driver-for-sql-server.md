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
ms.openlocfilehash: c88ef12d636dd5b10e1b7b3cd9418df3e058325b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007050"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componenti del driver OLE DB per SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver per SQL Server contiene i componenti seguenti:  

|Componente|Descrizione|  
|---------------|-----------------|  
|msoledbsql.dll|File DLL che contiene tutte le funzionalità di OLE DB Driver per SQL Server.|  
|msoledbsqlr.rll|File di risorse associato per la libreria di OLE DB Driver per SQL Server.|   
|msoledbsql.h|File di intestazione di OLE DB Driver per SQL Server che contiene tutte le nuove definizioni necessarie per usare OLE DB Driver per SQL Server. Questo file di intestazione sostituisce il file di intestazione sqloledb.h.<br /><br /> Nota: è possibile fare riferimento a msoledbsql.h e a sqloledb.h nello stesso programma purché sqloledb.h venga definito per primo.|  
|msoledbsql.lib|File di libreria necessario per chiamare direttamente la funzione [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) che fa parte di OLE DB Driver per SQL Server.<br /><br /> Nota: se si fa riferimento al file msoledbsql.lib nel codice di programmazione, è necessario assicurarsi che il file msoledbsql.dll si trovi nel proprio percorso di sistema e in quello degli utenti che usano l'applicazione.|  

## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con il driver OLE DB per SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
