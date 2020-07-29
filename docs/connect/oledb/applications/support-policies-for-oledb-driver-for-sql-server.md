---
title: Criteri di supporto per OLE DB Driver for SQL Server | Microsoft Docs
description: Criteri di supporto per driver OLE DB per SQL Server
ms.date: 05/25/2020
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.custom: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7e4b77a700d494f1ed8f11a0004c60b37c5cc361
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007040"
---
# <a name="support-policies-for-ole-db-driver-for-sql-server"></a>Criteri di supporto per driver OLE DB per SQL Server
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Questo articolo illustra come i vari componenti di accesso ai dati possono essere usati con OLE DB Driver per SQL Server.  

## <a name="sql-version-support"></a>Supporto delle versioni SQL  

OLE DB Driver per SQL Server viene testato con e supporta le connessioni alle versioni seguenti di SQL Server.

| Versione driver | database SQL di Azure | Azure SQL DW | Istanza gestita di SQL di Azure | SQL Server 2019 | SQL Server 2017 | SQL Server 2016 | SQL Server 2014 | SQL Server 2012 |
|----|-|-|-|-|-|-|-|-|
|18.4|S|S|S|S|S|S|S|S|
|18.3|S|S|S|S|S|S|S|S|
|18.2|S|S|S|S|S|S|S|S|
|18.1|S|S|S| |S|S|S|S|
|18.0|S|S|S| |S|S|S|S|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

## <a name="supported-operating-system-versions"></a>Versioni di sistema operativo supportate  

Nella tabella seguente sono elencati i sistemi operativi supportati da OLE DB Driver per SQL Server.  

| Versione driver | Windows Server 2019 | Windows Server 2016 | Windows Server 2012<sup>1</sup> | Windows Server 2012 R2<sup>2</sup> | Windows 10 | Windows 8.1<sup>3</sup> |
|----|-|-|-|-|-|-|
|18.4|S|S|S|S|S|S|
|18.3|S|S|S|S|S|S|
|18.2|S|S|S|S|S|S|
|18.1| |S|S|S|S|S|
|18.0| |S|S|S|S|S|
| &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; | &nbsp; |

<sup>1</sup> Supportato in Windows Server 2012 con [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061).  
<sup>2</sup> Supportato in Windows Server 2012 R2 con l'[aggiornamento di aprile 2014](https://go.microsoft.com/fwlink/?linkid=2073785) e [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061).  
<sup>3</sup> Supportato in Windows 8.1 con l'[aggiornamento di aprile 2014](https://go.microsoft.com/fwlink/?linkid=2073785) e [KB2999226](https://go.microsoft.com/fwlink/?linkid=2074061).  

## <a name="ado-support-policies"></a>Criteri di supporto ADO  

Le applicazioni ADO possono usare il provider OLE DB SQLOLEDB incluso in Windows se non richiedono alcuna funzionalità di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o versione successiva.  

Le applicazioni ADO possono usare OLE DB Driver per SQL Server. In tal caso è tuttavia necessario che sia specificato `DataTypeCompatibility=80` nelle stringhe di connessione. Se nelle stringhe di connessione è presente `DataTypeCompatibility=80`, sono disponibili solo le funzionalità di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)].  

## <a name="ole-db-support-policies"></a>Criteri di supporto OLE DB  

Le applicazioni possono usare il provider OLE DB (SQLOLEDB) incluso con il sistema operativo Windows. Questo provider è tuttavia in modalità manutenzione e non viene più aggiornato. Usare invece OLE DB Driver per SQL Server (MSOLEDBSQL).

## <a name="see-also"></a>Vedere anche  

[Compilazione di applicazioni con OLE DB Driver for SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)
