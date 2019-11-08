---
title: Requisiti di sistema per SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- system requirements [SQL Server Native Client]
- data access [SQL Server Native Client], system requirements
- SQL Server Native Client, system requirements
- SQLNCLI, system requirements
ms.assetid: 1c8e2f8a-a440-44da-8e3a-af632d34c52c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 85b00f00e2c557f31a7343a99e1f2592741a6b59
ms.sourcegitcommit: baa40306cada09e480b4c5ddb44ee8524307a2ab
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/06/2019
ms.locfileid: "73637791"
---
# <a name="system-requirements-for-sql-server-native-client"></a>Requisiti di sistema per SQL Server Native Client
  Per usare le caratteristiche di accesso ai dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ad esempio MARS, è necessario verificare che sia installato il software indicato di seguito:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sul client.  
  
-   Un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul server.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client richiede Windows Installer 3.0. Windows Installer 3.0 è già installato nei sistemi operativi [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Per tutte le altre piattaforme è necessario installarlo in modo esplicito. Per ulteriori informazioni, vedere [Windows Installer 3,0 Redistributable](https://www.microsoft.com/download/details.aspx?id=16821).  
  
> [!NOTE]  
>  Assicurarsi di accedere con privilegi di amministratore prima di installare il software.  
  
## <a name="operating-system-requirements"></a>Requisiti del sistema operativo  
 Per un elenco dei sistemi operativi che supportano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client, vedere [criteri di supporto per SQL Server Native Client](applications/support-policies-for-sql-server-native-client.md).  
  
## <a name="sql-server-requirements"></a>Requisiti di SQL Server  
 Per usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client per accedere ai dati nei database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario che sia installata un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] supporta connessioni da tutte le versioni di MDAC, Windows Data Access Components e tutte le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Quando si stabilisce una connessione tra una versione client meno recente e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i tipi di dati del server non riconosciuti dal client vengono mappati a tipi compatibili con la versione client. Per altre informazioni, vedere Compatibilità dei tipi di dati per le versioni client, più avanti in questo argomento.  
  
## <a name="cross-language-requirements"></a>Requisiti per lingue diverse  
 La versione in lingua inglese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è supportata in tutte le versioni localizzate dei sistemi operativi supportati. Le versioni localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sono supportate in tutti i sistemi operativi localizzati, purché della stessa lingua della versione localizzata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Le versioni localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client sono inoltre supportate in tutti i sistemi operativi in lingua inglese, purché siano installate le impostazioni nella lingua corrispondente.  
  
 Per gli aggiornamenti:  
  
-   Le versioni in lingua inglese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client possono essere aggiornate a qualsiasi versione localizzata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   Le versioni localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client possono essere aggiornate alle versioni localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client nella stessa lingua.  
  
-   Le versioni localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client possono essere aggiornate alla versione in lingua inglese di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
-   Le versioni localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client non possono essere aggiornate alle versioni localizzate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client in una lingua diversa.  
  
## <a name="data-type-compatibility-for-client-versions"></a>Compatibilità dei tipi di dati per le versioni client  
 In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client i nuovi tipi di dati vengono mappati a tipi di dati meno recenti compatibili con client di versioni precedenti, come illustrato nella tabella riportata di seguito.  
  
 Nelle applicazioni OLE DB e ADO è possibile usare la parola chiave della stringa di connessione `DataTypeCompatibility` con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client per l'utilizzo di tipi di dati di versioni precedenti. Se `DataTypeCompatibility=80`, i client OLE DB si connettono usando la versione del flusso TDS (Tabular Data Stream) di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], anziché quella corrente. Ciò significa che per i tipi di dati di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive, la conversione alle versioni precedenti verrà eseguita dal server e non da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Significa inoltre che le caratteristiche disponibili nella connessione saranno limitate al set di funzionalità di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. I tentativi di usare nuovi tipi di dati o caratteristiche vengono rilevati il prima possibile nelle chiamate API e, anziché tentare di passare richieste non valide al server, vengono restituiti errori all'applicazione chiamante.  
  
 Non sono presenti controlli `DataTypeCompatibility` per ODBC.  
  
 IDBInfo:: GetKeywords restituirà sempre un elenco di parole chiave che corrisponde alla versione del server nella connessione e non è interessato dalla `DataTypeCompatibility`.  
  
|Tipo di dati|SQL Server Native Client<br /><br /> SQL Server 2005|SQL Server Native Client 11.0<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|Applicazioni OLE DB di Windows Data Access Components, MDAC e<br /><br /> SQL Server Native Client con DataTypeCompatibility=80|  
|---------------|--------------------------------------------------|-------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|  
|CLR UDT (\<= 8Kb)|udt|Udt|Varbinary|  
|varbinary(max)|varbinary|varbinary|Immagine|  
|varchar(max)|varchar|varchar|Text|  
|nvarchar(max)|nvarchar|nvarchar|Ntext|  
|XML|XML|XML|Ntext|  
|UDT CLR (> 8Kb)|udt|varbinary|Immagine|  
|data|data|varchar|Varchar|  
|datetime2|datetime2|varchar|Varchar|  
|datetimeoffset|datetimeoffset|varchar|Varchar|  
|time|time|varchar|Varchar|  
  
## <a name="see-also"></a>Vedere anche  
 [Programmazione SQL Server Native Client](sql-server-native-client-programming.md)   
 [Installazione di SQL Server Native Client](applications/installing-sql-server-native-client.md)  
  
  
