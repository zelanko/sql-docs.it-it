---
description: Proprietà SQL Server Agent (pagina Cronologia)
title: Proprietà SQL Server Agent (pagina Cronologia)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.history.f1
ms.assetid: dc73734c-b3c3-407f-bbd1-8714b4fa47b0
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016
ms.openlocfilehash: b2981d9d99442b4743a1fad81512b504c9b323f9
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464312"
---
# <a name="sql-server-agent-properties-history-page"></a>Proprietà SQL Server Agent (pagina Cronologia)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte ma non tutte le funzionalità di SQL Server Agent. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare le impostazioni di gestione del log della cronologia del servizio di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Limita dimensioni log cronologia processo**  
Consente di impostare limiti sulla quantità di informazioni sulla cronologia processo che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantiene nel log.  
  
**Dimensioni massime log cronologia processo (righe)**  
Consente di impostare il numero massimo di righe che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantiene nel log. Quando il log raggiunge dimensioni tali da contenere questo numero di righe, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent rimuove le righe meno recenti per consentire l'inserimento delle nuove.  
  
**Numero massimo di righe di cronologia per processo**  
Consente di impostare il numero massimo di righe che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent mantiene per ogni processo. Quando la cronologia di un determinato processo si estende fino a contenere questo numero di righe, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent consente di rimuovere le righe meno recenti per consentire l'inserimento delle nuove.  
  
**Rimuovi cronologia dell'agente**  
Viene indicato che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent consentirà di rimuovere le voci presenti nel log da più tempo rispetto a quanto specificato. Si tratta di un'esecuzione singola che consente di rimuovere la cronologia. Se è necessario un processo ricorrente, creare e pianificare un piano di manutenzione con un processo di pulizia.  
  
**Più vecchia di**  
Consente di impostare il periodo di tempo per cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent manterrà le voci.  
  
## <a name="see-also"></a>Vedere anche  
[Log degli errori di SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
