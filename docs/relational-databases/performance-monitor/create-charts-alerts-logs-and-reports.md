---
title: Creare grafici, avvisi, log e report | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- System Monitor [SQL Server], charts and reports
- charts [SQL Server]
- reports [SQL Server]
- reports [SQL Server], creating
- Windows System Monitor [SQL Server], charts and reports
- logs [SQL Server], System Monitor
- System Monitor [SQL Server], logs
- Windows System Monitor [SQL Server], logs
ms.assetid: c9162b37-e5dc-43d1-a3aa-1e9ebc69fecc
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5e67b62ec00e2dd98ff4289c1f725892592340e0
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68024766"
---
# <a name="create-charts-alerts-logs-and-reports"></a>Creare grafici, avvisi, log e report
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Monitoraggio di sistema consente di creare grafici, avvisi, log e report per monitorare un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="charts"></a>Grafici  
 I grafici consentono di monitorare le prestazioni correnti di oggetti e contatori selezionati, ad esempio l'utilizzo della CPU o l'I/O su disco. È possibile inserire in un grafico diverse combinazioni di oggetti e contatori di Monitoraggio di sistema, nonché di oggetti e contatori di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows.  
  
 Ogni grafico rappresenta un subset di informazioni da monitorare. Ad esempio, è possibile utilizzare un grafico per registrare le statistiche di utilizzo della memoria e un secondo grafico per le statistiche dell'I/O su disco.  
  
 È possibile utilizzare i grafici per:  
  
-   Individuare la ragione delle scarse prestazioni di un computer o un'applicazione.  
  
-   Eseguire un monitoraggio continuo dei sistemi per individuare problemi di prestazioni intermittenti.  
  
-   Individuare la ragione per la quale è necessario un potenziamento del sistema.  
  
-   Visualizzare una tendenza sotto forma di grafico a linee.  
  
-   Visualizzare un confronto sotto forma di istogramma.  
  
 I grafici risultano particolarmente utili per i monitoraggi a breve termine e in tempo reale di computer locali o remoti, ad esempio per monitorare un evento in corso.  
  
## <a name="alerts"></a>Avvisi  
 Gli avvisi di Monitoraggio di sistema consentono di tenere traccia di determinati eventi e di riceverne notifica. È possibile utilizzare un log degli avvisi per monitorare le prestazioni correnti di contatori e istanze per gli oggetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se un contatore supera il valore specificato, la data e l'ora dell'evento vengono registrate nel log. Un evento può inoltre generare un avviso di rete ed è possibile fare in modo che venga avviato un determinato programma la prima volta o tutte le volte che si verifica un evento. Ad esempio, è possibile impostare un avviso che invia un messaggio di rete a tutti gli amministratori di sistema per comunicare che per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo spazio su disco è insufficiente.  
  
## <a name="logs"></a>Log  
 È possibile utilizzare i log per registrare le informazioni relative all'attività corrente di oggetti e computer in modo da poterle visualizzare ed esaminare in un momento successivo. È possibile raccogliere i dati relativi a più sistemi in un unico file di log. Ad esempio, è possibile creare diversi log per raccogliere informazioni sulle prestazioni di determinati oggetti in diversi computer in modo da poterle analizzare in seguito. La selezione di oggetti potrà essere salvata in un file in modo da poterla riutilizzare per creare un altro log contenente informazioni analoghe a scopo di confronto.  
  
 I file di log forniscono informazioni utili per la risoluzione dei problemi e la pianificazione. A differenza dei grafici, degli avvisi e dei report, che forniscono informazioni immediate sull'attività corrente, i file di log consentono di registrare i valori dei contatori su lunghi periodi di tempo fornendo un'analisi e una documentazione più dettagliata delle prestazioni del sistema.  
  
## <a name="reports"></a>Report  
 È possibile utilizzare i report per visualizzare i diversi valori dei contatori e delle istanze di determinati oggetti nella loro continua evoluzione. I valori di ogni istanza vengono visualizzati in colonne. È possibile modificare gli intervalli dei report, stampare snapshot ed esportare dati. Utilizzare i report per visualizzare i valori non elaborati.  
  
 Per ulteriori informazioni sulla creazione di grafici, avvisi, log e report o sugli oggetti e i contatori di Windows, vedere la documentazione di Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
