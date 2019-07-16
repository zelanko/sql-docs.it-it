---
title: Monitoraggio dell'Appliance - sistema di piattaforma Analitica | Microsoft Docs
description: Questa Guida al monitoraggio appliance descrive gli strumenti e le attività per monitorare l'appliance del sistema di piattaforma Analitica.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: cb25a5eccd1e77f08cedc74ad8042e0dc573605c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961505"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>Monitoraggio dell'Appliance per il sistema di piattaforma Analitica
Questa Guida al monitoraggio appliance descrive gli strumenti e le attività per monitorare l'appliance del sistema di piattaforma Analitica.  
  
## <a name="Basics"></a>Nozioni di base e gli strumenti di monitoraggio  
I valori e informazioni che è possibile monitorare l'appliance di SQL Server PDW sono numerose. Ad esempio, di seguito sono tipiche attività di monitoraggio.  
  
-   Verifica per qualsiasi avviso emesso da SQL Server PDW.  
  
-   Monitoraggio di hardware non riuscito.  
  
-   Monitoraggio di problemi di connettività di rete.  
  
-   Controllare gli errori restituiti agli utenti durante l'elaborazione delle query.  
  
-   Visualizzare il numero di sessioni attualmente attive e query.  
  
-   Controllare lo stato di caricamento, backup e ripristini.  
  
### <a name="appliance-monitoring-tools"></a>Strumenti di monitoraggio delle Appliance  
Sono disponibili vari strumenti disponibili per monitorare l'appliance.  
  
Console di amministrazione  
SQL Server PDW è una Console di amministrazione. Questo è uno strumento basato sul web che consente di visualizzare informazioni sulle query, caricamenti, backup e ripristino, i blocchi, sessioni, gli avvisi e stato dello strumento. La Console di amministrazione viene eseguita nell'appliance; gli utenti di connettersi alla Console di amministrazione tramite Internet Explorer. Per altre informazioni, vedere:  
  
-   [Monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![Avvisi della Console di amministrazione PDW](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
Viste di sistema  
SQL Server PDW include viste di sistema completi che consentono di ottenere informazioni dettagliate sull'integrità delle appliance, stato e prestazioni. Per un elenco di viste di sistema per il monitoraggio delle attività, vedere:  
  
-   [Monitorare l'Appliance usando le viste di sistema &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW è ampia integrazione con Systems Center Operations Manager. I management pack per SQL Server PDW sono disponibili come download gratuito. Per altre informazioni sull'uso di System Center per monitorare SQL Server PDW, vedere gli argomenti seguenti:  
  
-   [Monitorare l'Appliance usando System Center Operations Manager &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
Soluzioni personalizzate  
Per le situazioni quando System Center non è disponibile con strumenti di monitoraggio del data center è possibile monitorare l'appliance usando una soluzione di monitoraggio di terze parti. Installazione degli agenti software esterni non è attualmente supportata in PDW, ma la maggior parte delle soluzioni di monitoraggio supportano Transact\-integrazione di SQL, in modo che l'amministratore di sistema possa implementare Transact diretta\-query SQL PDW Appliance.  
  
Se la soluzione di monitoraggio non supporta direct Transact\-query SQL, oppure non è uno strumento di monitoraggio, quindi è possibile usare gli script per eseguire attività di monitoraggio, ad esempio l'invio di posta elettronica quando viene generato un avviso.  Wiki di TechNet contiene un esempio di soluzione di monitoraggio tramite script.  
  
-   [PowerShell di esempio di monitoraggio per SQL Server PDW](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>Relative attività di monitoraggio  
  
|Monitoraggio attività|Descrizione|  
|-------------------|---------------|  
|Monitorare l'appliance usando la Console di amministrazione.|[Monitorare l'Appliance usando la Console di amministrazione &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|Monitorare l'appliance usando le viste di sistema.|[Monitorare l'Appliance usando le viste di sistema &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-views.md)|  
|Monitorare l'appliance usando System Center|[Monitorare l'Appliance usando System Center Operations Manager &#40;sistema di piattaforma Analitica&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|Monitorare lo stato dell'appliance.|[Monitoraggio stato di integrità di Appliance &#40;sistema di piattaforma Analitica&#41;](monitor-appliance-health-state.md)|  
|Monitoraggio heartbeat.|[Inviare commenti e suggerimenti dati di telemetria a Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|Tenere traccia degli avvisi dell'appliance.|[Tenere traccia degli avvisi di Appliance &#40;sistema di piattaforma Analitica&#41;](track-appliance-alerts.md)|  
|Determinare la quantità di capacità è in uso.|[Visualizzare l'utilizzo della capacità &#40;sistema di piattaforma Analitica&#41;](view-capacity-utilization.md)|  
|Determinare la frequenza con cui eseguire il polling dell'appliance.|[Determinare la frequenza di Polling &#40;sistema di piattaforma Analitica&#41;](determine-polling-frequency.md)|  
|Quando si verifica un errore del cluster, determinare quale cluster nodo non è riuscito.|[Determinare quale nodo del Cluster non riuscita &#40;sistema di piattaforma Analitica&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Attività di gestione di Appliance &#40;sistema di piattaforma Analitica&#41;](appliance-management-tasks.md)  
  
