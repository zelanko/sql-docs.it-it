---
title: Monitorare con SCOM - sistema di piattaforma Analitica | Microsoft Docs
description: Usare System Center Operations Manager (SCOM) per monitorare l'appliance del sistema di piattaforma Analitica (AP).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3c43734dbd7ef1a766f3f1258f97565ab82e175d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639828"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>Monitoraggio con System Center Operations Manager - sistema di piattaforma Analitica
Usare System Center Operations Manager (SCOM) per monitorare l'appliance del sistema di piattaforma Analitica (AP).
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
  
1.  System Center Operations Manager 2007 R2, 2012 o 2012 SP1 deve essere installato e in esecuzione.  
  
2.  È necessario installare SQL Server 2008 R2 Native Client o SQL Server 2012 Native Client.  
  
3.  I management pack per monitorare SQL Server PDW devono essere installati, importati e configurati. Usare gli articoli seguenti per le istruzioni per eseguire queste attività.  
  
    -   [Installare i Management Pack SCOM &#40;sistema di piattaforma Analitica&#41;](install-the-scom-management-packs.md)  
  
    -   [Importare il Management Pack SCOM per PDW &#40;sistema di piattaforma Analitica&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configurare SCOM per monitorare il sistema di piattaforma Analitica &#40;sistema di piattaforma Analitica&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Per monitorare SQL Server PDW con SCOM  
Dopo aver configurato i Management Pack SCOM, fare clic sul monitoraggio riquadro di SCOM ed eseguire il drill-down **SQL Server Appliance** e quindi **Microsoft SQL Server Parallel Data Warehouse**. Di sotto di Microsoft SQL Server Parallel Data Warehouse, sono disponibili quattro opzioni: Gli avvisi, i dispositivi, diagramma di Appliance e nodi.  
  
### <a name="alerts"></a>Avvisi  
Gli avvisi sono in cui è possibile trovare gli avvisi correnti per la gestione.  
  
![Gli avvisi](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Strumenti  
I dispositivi sono in cui si troverà l'attualmente individuati e monitorati SQL Server PDW Appliance nell'ambiente in uso. Se un dispositivo non vengono visualizzati qui e aver creato la connessione ODBC per tale, può essere presente un problema con il proprio account PDWWatcher. Se vengono visualizzati come "Non monitorato", potrebbe esserci un problema con il proprio account PDWMonitor. Essere paziente poiché SCOM non apporta modifiche in tempo reale, ma periodicamente le nuove Appliance per il monitoraggio e invia periodicamente le query per Appliance per il monitoraggio.  
  
![Appliances](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagramma strumenti  
Pagina del diagramma Appliance è dove è possibile ottenere un aspetto dello stato del dispositivo con una visualizzazione albero:  
  
![Diagramma di Appliance](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nodi  
Infine, la visualizzazione di nodi consente di visualizzare l'integrità del dispositivo a ogni nodo:  
  
![Nodes](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Avvisi della Console di amministrazione informazioni sui &#40;sistema di piattaforma Analitica&#41;](understanding-admin-console-alerts.md)  
  
