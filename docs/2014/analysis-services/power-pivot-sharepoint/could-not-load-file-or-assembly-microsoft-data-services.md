---
title: Impossibile caricare il file o l'assembly &#39;Microsoft. AnalysisServices. SharePoint. Integration&#39; | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9baec97f8d1e779a84f25e7ddbf437e0a40ef4b3
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547493"
---
# <a name="could-not-load-file-or-assembly-39microsoftanalysisservicessharepointintegration39"></a>Impossibile caricare il file o l'assembly &#39;Microsoft. AnalysisServices. SharePoint. Integration&#39;
  Negli ambienti di SharePoint 2010 in cui è disponibile PowerPivot per SharePoint, questo errore si verificherà se la distribuzione della soluzione a livello di applicazione per PowerPivot non è stata eseguita correttamente.  
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Si applica a|PowerPivot per SharePoint|  
|Versione prodotto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|La soluzione Powerpivotwebapp non è stata distribuita o non ha eseguito correttamente la distribuzione.|  
|Testo del messaggio|Impossibile caricare il file o l'assembly "Microsoft.AnalysisServices.SharePoint.Integration"|  
  
## <a name="explanation"></a>Spiegazione  
 PowerPivot per SharePoint utilizza i pacchetti della soluzione per distribuire le funzionalità in un server SharePoint. Una delle soluzioni non è distribuita correttamente. Di conseguenza, questo errore viene visualizzato quando si tenta di aprire la raccolta PowerPivot o altre pagine dell'applicazione PowerPivot in un sito di SharePoint.  
  
## <a name="user-action"></a>Azione dell'utente  
 Distribuire il pacchetto della soluzione.  
  
1.  In Impostazioni sistema di Amministrazione centrale fare clic su **Gestisci soluzioni farm**.  
  
2.  Fare clic su **Powerpivotwebapp**.  
  
3.  Fare clic su **Distribuisci soluzione**.  
  
4.  Scegliere l'applicazione Web per la quale si sta verificando questo errore. Se sono presenti più applicazioni Web, ridistribuire la soluzione per tutte.  
  
5.  Fare clic su **OK**.  
  
## <a name="see-also"></a>Vedere anche  
 [Distribuire soluzioni PowerPivot in SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
