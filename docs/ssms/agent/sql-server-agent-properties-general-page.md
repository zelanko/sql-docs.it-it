---
title: Proprietà SQL Server Agent (pagina Generale)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.general.f1
ms.assetid: b51601e9-5454-43c6-bb5e-24eb2ff043c8
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: acc9737f55f0af9c4fc136474e6a9dcec247597a
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75234265"
---
# <a name="sql-server-agent-properties-general-page"></a>Proprietà SQL Server Agent (pagina Generale)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare le proprietà generali del servizio [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Stato del servizio**  
Visualizza lo stato corrente del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Riavvia automaticamente SQL Server in caso di arresto imprevisto**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esegue il riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] quando si verifica un arresto imprevisto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
**Riavvia automaticamente SQL Server Agent in caso di arresto imprevisto**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esegue il riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent quando si verifica un arresto imprevisto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Filename**  
Consente di specificare il nome del file per il log degli errori.  
  
**...**  
Consente di individuare i file di log degli errori.  
  
**Includi messaggi di traccia esecuzione**  
Consente di includere messaggi di traccia dell'esecuzione nel log degli errori. Nei messaggi di traccia sono incluse informazioni dettagliate sull'operazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se questa opzione è selezionata, per il file di log sarà necessario ulteriore spazio su disco. È consigliabile selezionare questa opzione solo durante la risoluzione di un problema che potrebbe coinvolgere [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
**Scrivi file OEM**  
Consente di scrivere il file di log degli errori come file non Unicode. In questo modo, è possibile ridurre la quantità di spazio su disco utilizzata dal file di log. Quando questa opzione è selezionata, è tuttavia possibile che i messaggi contenenti dati Unicode siano più difficili da leggere.  
  
**Destinatario Net Send**  
Consente di digitare il nome dell'operatore destinato a ricevere la notifica Net Send dei messaggi scritti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nel file di log.  
  
## <a name="see-also"></a>Vedere anche  
[Operatori](../../ssms/agent/operators.md)  
[Log degli errori di SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
