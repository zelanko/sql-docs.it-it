---
title: Criteri di supporto per OLE DB Driver for SQL Server | Microsoft Docs
description: Criteri di supporto per driver OLE DB per SQL Server
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 1ae0e332de1d1e673cfd4fff1e288acafa4a0619
ms.sourcegitcommit: b016c01c47bc08351d093a59448d895cc170f8c3
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 09/19/2019
ms.locfileid: "71118144"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Criteri di supporto per driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Questo articolo illustra il modo in cui i vari componenti di accesso ai dati possono essere usati con OLE DB driver per SQL Server.  

## <a name="server-support"></a>Supporto server  
 OLE DB driver per SQL Server supporta le connessioni [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]a [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)], [!INCLUDE[ssSQL15](../../../includes/sssql15-md.md)], [!INCLUDE[ssSQL17](../../../includes/sssql17-md.md)], e [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versioni di sistema operativo supportate  
 Nella tabella seguente sono elencati i sistemi operativi che supportano OLE DB driver per SQL Server.  

| Sistemi operativi supportati |  |
|--------------------------------------|---------------------------------|   
| Aggiornamento + di Microsoft Windows 8.1 + [aprile 2014](https://go.microsoft.com/fwlink/?linkid=2073785)[KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [aprile 2014 aggiornamento](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016<br /><br />Microsoft Windows Server 2019 |  |


## <a name="ado-support-policies"></a>Criteri di supporto ADO  
 Le applicazioni ADO possono usare il provider OLE DB SQLOLEDB incluso in Windows se non richiedono alcuna funzionalità di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva.  

 Le applicazioni ADO possono utilizzare il driver OLE DB per SQL Server, ma in tal caso devono specificare `DataTypeCompatibility=80` nelle stringhe di connessione. Se nelle stringhe di connessione è presente `DataTypeCompatibility=80`, sono disponibili solo le funzionalità di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

## <a name="ole-db-support-policies"></a>Criteri di supporto OLE DB  
Le applicazioni possono usare il provider OLE DB (SQLOLEDB) incluso con il sistema operativo Windows. Tuttavia, si trova in modalità di manutenzione e non viene più aggiornato. Usare invece il driver OLE DB per SQL Server (MSOLEDBSQL).

## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con OLE DB Driver for SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
