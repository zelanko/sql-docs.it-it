---
title: Integrazione di Reporting Services tramite i controlli Visualizzatore report | Microsoft Docs
ms.date: 09/18/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: application-integration
ms.topic: reference
helpviewer_keywords:
- Report Viewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8ffaeb12bc961256959571d18808e2869a1d7485
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62741884"
---
# <a name="integrating-reporting-services-using-report-viewer-controls"></a>Integrazione di Reporting Services tramite i controlli Visualizzatore report
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 2015 sono disponibili due controlli Visualizzatore report per l'integrazione delle funzionalità di visualizzazione dei report nelle applicazioni. È disponibile una versione per le applicazioni basate su Windows Form e una per le applicazioni Web Form. Ogni controllo offre funzionalità simili, ma ognuno è progettato per un ambiente specifico. Entrambi i controlli consentono di elaborare i report distribuiti in un server di report (modalità di elaborazione remota) o copiati in un computer in cui [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è stato installato (modalità di elaborazione locale).  
  
 Il controllo Visualizzatore report non include il supporto integrato per l'adattamento dinamico ai diversi dispositivi con risoluzioni dello schermo diverse.  
  
## <a name="remote-processing-mode"></a>Modalità di elaborazione remota  
 La modalità di elaborazione remota è il metodo migliore per la visualizzazione dei report distribuiti in un server di report. La modalità di elaborazione remota offre i vantaggi seguenti:  
  
-   L'elaborazione remota fornisce una soluzione ottimizzata per l'esecuzione di report, in quanto il rendering e l'elaborazione dei report vengono eseguiti dal server di report.  
  
-   Poiché l'elaborazione viene gestita dal server di report, una richiesta del report può essere elaborata da più server di report in una distribuzione con scalabilità orizzontale o da un server con più processori in uno scenario con scalabilità verticale.  
  
 Per i report eseguiti in modalità remota possono inoltre venire usate le funzionalità complete del server di report, incluse tutte le estensioni dati e per il rendering.  
  
> [!NOTE]  
>  L'elenco di estensioni disponibili per il controllo Visualizzatore report quando l'esecuzione avviene in modalità di elaborazione remota dipende dall'edizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installata nel server di report.  
  
## <a name="local-processing-mode"></a>Modalità di elaborazione locale  
 La modalità di elaborazione locale offre un metodo alternativo per la visualizzazione e il rendering dei report quando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è installato. A differenza dell'elaborazione remota, nel controllo è disponibile solo un subset delle funzionalità fornite dal server di report. Nella modalità locale l'elaborazione dei dati non viene gestita dal controllo ma implementata dall'applicazione host. L'elaborazione dei report viene tuttavia gestita dal controllo. Nella modalità di elaborazione locale sono disponibili solo le estensioni per il rendering PDF, Excel, Word e Image.  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione di Reporting Services nelle applicazioni](../../reporting-services/application-integration/integrating-reporting-services-into-applications.md)   
 [Uso del controllo Web Form Visualizzatore report](../../reporting-services/application-integration/using-the-webforms-reportviewer-control.md)   
 [Uso del controllo Windows Form Visualizzatore report](../../reporting-services/application-integration/using-the-winforms-reportviewer-control.md)  

  
  
