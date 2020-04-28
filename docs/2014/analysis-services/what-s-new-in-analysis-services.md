---
title: Novità di Analysis Services e Business Intelligence |&#39;Microsoft Docs
ms.custom: ''
ms.date: 06/07/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: aa69c299-b8f4-4969-86d8-b3292fe13f08
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1458dcf473ffbf7fc9bab13c2c688a4e01954c56
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78175540"
---
# <a name="what39s-new-in-sql-server-2014-analysis-services"></a>Novità di SQL Server 2014 Analysis Services&#39;
  Fatta eccezione per la funzionalità aggiuntiva che supporta Power View report sui modelli multidimensionali [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , è invariata rispetto alla versione precedente.

 Per informazioni su altri [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] prodotti e tecnologie diversi in questa versione, vedere novità [di SQL Server 2014](../sql-server/what-s-new-in-sql-server-2016.md).

## <a name="updates-to-design-tool-installation"></a>Aggiornamenti all'installazione dello strumento di progettazione
 [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] per Business Intelligence (SSDT-BI), precedentemente noto come Business Intelligence Development Studio (BIDS), viene utilizzato per creare i modelli di Analysis Services, i report di Reporting Services e i pacchetti di Integration Services. È possibile scaricare SSDT-BI dai percorsi seguenti:

-   [Scaricare SSDT-BI per Visual Studio 2013](https://go.microsoft.com/fwlink/p/?LinkId=396526)

-   [Download di SSDT-BI per Visual Studio 2012](https://go.microsoft.com/fwlink/p/?LinkID=273673)

 Se si dispone di una versione precedente di SSDT-BI o BIDS installata nel computer, la versione più recente viene installata side-by-side alla versione precedente. La versione più recente e quella precedente degli strumenti di progettazione vengono in genere eseguite su una sola workstation in modo da poter modificare progetti e soluzioni legati a versioni specifiche del server.

> [!NOTE]
>  Sono disponibili vari siti di download per le versioni di SSDT di Visual Studio 2012 e Visual Studio 2013. La maggior parte non include i modelli di progetto BI. Tramite i collegamenti sopra indicati è possibile scaricare la versione corretta. Si noterà che è presente la versione corretta di SSDT-BI se viene visualizzata la cartella dei modelli di progetto di business intelligence. Questa cartella contiene i modelli di progetto per Analysis Services, Reporting Services e Integration Services. A seconda della modalità di installazione di SSDT-BI, potrebbe essere visualizzato anche un modello di progetto aggiuntivo per i database di SQL Server.

 ![Nuovi modelli di progetto in SSDT](media/ssdt-biprojects.png "Nuovi modelli di progetto in SSDT")

## <a name="features-recently-added-power-view-for-multidimensional-models"></a>Funzionalità recentemente aggiunte: Power View per i modelli multidimensionali
 La possibilità di creare report Power View nei modelli multidimensionali è stata introdotta per la prima volta nell'aggiornamento cumulativo 4 di [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] Service Pack 1. La funzionalità Power View per i modelli multidimensionali è ora incluso in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)].

 **Report Power View per un modello multidimensionale**

 ![Report Power View](media/powerviewreport-wn.gif "Report Power View")

 Questa funzionalità consente alle organizzazioni di ottimizzare gli investimenti esistenti di business intelligence permettendo di utilizzare i modelli multidimensionali (anche noti come cubi OLAP) con i più recenti strumenti client per la creazione di report. A seconda dei tipi di dati contenuti in un modello multidimensionale, gli utenti possono creare facilmente varie visualizzazioni dinamiche dalle tabelle e dalle matrici, ai grafici a bolle, alle mappe geografiche. I modelli multidimensionali ora supportano anche le query che utilizzano Data Analysis Expressions (DAX).

 Power View per modelli multidimensionali richiede la funzionalità predefinita di creazione di report Power View in [!INCLUDE[ssSQL14](../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] (modalità SharePoint). Altre versioni di Power View, in particolare il componente aggiuntivo di Power View in Excel 2013, non supportano i modelli multidimensionali.

 Per ulteriori informazioni, vedere [Power View per i modelli multidimensionali](https://msdn.microsoft.com/library/dn140246.aspx).


