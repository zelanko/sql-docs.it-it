---
title: Funzionalità di SQL Server deprecate in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 44fbab98aa017be66cd4dc369a713f44e8d248d5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "75228222"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>Funzionalità di SQL Server deprecate in SQL Server 2014
  In questo argomento vengono descritte le funzionalità deprecate ancora disponibili in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Tali funzionalità verranno rimosse a partire da una delle prossime versioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È consigliabile non usare le funzionalità deprecate nelle nuove applicazioni.  
  
## <a name="features-not-supported-in-the-next-version-of-ssnoversion"></a>Funzionalità non supportate nella prossima versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Le funzionalità riportate di seguito di [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] non saranno supportate nella prossima versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Non usare queste funzionalità in un nuovo progetto di sviluppo e modificare non appena possibile le applicazioni in cui sono attualmente implementate. La colonna Nome funzionalità viene visualizzata negli eventi di traccia come nome dell'oggetto, mentre nei contatori delle prestazioni e in sys.dm_os_performance_counters viene visualizzata come nome dell'istanza. L'ID della funzionalità viene visualizzato negli eventi di traccia come ObjectId.  
  
|Category|Funzionalità deprecata|Sostituzione|Nome funzionalità|ID funzionalità|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Programmabilità dei dati|[sys. soap_endpoints &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) o ASP.NET|Servizi Web XML nativi|22|  
|Programmabilità dei dati|[sys. endpoint_webmethods &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) o ASP.NET|Servizi Web XML nativi|23|  
  
### <a name="slipstream-functionality"></a>Funzionalità di integrazione  
 La [funzionalità di aggiornamento del prodotto](/previous-versions/sql/sql-server-2012/hh231670(v=sql.110)?redirectedfrom=MSDN) è stata introdotta in SQL Server 2012 come estensione della funzionalità di integrazione disponibile [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] in PCU1. In SQL Server 2014, la funzionalità di aggiornamento del prodotto è il metodo consigliato da usare per l'integrazione di SQL Server. Pertanto, i parametri della riga di comando,/*PCUSource* e/*CUSOURCE*, associati alla funzionalità di integrazione originale, non devono più essere utilizzati. Questi parametri continueranno a funzionare, ma potrebbero essere rimossi in una versione futura del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] programma di installazione. Il parametro consigliato da usare è/*UpdateSource* che combina la funzionalità dei parametri di integrazione originali,/*PCUSource* e/*CUSOURCE*.  
  
 Per ulteriori informazioni sulla funzionalità di integrazione disponibile in [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1, vedere la pagina relativa all' [installazione integrata di un SQL Server aggiornamento](https://go.microsoft.com/fwlink/?LinkId=219945) (.https://go.microsoft.com/fwlink/?LinkId=219945)  
 Per informazioni su come usare/*UpdateSource* per integrare SQL Server compilazioni, vedere gli argomenti seguenti:
 
 - [Come applicare la patch SQL Server installazione di 2012 con un pacchetto di installazione aggiornato (usando UpdateSource per ottenere una configurazione intelligente)](https://blogs.msdn.microsoft.com/jason_howell/2012/08/28/how-to-patch-sql-server-2012-setup-with-an-updated-setup-package-using-updatesource-to-get-a-smart-setup/)
 
 - [Il programma di installazione di SQL Server 2012 è diventato più intelligente...](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2012-Setup-just-got-smarter-8230/ba-p/317440)
 
## <a name="see-also"></a>Vedere anche  
 [Compatibilità con le versioni precedenti](../../2014/getting-started/backward-compatibility.md)  
  
  
