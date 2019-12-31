---
title: Monitoraggio dell'appliance
description: Questa guida di monitoraggio dell'appliance descrive gli strumenti e le attività per il monitoraggio dell'appliance del sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: cec604ff1a93213fc6308455cadda90e6efa2d61
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401420"
---
# <a name="appliance-monitoring-for-analytics-platform-system"></a>Monitoraggio degli appliance per il sistema di piattaforma Analytics
Questa guida di monitoraggio dell'appliance descrive gli strumenti e le attività per il monitoraggio dell'appliance del sistema della piattaforma di analisi.  
  
## <a name="Basics"></a>Strumenti e nozioni di base sul monitoraggio  
I valori e le informazioni che è possibile monitorare nell'appliance SQL Server PDW sono estesi. Ad esempio, di seguito sono riportate le attività di monitoraggio tipiche.  
  
-   Verificare la presenza di eventuali avvisi emessi dal SQL Server PDW.  
  
-   Monitoraggio dell'hardware non riuscito.  
  
-   Monitoraggio dei problemi di connettività di rete.  
  
-   Verificare la presenza di errori restituiti agli utenti durante l'elaborazione della query.  
  
-   Visualizzare il numero di sessioni e query attualmente attive.  
  
-   Verificare lo stato di caricamenti, backup e ripristini.  
  
### <a name="appliance-monitoring-tools"></a>Strumenti di monitoraggio degli appliance  
Sono disponibili diversi strumenti per il monitoraggio dell'appliance.  
  
Console di amministrazione  
SQL Server PDW dispone di una console di amministrazione. Si tratta di uno strumento basato sul Web che consente di visualizzare informazioni su query, caricamenti, backup e ripristino, blocchi, sessioni, avvisi e stato dell'appliance. La console di amministrazione viene eseguita nell'appliance. Gli utenti si connettono alla console di amministrazione tramite Internet Explorer. Per altre informazioni, vedere:  
  
-   [Monitorare l'appliance usando la console di amministrazione &#40;sistema della piattaforma di analisi&#41;](monitor-the-appliance-by-using-the-admin-console.md)  
  
![Avvisi della console di amministrazione di PDW](./media/appliance-monitoring/SQL_Server_PDW_AdminConsol_Queries.png "SQL_Server_PDW_AdminConsol_Queries")  
  
Viste di sistema  
SQL Server PDW include viste di sistema complete che consentono di ottenere informazioni dettagliate sull'integrità, lo stato e le prestazioni dell'appliance. Per un elenco delle viste di sistema per le attività di monitoraggio, vedere:  
  
-   [Monitorare l'appliance usando le viste di sistema &#40;sistema della piattaforma di analisi&#41;](monitor-the-appliance-by-using-system-views.md)  
  
System Center Operations Manager (SCOM)  
SQL Server PDW offre un'ampia integrazione con Systems Center Operations Manager. I Management Pack per SQL Server PDW sono disponibili come download gratuito. Per ulteriori informazioni sull'utilizzo di System Center per monitorare SQL Server PDW, vedere gli argomenti seguenti:  
  
-   [Monitorare l'appliance usando System Center Operations Manager sistema di piattaforma &#40;Analytics&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)  
  
Soluzioni personalizzate  
Per le situazioni in cui System Center non è disponibile con gli strumenti di monitoraggio di data center, è possibile monitorare l'appliance usando una soluzione di monitoraggio di terze parti. L'installazione di agenti software esterni non è attualmente supportata in PDW, ma la maggior parte delle\-soluzioni di monitoraggio supporta l'integrazione di Transact SQL, quindi\-l'amministratore di sistema può implementare query Transact-SQL dirette sul dispositivo PDW.  
  
Se la soluzione di monitoraggio non supporta le query\-Transact-SQL dirette oppure non si dispone di uno strumento di monitoraggio, è possibile utilizzare gli script per eseguire attività di monitoraggio, ad esempio l'invio di messaggi di posta elettronica quando si verifica un avviso.  Il wiki TechNet contiene un esempio di soluzione di monitoraggio con script.  
  
-   [Esempio di monitoraggio di Power Shell per SQL Server PDW](https://go.microsoft.com/fwlink/?LinkId=248020)  
   
## <a name="Tasks"></a>Attività di monitoraggio correlate  
  
|Attività di monitoraggio|Description|  
|-------------------|---------------|  
|Monitorare l'appliance usando la console di amministrazione.|[Monitorare l'appliance usando la console di amministrazione &#40;sistema della piattaforma di analisi&#41;](monitor-the-appliance-by-using-the-admin-console.md)|  
|Monitorare l'appliance usando le visualizzazioni di sistema.|[Monitorare l'appliance usando le viste di sistema &#40;sistema della piattaforma di analisi&#41;](monitor-the-appliance-by-using-system-views.md)|  
|Monitorare l'appliance usando System Center|[Monitorare l'appliance usando System Center Operations Manager sistema di piattaforma &#40;Analytics&#41;](monitor-the-appliance-by-using-system-center-operations-manager.md)|  
|Monitorare lo stato dell'appliance.|[Monitorare lo stato di integrità dell'appliance &#40;sistema della piattaforma di analisi&#41;](monitor-appliance-health-state.md)|  
|Monitoraggio heartbeat.|[Invia il feedback di telemetria a Microsoft &#40;SQL Server PDW&#41;](send-telemetry-feedback-to-microsoft-sql-server-pdw.md)|  
|Rilevare gli avvisi dell'appliance.|[Tenere traccia degli avvisi dell'appliance &#40;sistema della piattaforma di analisi&#41;](track-appliance-alerts.md)|  
|Determinare la quantità di capacità usata.|[Visualizzare l'utilizzo della capacità &#40;sistema della piattaforma di analisi&#41;](view-capacity-utilization.md)|  
|Determinare la frequenza con cui eseguire il polling dell'appliance.|[Determinare la frequenza di polling &#40;sistema della piattaforma di analisi&#41;](determine-polling-frequency.md)|  
|Quando si verifica un errore del cluster, determinare quale nodo del cluster ha avuto esito negativo.|[Determinare quale nodo del cluster non è riuscito &#40;sistema della piattaforma di analisi&#41;](determine-which-cluster-node-failed.md)|  


<!-- MISSING LINKS |Monitor loads.|[Monitor Loads &#40;SQL Server PDW&#41;](../sqlpdw/monitor-loads-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor backups and restores.|[Monitor Backups and Restores &#40;SQL Server PDW&#41;](../sqlpdw/monitor-backups-and-restores-sql-server-pdw.md)|  -->  
<!-- MISSING LINKS |Monitor the active queries.|[Monitoring Active Queries &#40;SQL Server PDW&#41;](../sqlpdw/monitoring-active-queries-sql-server-pdw.md)|  -->  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Attività di gestione degli appliance &#40;sistema di piattaforma di analisi&#41;](appliance-management-tasks.md)  
  
