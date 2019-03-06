---
title: Driver Microsoft OLE DB per SQL Server | Microsoft Docs
description: Driver Microsoft OLE DB per SQL Server
ms.custom: ''
ms.date: 02/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 00be1d87dbc8ba071403722b7e575e5ab1c7a215
ms.sourcegitcommit: 958cffe9288cfe281280544b763c542ca4025684
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/23/2019
ms.locfileid: "56744571"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>Driver Microsoft OLE DB per SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  Driver OLE DB per SQL Server è una dati autonomo access application programming interface (API), usata per OLE DB, che è stato introdotto in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Driver OLE DB per SQL Server offre il driver OLE DB per SQL in un'unica libreria di collegamento dinamico (DLL). Fornisce inoltre nuove funzionalità che estendono quelle fornite da Windows Data Access Components (Windows DAC, applicazione livello dati, precedentemente noto come Microsoft Data Access Components o MDAC). È possibile usare il driver OLE DB per SQL Server per creare nuove applicazioni o per migliorare applicazioni esistenti al fine di sfruttare le nuove caratteristiche di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], ad esempio MARS (Multiple Active Result Set), tipi di dati definiti dall'utente (UDT), notifica delle query, isolamento dello snapshot e supporto del tipo di dati XML.  
  
> [!NOTE]  
>  Per un elenco delle differenze tra il Driver OLE DB per SQL Server e Windows DAC, oltre a informazioni sui problemi da considerare prima di aggiornare un'applicazione livello dati di Windows per Driver OLE DB per SQL Server, vedere [aggiornamento di un'applicazione al Driver OLE DB per SQL Server da MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md).  
  
 Il provider OLE DB del driver OLE DB per SQL Server può essere usato con i servizi principali OLE DB inclusi con Windows DAC (applicazione livello dati), ma non si tratta di un requisito obbligatorio. La scelta di usare o meno i servizi di base dipende dai requisiti dell'applicazione specifica (ad esempio se è richiesto il pool di connessioni).  
  
 Le applicazioni dati oggetto ADO (ActiveX) possono usare il Driver OLE DB per SQL Server, ma è consigliabile utilizzare ADO in combinazione con il **DataTypeCompatibility** parola chiave di stringa di connessione (o corrispondente  **DataSource** proprietà). Quando si usa il Driver OLE DB per SQL Server, le applicazioni ADO possono sfruttare le nuove caratteristiche introdotte in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] che sono disponibili tramite il Driver OLE DB per SQL Server tramite parole chiave delle stringhe di connessione o le proprietà OLE DB o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Per altre informazioni sull'uso di queste caratteristiche con ADO, vedere [utilizzo di ADO con il Driver OLE DB per SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
 Il driver OLE DB per SQL Server è stato progettato come metodo semplificato per ottenere l'accesso ai dati nativo in SQL Server tramite OLE DB o ODBC. Fornisce un modo per innovare e sviluppare nuove funzionalità di accesso di dati senza modificare i componenti di Windows dell'applicazione livello dati correnti, che ora fanno parte della piattaforma Microsoft Windows.  
  
 Anche se il driver OLE DB per SQL Server usa componenti di Windows DAC (applicazione livello dati), non dipende in modo esplicito da una determinata versione di Windows DAC. È possibile usare il Driver OLE DB per SQL Server con la versione dell'applicazione livello dati di Windows che viene installato con qualsiasi sistema operativo supportato dal Driver OLE DB per SQL Server.  

 ## <a name="different-generations-of-ole-db-drivers"></a>Diverse generazioni di driver OLE DB

Sono disponibili tre generazioni distinte di provider Microsoft OLE DB per SQL Server.

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1. Provider Microsoft OLE DB per SQL Server (SQLOLEDB)
Il [Provider Microsoft OLE DB per SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) viene ancora fornito come parte del [Windows Data Access Components](https://msdn.microsoft.com/library/ms692897.aspx). Non vengono mantenuta più e non è consigliabile usare il driver per i nuovi sviluppi.

### <a name="2-sql-server-native-client-snac"></a>2. SQL Server Native Client (SNAC)
A partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], il [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md) include un'interfaccia di provider OLE DB (SQLNCLI) ed è il provider OLE DB fornito con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] tramite [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].

Era [annunciate come deprecate nel 2011](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/) e non è consigliabile usare il driver per i nuovi sviluppi. Per altre informazioni sul ciclo di vita SNAC e i download disponibili, consultare [ciclo di vita SNAC spiegato](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/).

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3. Driver Microsoft OLE DB per SQL Server (MSOLEDBSQL)
OLE DB è stata [deprecata](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/) e rilasciato nel 2018.

Il nuovo provider OLE DB viene chiamato il Driver OLE DB Microsoft per SQL Server (MSOLEDBSQL). Il nuovo provider verrà aggiornato con le funzionalità server più recenti in futuro.

> [!NOTE]
> Per usare il nuovo Microsoft Driver OLE DB per SQL Server nelle applicazioni esistenti, è consigliabile convertire le stringhe di connessione da SQLOLEDB o SQLNCLI, a MSOLEDBSQL.
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Quando usare il driver OLE DB per SQL Server](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 Viene illustrato in che modo il driver OLE DB per SQL Server si integra con le tecnologie di accesso ai dati di Microsoft, viene presentato un confronto con Windows DAC (applicazione livello dati) e ADO.NET e vengono visualizzate informazioni utili per decidere quale tecnologia di accesso ai dati usare.  
  
 [Funzionalità di OLE DB Driver for SQL Server](../oledb/features/oledb-driver-for-sql-server-features.md )  
 Descrive le funzionalità supportate dal Driver OLE DB per SQL Server.  
  
 [Compilazione di applicazioni con OLE DB Driver for SQL Server](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 Viene presentata una panoramica dello sviluppo con il driver OLE DB per SQL Server, incluse le differenze rispetto a Windows DAC (applicazione livello dati), i componenti usati e la modalità di uso di ADO con questo prodotto.  
  
 Questa sezione illustra anche i Driver OLE DB per la distribuzione, incluse le procedure ridistribuire il Driver OLE DB per la libreria di SQL Server e installazione di SQL Server.  
  
 [Requisiti di sistema per OLE DB Driver for SQL Server](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 Descrive le risorse di sistema necessarie per l'utilizzo del Driver OLE DB per SQL Server.  
  
 [Programmazione con OLE DB Driver for SQL Server](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 Vengono fornite informazioni sull'utilizzo del Driver OLE DB per SQL Server.  
  
 [Ricerca di altre informazioni su OLE DB Driver for SQL Server](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 Fornisce risorse aggiuntive sul Driver OLE DB per SQL Server, inclusi i collegamenti a risorse esterne e istruzioni per ottenere assistenza.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento di un'applicazione da SQL Server 2005 Native Client](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [Procedure relative a OLE DB](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
