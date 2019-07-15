---
title: Ottimizzare l'amministrazione automatizzata in un'organizzazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- performance [SQL Server], automated administration
- tuning automated administration [SQL Server]
- monitoring performance [SQL Server], automated administration
ms.assetid: 671fed35-3859-4b0d-8f38-4dd07436857e
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 671b2e98cf9e9969af68612d75af97bb17984c99
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67681418"
---
# <a name="tune-automated-administration-across-an-enterprise"></a>Ottimizzazione dell'amministrazione automatizzata in un'organizzazione
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

L'amministrazione multiserver implementata da Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sfrutta le caratteristiche di ottimizzazione automatica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In condizioni normali, non è pertanto necessario eseguire ottimizzazioni dei processi aggiuntive. L'esecuzione di processi, la generazione di avvisi e le notifiche agli operatori possono tuttavia determinare un aumento dei carichi di rete e in questi casi è possibile ottimizzare l'amministrazione automatizzata all'interno di un'organizzazione in modo da ridurre al minimo il traffico di rete provocato da queste attività.  
  
## <a name="see-also"></a>Vedere anche  
[Monitoraggio delle prestazioni del motore del flusso di dati](../../integration-services/performance/performance-counters.md)  
  
