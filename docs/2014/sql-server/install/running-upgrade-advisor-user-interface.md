---
title: Esecuzione di preparazione aggiornamento (interfaccia utente) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor Report Viewer
- Upgrade Advisor [SQL Server], running
- launching Upgrade Advisor
- Upgrade Advisor Analysis Wizard
- starting Upgrade Advisor
- SQL Server Upgrade Advisor, running
ms.assetid: 7f47c9b3-88d3-43d6-837e-f157b49a55ac
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 653e3d0565d0b32c67ccf77772a9b89f611dd082
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85058944"
---
# <a name="running-upgrade-advisor-user-interface"></a>Esecuzione di Preparazione aggiornamento (interfaccia utente)
  È possibile eseguire Preparazione aggiornamento per analizzare componenti locali o remoti durante la pianificazione dell'aggiornamento. Per ogni istanza e componente analizzato, viene prodotto un report.  
  
> [!IMPORTANT]  
>  Le istanze remote di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non vengono analizzate. Per analizzare un'istanza di [!INCLUDE[ssRS](../../includes/ssrs.md)], è necessario installare Preparazione aggiornamento nel computer in cui è installato [!INCLUDE[ssRS](../../includes/ssrs.md)].  
>   
>  Per analizzare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services, è necessario che sia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] installato e [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installato nello stesso computer.  
  
## <a name="running-the-upgrade-advisor-analysis-wizard"></a>Esecuzione dell'Analisi guidata di Preparazione aggiornamento  
 L'esecuzione dell'Analisi guidata di Preparazione aggiornamento prevede sei passaggi:  
  
1.  Avvio della procedura guidata dalla pagina iniziale di Preparazione aggiornamento.  
  
2.  Identificazione dei server e dei componenti da analizzare.  
  
3.  Raccolta di informazioni sull'autenticazione.  
  
4.  Raccolta di parametri aggiuntivi in base al tipo di componente.  
  
5.  Analisi dei componenti selezionati.  
  
6.  Generazione del report dei problemi di aggiornamento.  
  
 Per ulteriori informazioni sull'analisi guidata di preparazione aggiornamento, vedere [procedura: esecuzione dell'analisi guidata di preparazione aggiornamento](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md).  
  
 Per informazioni specifiche richieste per ogni passaggio, vedere Guida di [riferimento all'interfaccia utente di preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md).  
  
## <a name="running-the-upgrade-advisor-report-viewer"></a>Esecuzione del Visualizzatore report di Preparazione aggiornamento  
 Utilizzare il Visualizzatore report di Preparazione aggiornamento per visualizzare i report generati dall'Analisi guidata di Preparazione aggiornamento. Quando il report viene caricato, è possibile filtrare i componenti del report in base ai fattori seguenti:  
  
-   Tutti i problemi  
  
-   Tutti i problemi di aggiornamento  
  
-   Problemi di pre-aggiornamento  
  
-   Tutti i problemi di migrazione  
  
-   Problemi risolti  
  
-   Problemi irrisolti  
  
 Per le istruzioni dettagliate per l'utilizzo del visualizzatore di report, vedere gli argomenti seguenti:  
  
-   [Procedura: Visualizzare un report di Preparazione aggiornamento](../../../2014/sql-server/install/how-to-view-an-upgrade-advisor-report.md)  
  
-   [Procedura: Filtrare i report](../../../2014/sql-server/install/how-to-filter-reports.md)  
  
-   [Procedura: Esportare i report](../../../2014/sql-server/install/how-to-export-reports.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura: esecuzione dell'analisi guidata di preparazione aggiornamento](../../../2014/sql-server/install/how-to-run-the-upgrade-advisor-analysis-wizard.md)   
 [Guida di riferimento all'interfaccia utente di preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)   
 [Risoluzione dei problemi di aggiornamento](../../../2014/sql-server/install/resolving-upgrade-issues.md)   
 [Uso di Preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)  
  
  
