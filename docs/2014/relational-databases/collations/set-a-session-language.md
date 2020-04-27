---
title: Impostare una lingua di sessione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [SQL Server], international considerations
- globalization [SQL Server], sessions
- time [SQL Server]
- sessions [SQL Server], languages
- international considerations [SQL Server], sessions
- dates [SQL Server], session languages
- global considerations [SQL Server], sessions
- client-side session language
- time [SQL Server], session languages
- messages [SQL Server], international considerations
- server-side session language
ms.assetid: de7f2c90-8f4f-4cfc-94cc-4933a7fd2bde
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf4eb1d7595d16369a0355562f090b746a4203ca
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62918942"
---
# <a name="set-a-session-language"></a>Impostazione di una lingua di sessione
  È possibile utilizzare la lingua di sessione per impostare la modalità di visualizzazione degli elementi seguenti nel server, in base a preferenze linguistiche e impostazioni locali:  
  
-   Lingua che verrà utilizzata per messaggi di errore e altri messaggi di sistema. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta più copie di tutte le stringhe di errore e dei messaggi del sistema in tutte le lingue in cui è disponibile [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questi messaggi possono essere visualizzati nella vista del catalogo [sys.messages](/sql/relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages) . Quando si installa una versione localizzata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], questi messaggi di sistema vengono tradotti nella lingua della versione installata. Per impostazione predefinita, è disponibile anche il set dei messaggi in inglese (Stati Uniti). È inoltre possibile aggiungere messaggi definiti dall'utente in una lingua specifica usando [sp_addmessage](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql).  
  
-   Il formato di data e ora.  
  
-   I nomi dei giorni e dei mesi, incluse le abbreviazioni.  
  
-   Il primo giorno della settimana.  
  
-   Le informazioni di valuta.  
  
 Sono disponibili 33 lingue per le impostazioni di sessione. Per un elenco completo, vedere [sys.syslanguages](/sql/relational-databases/system-compatibility-views/sys-syslanguages-transact-sql).  
  
## <a name="setting-the-session-language-from-the-server"></a>Impostazione della lingua di sessione dal server  
 Per impostare la lingua di sessione dal lato server, utilizzare l'istruzione [SET LANGUAGE](/sql/t-sql/statements/set-language-transact-sql).  
  
## <a name="setting-the-session-language-from-the-client"></a>Impostazione della lingua di sessione dal client  
 È possibile impostare la lingua di sessione dal client utilizzando OLE DB, ODBC o ADO.NET. Per OLE DB, utilizzare la proprietà SSPROP_INIT_CURRENTLANGUAGE. Per altre informazioni, vedere [Proprietà di inizializzazione e di autorizzazione](../native-client-ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
 Per ODBC, utilizzare la parola chiave Language. Per altre informazioni, vedere [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md).  
  
 Per ADO.NET, usare il parametro **Current Language** dell'oggetto **ConnectionString** . Per ulteriori informazioni, vedere la documentazione relativa al Software Development Kit (SDK) di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Data Access Components (MDAC).  
  
  
