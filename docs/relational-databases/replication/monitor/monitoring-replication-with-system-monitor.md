---
title: Monitoraggio della replica con Monitor di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- monitoring performance [SQL Server replication], System Monitor
- System Monitor [SQL Server], replication
- performance counters [SQL Server replication]
ms.assetid: 8cd3a270-0328-4bfd-bf23-b1d759cc120c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 91db0303326c74b710e7755de5a9573539e61425
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "68082978"
---
# <a name="monitoring-replication-with-system-monitor"></a>Monitoraggio della replica con Monitor di sistema
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Monitor di sistema di[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows consente di utilizzare grafici e report per valutare l'efficienza del computer, identificare e risolvere eventuali problemi, ad esempio un utilizzo non equilibrato delle risorse, componenti hardware inadeguati e configurazioni di programmi insufficienti, nonché pianificare risorse hardware aggiuntive. Per altre informazioni, vedere [Monitoraggio dell'utilizzo delle risorse&#40;Monitor di sistema&#41;](../../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 In Monitor di sistema vengono utilizzati oggetti e contatori delle prestazioni che forniscono informazioni sulle prestazioni dei vari processi. È possibile misurare le prestazioni della replica mediante contatori associati agli agenti di replica:  
  
|Agente|Oggetto prestazione|Contatore|Descrizione|  
|-----------|------------------------|-------------|-----------------|  
|Tutti gli agenti|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agenti di replica|In esecuzione|Numero di agenti di replica correntemente in esecuzione.|  
|agente snapshot|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Snapshot repliche|Snapshot: Comandi recapitati/sec|Numero di comandi al secondo recapitati al database di distribuzione.|  
|agente snapshot|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Snapshot repliche|Snapshot: Transazioni recapitate/sec|Numero di transazioni al secondo recapitate al database di distribuzione.|  
|Agente di lettura log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Lettura log repliche|Logreader: Comandi recapitati/sec|Numero di comandi al secondo recapitati al database di distribuzione.|  
|Agente di lettura log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Lettura log repliche|Logreader: Transazioni recapitate/sec|Numero di transazioni al secondo recapitate al database di distribuzione.|  
|Agente di lettura log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Lettura log repliche|Logreader: Latenza recapito|L'intervallo di tempo in millisecondi che intercorre tra l'applicazione delle transazioni nel server di pubblicazione e il recapito delle transazioni al server di distribuzione.|  
|Agente di distribuzione|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribuzione repliche|Dist: Comandi recapitati/sec|Numero di comandi al secondo recapitati al Sottoscrittore.|  
|Agente di distribuzione|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribuzione repliche|Dist: Transazioni recapitate/sec|Numero di transazioni al secondo recapitate al Sottoscrittore.|  
|Agente di distribuzione|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribuzione repliche|Dist: Latenza recapito|L'intervallo di tempo in millisecondi che intercorre tra il recapito delle transazioni al server di distribuzione e l'applicazione delle transazioni nel Sottoscrittore.|  
|Agente di merge|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Merge repliche|Conflitti/sec|Numero di conflitti al secondo generati durante il processo di replica di tipo merge.|  
|Agente di merge|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Merge repliche|Modifiche scaricate/sec|Il numero di righe al secondo replicate dal server di pubblicazione nel Sottoscrittore.|  
|Agente di merge|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Merge repliche|Modifiche caricate/sec|Il numero di righe al secondo replicate dal Sottoscrittore nel server di pubblicazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio &#40;replica&#41;](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
