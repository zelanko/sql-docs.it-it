---
title: Integrazione di Reporting Services tramite i controlli ReportViewer | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- ReportViewer controls
- integrating reports [Reporting Services]
ms.assetid: 3ba47fb4-73a9-4059-89fd-329adebe94a8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cbaa41c75297d62e84cfc808463214d19c4ff8fa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63126272"
---
# <a name="integrating-reporting-services-using-the-reportviewer-controls"></a>Integrazione di Reporting Services tramite i controlli ReportViewer
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)] in sono disponibili due controlli ReportViewer per l'integrazione delle funzionalità di visualizzazione dei report nelle applicazioni. È disponibile una versione per le applicazioni basate su Windows Form e una per le applicazioni Web Form. Ogni controllo offre funzionalità simili, ma ognuno è progettato per un ambiente specifico. Entrambi i controlli consentono di elaborare i report distribuiti in un server di report (modalità di elaborazione remota) o copiati in un computer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in cui non è stato installato (modalità di elaborazione locale).  
  
 Il controllo ReportViewer non include il supporto integrato per l'adattamento dinamico ai diversi dispositivi con risoluzioni dello schermo diverse.  
  
## <a name="remote-processing-mode"></a>Modalità di elaborazione remota  
 La modalità di elaborazione remota è il metodo migliore per la visualizzazione dei report distribuiti in un server di report. La modalità di elaborazione remota offre i vantaggi seguenti:  
  
-   L'elaborazione remota fornisce una soluzione ottimizzata per l'esecuzione di report, in quanto il rendering e l'elaborazione dei report vengono eseguiti dal server di report.  
  
-   Poiché l'elaborazione viene gestita dal server di report, una richiesta del report può essere elaborata da più server di report in una distribuzione con scalabilità orizzontale o da un server con più processori in uno scenario con scalabilità verticale.  
  
 Per i report eseguiti in modalità remota possono inoltre venire usate le funzionalità complete del server di report, incluse tutte le estensioni dati e per il rendering.  
  
> [!NOTE]  
>  L'elenco di estensioni disponibili per il controllo ReportViewer quando l'esecuzione avviene in modalità di elaborazione remota dipende dall'edizione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installata nel server di report.  
  
## <a name="local-processing-mode"></a>Modalità di elaborazione locale  
 La modalità di elaborazione locale offre un metodo alternativo per la visualizzazione e il rendering dei report quando [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non è installato. A differenza dell'elaborazione remota, nel controllo è disponibile solo un subset delle funzionalità fornite dal server di report. Nella modalità locale l'elaborazione dei dati non viene gestita dal controllo ma implementata dall'applicazione host. L'elaborazione dei report viene tuttavia gestita dal controllo. Nella modalità di elaborazione locale sono disponibili solo le estensioni per il rendering PDF, Excel, Word e Image.  
  
## <a name="see-also"></a>Vedere anche  
 [Integrazione di Reporting Services in applicazioni](../application-integration/integrating-reporting-services-into-applications.md)   
 [Creazione di report SSRS con Visual Studio (Blog)](https://jwcooney.com/2015/01/07/ssrs-basics-set-up-visual-studio-to-write-a-new-ssrs-report/)  
  
  
