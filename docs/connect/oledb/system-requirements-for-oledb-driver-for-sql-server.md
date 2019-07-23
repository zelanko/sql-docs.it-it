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
ms.openlocfilehash: cec8b2aca53f64e7a3883dbccddce1a330c8a6e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67993784"
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
 Per un elenco dei sistemi operativi che supportano OLE DB driver per SQL Server, vedere [criteri di supporto per OLE DB driver per SQL Server](../oledb/applications/support-policies-for-oledb-driver-for-sql-server.md).  

 ## <a name="azure-active-directory-authentication-requirements"></a>Requisiti di autenticazione di Azure Active Directory  
 Quando si usano Azure Active Directory metodi di autenticazione con il driver OLE DB, assicurarsi che sia stata installata la [Active Directory Authentication Library per SQL Server](https://go.microsoft.com/fwlink/?LinkID=513072) . ADAL non è necessario per gli altri metodi di autenticazione o OLE DB operazioni.
Per altre informazioni vedere [Uso di Azure Active Directory](features/using-azure-active-directory.md).

## <a name="sql-server-requirements"></a>requisiti di SQL Server  
 Per utilizzare OLE DB driver per SQL Server accedere ai dati nei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] database di, è necessario che sia installata [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] un'istanza di.  

 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] supporta connessioni da tutte le versioni di MDAC, Windows Data Access Components e da tutte le versioni del driver OLE DB per SQL Server. Quando si stabilisce una connessione tra una versione client meno recente e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i tipi di dati del server non riconosciuti dal client vengono mappati a tipi compatibili con la versione client. Per altre informazioni, vedere [Compatibilità dei tipi di dati per le versioni client](#data-type-compatibility-for-client-versions).  

## <a name="cross-language-requirements"></a>Requisiti per lingue diverse  
 La versione in lingua inglese di OLE DB driver per SQL Server è supportata in tutte le versioni localizzate dei sistemi operativi supportati. Le versioni localizzate del driver OLE DB per SQL Server sono supportate nei sistemi operativi localizzati che corrispondono alla stessa lingua del driver OLE DB localizzato per la versione SQL Server. Le versioni localizzate del driver OLE DB per SQL Server sono supportate anche in tutti i sistemi operativi in lingua inglese, purché siano installate le impostazioni nella lingua corrispondente.  

 Per gli aggiornamenti:  

-   È possibile aggiornare le versioni in lingua inglese del driver OLE DB per SQL Server a qualsiasi versione localizzata di OLE DB driver per SQL Server.  

-   Le versioni localizzate del driver OLE DB per SQL Server possono essere aggiornate alle versioni localizzate di OLE DB driver per SQL Server della stessa lingua.  

-   La versione localizzata del driver OLE DB per SQL Server può essere aggiornata alla versione in lingua inglese di OLE DB driver per SQL Server.  

-   Le versioni localizzate del driver OLE DB per SQL Server non possono essere aggiornate al driver di OLE DB localizzato per le versioni SQL Server di una lingua localizzata diversa.  

## <a name="data-type-compatibility-for-client-versions"></a>Compatibilità dei tipi di dati per le versioni client  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il driver OLE DB per SQL Server eseguono il mapping dei nuovi tipi di dati a tipi di dati meno recenti compatibili con client di versioni precedenti, come illustrato nella tabella riportata di seguito.  

 Le applicazioni OLE DB e ADO possono usare la parola chiave della stringa di connessione **DataTypeCompatibility** con OLE DB Driver per SQL Server di operare con i tipi di dati meno recenti. Se **DataTypeCompatibility=80**, i client OLE DB si connettono usando la versione del flusso TDS di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], anziché quella corrente. Ciò significa che per i tipi di dati di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive, la conversione alle versioni precedenti verrà eseguita dal server e non dal driver OLE DB per SQL Server. Significa inoltre che le caratteristiche disponibili nella connessione saranno limitate al set di funzionalità di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. I tentativi di usare nuovi tipi di dati o caratteristiche vengono rilevati il prima possibile nelle chiamate API e, anziché tentare di passare richieste non valide al server, vengono restituiti errori all'applicazione chiamante.   


 IDBInfo:: GetKeywords restituirà sempre un elenco di parole chiave che corrisponde alla versione del server nella connessione e non è influenzato da **DataTypeCompatibility**.  

|Tipo di dati|SQL Server Native Client<br /><br />SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Driver OLE DB per SQL Server|Applicazioni OLE DB di Windows Data Access Components, MDAC e<br /><br /> Driver OLE DB per SQL Server applicazioni OLE DB con DataTypeCompatibility = 80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|Tipo definito dall'utente CLR (\<= 8 KB)|udt|udt|udt|Varbinary|  
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
