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
ms.openlocfilehash: 5a5124519bd95ec02e93a007d9881ec80814cfc8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989326"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>Componenti del driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB driver per SQL Server contiene i componenti seguenti:  

|Componente|Descrizione|  
|---------------|-----------------|  
|msoledbsql.dll|Il file DLL (Dynamic-Link Library) che contiene tutti i driver di OLE DB per la funzionalità SQL Server.|  
|msoledbsqlr.rll|File di risorse associato per il driver OLE DB per la libreria di SQL Server.|   
|msoledbsql.h|Il driver OLE DB per SQL Server file di intestazione che contiene tutte le nuove definizioni necessarie per utilizzare OLE DB driver per SQL Server. Questo file di intestazione sostituisce il file di intestazione SQLOLEDB. h.<br /><br /> Nota: è possibile fare riferimento a msoledbsql. h e SQLOLEDB. h nello stesso programma purché venga definito prima SQLOLEDB. h.|  
|msoledbsql.lib|File di libreria necessario per chiamare direttamente la funzione [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) che fa parte del driver OLE DB per SQL Server.<br /><br /> Nota: se si fa riferimento al file msoledbsql.lib nel codice di programmazione, è necessario assicurarsi che il file msoledbsql.dll si trovi nel proprio percorso di sistema e in quello degli utenti che usano l'applicazione.|  

## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con il driver OLE DB per SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
