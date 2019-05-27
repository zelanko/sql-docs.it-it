---
title: Panoramica di preparazione aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- SQL Server Upgrade Advisor, components
- tools [Upgrade Advisor]
- Upgrade Advisor [SQL Server], components
- components [Upgrade Advisor]
- Upgrade Advisor Analysis Wizard
- limitations [Upgrade Advisor]
- analyzing system [Upgrade Advisor]
- analyzing system [Upgrade Advisor], about analysis
ms.assetid: f5c56f63-4478-40af-abb9-642f58a0026c
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c78630764a26bb8fe281446c1bb997f18d965db7
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66091602"
---
# <a name="upgrade-advisor-overview"></a>Panoramica di Preparazione aggiornamento
  Preparazione aggiornamento rende disponibile una console centrale per l'analisi dei componenti di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] e [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], nonché per la visualizzazione di report contenenti informazioni sui risultati dell'analisi.  
  
## <a name="how-upgrade-advisor-works"></a>Funzionamento di Preparazione aggiornamento  
 Quando si esegue Preparazione aggiornamento, viene visualizzata la relativa pagina iniziale, ovvero il punto di avvio per gli elementi seguenti:  
  
-   Analisi guidata di Preparazione aggiornamento  
  
-   Visualizzatore report di Preparazione aggiornamento  
  
-   Guida di Preparazione aggiornamento  
  
 La prima volta che si utilizza Preparazione aggiornamento, eseguire l'Analisi guidata di Preparazione aggiornamento per analizzare un server. Al termine dell'analisi, fare clic su **avvia Report** dalla procedura guidata o tornare alla pagina iniziale di preparazione aggiornamento. Da questa pagina eseguire il Visualizzatore report di Preparazione aggiornamento per visualizzare il report. Il report fornisce collegamenti a informazioni che consentiranno di risolvere i problemi noti.  
  
## <a name="upgrade-advisor-analysis-wizard"></a>Analisi guidata di Preparazione aggiornamento  
 Per eseguire un'analisi, fare clic su **avviare Analisi guidata Preparazione aggiornamento** nella pagina iniziale di preparazione aggiornamento. Verranno raccolte informazioni sul computer, sulle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sui componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sui file di traccia che si desidera analizzare. Dopo la raccolta e la verifica di tutte le informazioni, verranno analizzati i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Ogni volta che si esegue l'Analisi guidata di Preparazione aggiornamento, viene generato un report separato e i report esistenti per i componenti selezionati non vengono sovrascritti. Tuttavia, nel visualizzatore di report vengono visualizzati solo gli ultimi cinque report.  
  
 Al termine dell'analisi, verrà creato un file XML per ogni componente incluso nell'analisi. I file XML contengono gli elementi e i problemi individuati in ogni componente.  
  
### <a name="what-upgrade-advisor-analyzes"></a>Elementi analizzati da Preparazione aggiornamento  
 Per ogni componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene eseguito un analizzatore dedicato nel contesto di Preparazione aggiornamento. L'output di ogni analizzatore è costituito da un report XML per il componente.  
  
 Preparazione aggiornamento esegue query sui componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguenti:  
  
-   Server di database, denominato anche [!INCLUDE[ssDE](../../includes/ssde-md.md)] nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], che include Replica, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, Ricerca full-text e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
> [!NOTE]  
>  Durante l'analisi, ogni analizzatore crea un file di log. È possibile utilizzare questi file di log per risolvere i problemi di analisi. Ad esempio, se l'esecuzione di Preparazione aggiornamento è lenta, è possibile visualizzare i file di log per determinare la causa del ritardo.  
  
### <a name="upgrade-advisor-limitations"></a>Limitazioni di Preparazione aggiornamento  
 Preparazione aggiornamento non è in grado di rilevare tutti i problemi che possono influire su un aggiornamento. Ad esempio, se un'applicazione client eseguita sui desktop degli utenti finali contiene codice SQL incorporato, non sarà possibile analizzare le applicazioni con Preparazione aggiornamento. Per questi elementi, è ancora necessario valutare i problemi ed eseguire l'aggiornamento, la migrazione o la modifica delle informazioni in base ai requisiti dell'installazione.  
  
 Preparazione aggiornamento non analizza le stored procedure crittografate, il codice delle stored procedure estese e il codice sorgente in linguaggi diversi da [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="upgrade-advisor-report-viewer"></a>Visualizzatore report di Preparazione aggiornamento  
 Per visualizzare un report di preparazione aggiornamento, fare clic su **avviare Visualizzatore Report Preparazione aggiornamento** nella pagina iniziale di preparazione aggiornamento. All'avvio del Visualizzatore report di Preparazione aggiornamento verranno caricati i report presenti nella directory predefinita. I report non vengono visualizzati se non vengono trovati nella directory predefinita. Se la directory predefinita non contiene report, è possibile eseguire l'Analisi guidata di Preparazione aggiornamento per creare un report oppure caricare un report esistente da un altro server o da una sottodirectory.  
  
 I report esistenti non vengono sovrascritti da Preparazione aggiornamento di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Tuttavia, nel visualizzatore di report vengono visualizzati solo gli ultimi cinque report. Per visualizzare un report precedente, selezionare il report dal **Report** casella di riepilogo a discesa. Il valore timestamp indica la data e l'ora in cui il report è stato generato.  
  
 Quando i file XML dell'Analisi guidata di Preparazione aggiornamento vengono caricati nel Visualizzatore report di Preparazione aggiornamento, verrà visualizzato un report per ogni componente. Il report contiene tutti i problemi noti, sia rilevabili che non rilevabili, che è necessario risolvere. A ogni problema è associata un'icona che ne indica l'importanza, un'etichetta con informazioni su quando è necessario risolvere il problema e una breve descrizione. Se un problema viene espanso, verrà visualizzata una descrizione più lunga, un collegamento ai dettagli e un collegamento al file della Guida. La quantità di informazioni fornite per ogni problema dovrebbe essere sufficiente per consentirne la correzione.  
  
 La maggior parte dei componenti presenta problemi che non è possibile rilevare. Per visualizzare tali problemi, espandere la **altri problemi di aggiornamento** elemento per il componente e quindi fare clic sul collegamento per visualizzare informazioni aggiuntive sui problemi nella documentazione. Per ulteriori informazioni sui problemi relativi alla compatibilità con le versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere la documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
