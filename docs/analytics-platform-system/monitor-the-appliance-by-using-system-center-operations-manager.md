---
title: Usare System Center Operations Manager per monitorare i punti di APS
description: Usare System Center Operations Manager (SCOM) per monitorare l'appliance del sistema di piattaforma analitica (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 539c18efe43afcf5436c6913c20cab081974b7f5
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86941123"
---
# <a name="monitor-with-system-center-operations-manager---analytics-platform-system"></a>Monitorare con System Center Operations Manager-Analytics Platform System
Usare System Center Operations Manager (SCOM) per monitorare l'appliance del sistema di piattaforma analitica (APS).
  
## <a name="before-you-begin"></a>Prima di iniziare  
  
### <a name="prerequisites"></a>Prerequisiti  
  
1.  System Center Operations Manager 2007 R2, 2012 o 2012 SP1 devono essere installati e in esecuzione.  
  
2.  È necessario installare SQL Server 2008 R2 Native client o SQL Server 2012 Native Client.  
  
3.  È necessario installare, importare e configurare i Management Pack per il monitoraggio SQL Server PDW. Usare gli articoli seguenti per istruzioni sull'esecuzione di queste attività.  
  
    -   [Installare i Management Pack di SCOM &#40;sistema di piattaforma di analisi&#41;](install-the-scom-management-packs.md)  
  
    -   [Importare il Management Pack SCOM per il sistema di piattaforma &#40;Analytics per PDW&#41;](import-the-scom-management-pack-for-pdw.md) 
    
    -   [Configurare SCOM per monitorare il sistema della piattaforma di &#40;Analytics della piattaforma Analytics&#41;](configure-scom-to-monitor-analytics-platform-system.md)
  
<!-- MISSING LINKS    -   [Import the SCOM Management Pack for HDInsight &#40;Analytics Platform System&#41;](import-the-scom-management-pack-for-hdinsight.md)  -->  
   
  
## <a name="to-monitor-sql-server-pdw-with-scom"></a>Per monitorare SQL Server PDW con SCOM  
Dopo aver configurato i Management Pack di SCOM, fare clic sul riquadro Monitoraggio di SCOM ed eseguire il drill-down fino a **SQL Server Appliance** , quindi **Microsoft SQL Server Parallel Data Warehouse**. Sotto Microsoft SQL Server Parallel Data Warehouse sono disponibili quattro opzioni: avvisi, appliance, diagramma di appliance e nodi.  
  
### <a name="alerts"></a>Avvisi  
Gli avvisi sono la posizione in cui è possibile trovare gli avvisi correnti da gestire.  
  
![Avvisi](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM.png "SCOM_SCOM")  
  
### <a name="appliances"></a>Strumenti  
Le appliance sono la posizione in cui si troveranno le appliance SQL Server PDW attualmente individuate e monitorate nell'ambiente in uso. Se un dispositivo non viene visualizzato qui ed è stata creata la connessione ODBC, potrebbe essersi verificato un errore con l'account PDWWatcher. Se vengono visualizzati come "non monitorati", potrebbe essersi verificato un errore con l'account PDWMonitor. Essere paziente perché SCOM non modifica in tempo reale, ma verifica periodicamente la presenza di nuove appliance per il monitoraggio e l'invio periodico di query alle appliance per il monitoraggio.  
  
![Appliance](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM2.png "SCOM_SCOM2")  
  
### <a name="appliances-diagram"></a>Diagramma Appliance  
La pagina del diagramma delle appliance è la posizione in cui è possibile esaminare l'integrità del dispositivo con una visualizzazione albero:  
  
![Diagramma Strumenti](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM3.png "SCOM_SCOM3")  
  
### <a name="nodes"></a>Nodi  
Infine, la visualizzazione nodi consente di visualizzare l'integrità dell'appliance tramite ogni nodo:  
  
![Nodi](./media/monitor-the-appliance-by-using-system-center-operations-manager/SCOM_SCOM4.png "SCOM_SCOM4")  
  
## <a name="see-also"></a>Vedere anche  
<!-- MISSING LINKS [Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
[Informazioni sugli avvisi della console di amministrazione &#40;sistema di piattaforma di analisi&#41;](understanding-admin-console-alerts.md)  
  
