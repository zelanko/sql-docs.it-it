---
title: Criteri di supporto per OLE DB Driver for SQL Server | Microsoft Docs
description: Criteri di supporto per driver OLE DB per SQL Server
ms.date: 10/11/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b02789c787266a3370e3c5c9bfae50ea337d19db
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "72381856"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Criteri di supporto per driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Questo articolo illustra come i vari componenti di accesso ai dati possono essere usati con OLE DB Driver per SQL Server.  

## <a name="server-support"></a>Supporto server  
 OLE DB Driver per SQL Server supporta le connessioni alle versioni comprese tra [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] e [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] e ad [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

## <a name="supported-operating-system-versions"></a>Versioni di sistema operativo supportate  
 Nella tabella seguente sono elencati i sistemi operativi supportati da OLE DB Driver per SQL Server.  

| Sistemi operativi supportati |  |
|--------------------------------------|---------------------------------|   
| Microsoft Windows 8.1 + [aggiornamento di aprile 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows 10<br /><br /> Microsoft Windows Server 2012 + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2012 R2 + [aggiornamento di aprile 2014](https://go.microsoft.com/fwlink/?linkid=2073785) + [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061)<br /><br />Microsoft Windows Server 2016<br /><br />Microsoft Windows Server 2019 |  |


## <a name="ado-support-policies"></a>Criteri di supporto ADO  
 Le applicazioni ADO possono usare il provider OLE DB SQLOLEDB incluso in Windows se non richiedono alcuna funzionalità di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva.  

 Le applicazioni ADO possono usare OLE DB Driver per SQL Server. In tal caso è tuttavia necessario che sia specificato `DataTypeCompatibility=80` nelle stringhe di connessione. Se nelle stringhe di connessione è presente `DataTypeCompatibility=80`, sono disponibili solo le funzionalità di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

## <a name="ole-db-support-policies"></a>Criteri di supporto OLE DB  
Le applicazioni possono usare il provider OLE DB (SQLOLEDB) incluso con il sistema operativo Windows. Questo provider è tuttavia in modalità manutenzione e non viene più aggiornato. Usare invece OLE DB Driver per SQL Server (MSOLEDBSQL).

## <a name="see-also"></a>Vedere anche  
 [Compilazione di applicazioni con OLE DB Driver for SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)   
