---
title: Cosa&#39;s New in Analysis Services e Business Intelligence | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 173ca9fbf1fa3e9e2dc9dcb177c45a2ea3849415
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66065321"
---
# <a name="what39s-new-in-analysis-services-and-business-intelligence"></a>Cosa&#39;s New in Analysis Services e Business Intelligence
  Fatta eccezione per la funzionalità aggiunta che supporta i report di Power View sui modelli multidimensionali, [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)][!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] è invariato rispetto alla versione precedente.  
  
 Per informazioni su altri [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] prodotti e tecnologie che sono diverse in questa versione, vedere [What ' s New in SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).  
  
## <a name="updates-to-design-tool-installation"></a>Aggiornamenti all'installazione dello strumento di progettazione  
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] per Business Intelligence (SSDT-BI), precedentemente noto come Business Intelligence Development Studio (BIDS), viene utilizzato per creare i modelli di Analysis Services, i report di Reporting Services e i pacchetti di Integration Services. È possibile scaricare SSDT-BI dai percorsi seguenti:  
  
-   [Scaricare SSDT-BI per Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)  
  
-   [Scaricare SSDT-BI per Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)  
  
 Se si dispone di una versione precedente di SSDT-BI o BIDS installata nel computer, la versione più recente viene installata side-by-side alla versione precedente. La versione più recente e quella precedente degli strumenti di progettazione vengono in genere eseguite su una sola workstation in modo da poter modificare progetti e soluzioni legati a versioni specifiche del server.  
  
> [!NOTE]  
>  Sono disponibili vari siti di download per le versioni di SSDT di Visual Studio 2012 e Visual Studio 2013. La maggior parte non include i modelli di progetto BI. Tramite i collegamenti sopra indicati è possibile scaricare la versione corretta. Si sarà certi di disporre della versione corretta di SSDT-BI se viene visualizzata la cartella dei modelli di progetto Business Intelligence. Questa cartella contiene i modelli di progetto per Analysis Services, Reporting Services e Integration Services. A seconda della modalità di installazione di SSDT-BI, potrebbe essere visualizzato anche un modello di progetto aggiuntivo per i database di SQL Server.  
  
 ![Nuovi modelli di progetto in SSDT](media/ssdt-biprojects.png "Nuovi modelli di progetto in SSDT")  
  
## <a name="features-recently-added-power-view-for-multidimensional-models"></a>Funzionalità recentemente aggiunte: Power View per i modelli multidimensionali  
 La possibilità di creare report Power View nei modelli multidimensionali è stata introdotta per la prima volta nell'aggiornamento cumulativo 4 di [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1. La funzionalità Power View per i modelli multidimensionali è ora incluso in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].  
  
 **Report di Power View per un modello multidimensionale**  
  
 ![Report di Power View](media/powerviewreport-wn.gif "Report Power View")  
  
 Questa funzionalità consente alle organizzazioni di ottimizzare gli investimenti esistenti di business intelligence permettendo di utilizzare i modelli multidimensionali (anche noti come cubi OLAP) con i più recenti strumenti client per la creazione di report. A seconda dei tipi di dati contenuti in un modello multidimensionale, gli utenti possono creare facilmente varie visualizzazioni dinamiche dalle tabelle e dalle matrici, ai grafici a bolle, alle mappe geografiche. I modelli multidimensionali ora supportano anche le query che utilizzano Data Analysis Expressions (DAX).  
  
 Power View per modelli multidimensionali richiede la funzionalità predefinita di creazione di report Power View in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (modalità SharePoint). Altre versioni di Power View, in particolare il componente aggiuntivo di Power View in Excel 2013, non supportano i modelli multidimensionali.  
  
 Per altre informazioni, vedere [Power View per modelli multidimensionali](https://msdn.microsoft.com/library/dn140246.aspx).  
  
  
