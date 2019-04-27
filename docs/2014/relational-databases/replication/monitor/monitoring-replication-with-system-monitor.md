---
title: Monitoraggio della replica con Monitor di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 2b5d1a63937a11da4703ec4ef0338dee89a5c33f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62667306"
---
# <a name="monitoring-replication-with-system-monitor"></a>Monitoraggio della replica con Monitor di sistema
  Monitor di sistema di[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows consente di utilizzare grafici e report per valutare l'efficienza del computer, identificare e risolvere eventuali problemi, ad esempio un utilizzo non equilibrato delle risorse, componenti hardware inadeguati e configurazioni di programmi insufficienti, nonché pianificare risorse hardware aggiuntive. Per altre informazioni, vedere [Monitoraggio dell'utilizzo delle risorse&#40;Monitor di sistema&#41;](../../performance-monitor/monitor-resource-usage-system-monitor.md).  
  
 In Monitor di sistema vengono utilizzati oggetti e contatori delle prestazioni che forniscono informazioni sulle prestazioni dei vari processi. È possibile misurare le prestazioni della replica mediante contatori associati agli agenti di replica:  
  
|Agent|Oggetto prestazione|Contatore|Descrizione|  
|-----------|------------------------|-------------|-----------------|  
|Tutti gli agenti|[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agenti di replica|In esecuzione|Numero di agenti di replica correntemente in esecuzione.|  
|agente snapshot|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Snapshot repliche|Snapshot: Comandi recapitati/sec|Numero di comandi al secondo recapitati al database di distribuzione.|  
|agente snapshot|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Snapshot repliche|Snapshot: Transazioni recapitate/sec|Numero di transazioni al secondo recapitate al database di distribuzione.|  
|Agente di lettura log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agente lettura log repliche|Agente di lettura log: Comandi recapitati/sec|Numero di comandi al secondo recapitati al database di distribuzione.|  
|Agente di lettura log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agente lettura log repliche|Agente di lettura log: Transazioni recapitate/sec|Numero di transazioni al secondo recapitate al database di distribuzione.|  
|Agente di lettura log|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Agente lettura log repliche|Agente di lettura log: Latenza recapito|L'intervallo di tempo in millisecondi che intercorre tra l'applicazione delle transazioni nel server di pubblicazione e il recapito delle transazioni al server di distribuzione.|  
|Agente di distribuzione|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribuzione repliche|Dist: Comandi recapitati/sec|Numero di comandi al secondo recapitati al Sottoscrittore.|  
|Agente di distribuzione|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribuzione repliche|Dist: Transazioni recapitate/sec|Numero di transazioni al secondo recapitate al Sottoscrittore.|  
|Agente di distribuzione|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Distribuzione repliche|Dist: Latenza recapito|L'intervallo di tempo in millisecondi che intercorre tra il recapito delle transazioni al server di distribuzione e l'applicazione delle transazioni nel Sottoscrittore.|  
|Agente di merge|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Merge repliche|Conflitti/sec|Numero di conflitti al secondo generati durante il processo di replica di tipo merge.|  
|Agente di merge|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Merge repliche|Modifiche scaricate/sec|Il numero di righe al secondo replicate dal server di pubblicazione nel Sottoscrittore.|  
|Agente di merge|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Merge repliche|Modifiche caricate/sec|Il numero di righe al secondo replicate dal Sottoscrittore nel server di pubblicazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio &#40;replica&#41;](../monitoring-replication.md)  
  
  
