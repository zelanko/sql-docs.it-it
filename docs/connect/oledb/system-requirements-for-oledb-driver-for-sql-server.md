---
title: Requisiti di sistema di OLE DB Driver for SQL Server | Microsoft Docs
description: Requisiti del driver OLE DB per SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- system requirements [OLE DB Driver for SQL Server]
- data access [OLE DB Driver for SQL Server], system requirements
- OLE DB Driver for SQL Server, system requirements
- MSOLEDBSQL, system requirements
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 6462901ba1e3e73ca8c0a4ca448d8bc689bd8868
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744431"
---
# <a name="system-requirements-for-ole-db-driver-for-sql-server"></a>Requisiti di sistema per driver OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Per usare le caratteristiche di accesso ai dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio MARS, è necessario verificare che sia installato il software indicato di seguito:  

-   Driver OLE DB per SQL Server nel client.  

-   Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul server.   

> [!NOTE]  
>  Assicurarsi di accedere con privilegi di amministratore prima di installare il software.  

## <a name="operating-system-requirements"></a>Requisiti del sistema operativo  
 Per un elenco di sistemi operativi che supportano i Driver OLE DB per SQL Server, vedere [criteri di supporto per Driver OLE DB per SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

 ## <a name="azure-active-directory-authentication-requirements"></a>Requisiti di autenticazione di Azure Active Directory  
 Quando si usano i metodi di autenticazione di Azure Active Directory con il driver OLE DB, assicurarsi che il [Active Directory Authentication Library per SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) sia stato installato. ADAL non è necessaria per altri metodi di autenticazione o operazioni di OLE DB.
Per altre informazioni vedere [Uso di Azure Active Directory](features/using-azure-active-directory.md).

## <a name="sql-server-requirements"></a>requisiti di SQL Server  
 Usare il Driver OLE DB per SQL Server per accedere ai dati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database, è necessario disporre di un'istanza [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installato.  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] supporta connessioni da tutte le versioni di MDAC, Windows Data Access Components e da tutte le versioni del driver OLE DB per SQL Server. Quando si stabilisce una connessione tra una versione client meno recente e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i tipi di dati del server non riconosciuti dal client vengono mappati a tipi compatibili con la versione client. Per altre informazioni, vedere [Compatibilità dei tipi di dati per le versioni client](#data-type-compatibility-for-client-versions).  

## <a name="cross-language-requirements"></a>Requisiti per lingue diverse  
 La versione in lingua inglese del Driver OLE DB per SQL Server è supportata in tutte le versioni localizzate dei sistemi operativi supportati. Le versioni localizzate del Driver OLE DB per SQL Server sono supportate nei sistemi operativi localizzati che sono nella stessa lingua di localizzata Driver OLE DB per la versione di SQL Server. Le versioni localizzate del driver OLE DB per SQL Server sono supportate anche in tutti i sistemi operativi in lingua inglese, purché siano installate le impostazioni nella lingua corrispondente.  

 Per gli aggiornamenti:  

-   Versioni in lingua inglese del Driver OLE DB per SQL Server possono essere aggiornate a qualsiasi versione localizzata del Driver OLE DB per SQL Server.  

-   Le versioni localizzate del Driver OLE DB per SQL Server possono essere aggiornate alle versioni localizzate del Driver OLE DB per SQL Server nella stessa lingua.  

-   Versione localizzata del Driver OLE DB per SQL Server può essere aggiornata alla versione in lingua inglese del Driver OLE DB per SQL Server.  

-   Impossibile aggiornare le versioni localizzate del Driver OLE DB per SQL Server a localizzata Driver OLE DB per le versioni di SQL Server di una lingua diversa.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilità dei tipi di dati per le versioni client  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il driver OLE DB per SQL Server eseguono il mapping dei nuovi tipi di dati a tipi di dati meno recenti compatibili con client di versioni precedenti, come illustrato nella tabella riportata di seguito.  

 Le applicazioni OLE DB e ADO possono utilizzare il **DataTypeCompatibility** parola chiave di stringa di connessione con il Driver OLE DB per SQL Server per il funzionamento con tipi di dati meno recenti. Se **DataTypeCompatibility=80**, i client OLE DB si connettono usando la versione del flusso TDS di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], anziché quella corrente. Ciò significa che per i tipi di dati di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive, la conversione alle versioni precedenti verrà eseguita dal server e non dal driver OLE DB per SQL Server. Significa inoltre che le caratteristiche disponibili nella connessione saranno limitate al set di funzionalità di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. I tentativi di usare nuovi tipi di dati o caratteristiche vengono rilevati il prima possibile nelle chiamate API e, anziché tentare di passare richieste non valide al server, vengono restituiti errori all'applicazione chiamante.   


 IDBInfo:: GetKeywords restituirà sempre un elenco di parole chiave che corrisponde alla versione del server per la connessione e non è influenzato **DataTypeCompatibility**.  

|Tipo di dati|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Driver OLE DB per SQL Server|Applicazioni OLE DB di Windows Data Access Components, MDAC e<br /><br /> Driver OLE DB per le applicazioni OLE DB per SQL Server con Datatypecompatibility=80 = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR definito dall'utente (\<= 8 Kb)|udt|udt|udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|varbinary|image|  
|ntext|varchar|varchar|varchar|Text|  
|nvarchar(max)|NVARCHAR|NVARCHAR|NVARCHAR|Ntext|  
|xml|xml|xml|xml|Ntext|  
|Tipo CLR definito dall'utente (> 8 KB)|varbinary|udt|udt|image|  
|Data|varchar|Data|Data|Varchar|  
|datetime2|varchar|datetime2|datetime2|Varchar|  
|datetimeoffset|varchar|datetimeoffset|datetimeoffset|Varchar|  
|time|varchar|time|time|Varchar|  

## <a name="see-also"></a>Vedere anche  
 [Driver OLE DB per SQL Server](../oledb/oledb-driver-for-sql-server.md)   
 [Installazione del driver OLE DB per SQL Server](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
