---
title: 'Lezione 8: Definizione delle azioni | Microsoft Docs'
ms.date: 05/06/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 2f233bab0c90abf41ab8fbef923e7c7b920ff2c3
ms.sourcegitcommit: 54c8420b62269f6a9e648378b15127b5b5f979c1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/07/2019
ms.locfileid: "65403673"
---
# <a name="lesson-8-defining-actions"></a>Lezione 8: Definizione di azioni
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]

In questa lezione verranno descritte le procedure per definire le azioni del progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Un'azione è semplicemente un'istruzione MDX (Multidimensional Expressions) archiviata in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , che può essere incorporata in applicazioni client e avviata da un utente.  
  
> [!NOTE]  
> I progetti completati per tutte le lezioni in questa esercitazione sono disponibili online. È possibile passare a qualsiasi lezione utilizzando il progetto completato della lezione precedente come punto iniziale. [Fare clic qui](http://go.microsoft.com/fwlink/?LinkID=221866) per scaricare i progetti di esempio usati in questa esercitazione.  
  
[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta i tipi di azioni descritti nella tabella seguente.  
  
|||  
|-|-|  
|CommandLine|Esegue un comando al prompt dei comandi|  
|Set di dati|Restituisce un set di dati a un'applicazione client.|  
|Drill-through|Restituisce un'istruzione drill-through come un'espressione che viene eseguita dal client per restituire un set di righe|  
|Html|Esegue uno script HTML in un browser Internet|  
|Proprietario|Esegue un'operazione utilizzando un'interfaccia diversa da quelle elencate in questa tabella.|  
|Report|Invia una richiesta con parametri basata sull'URL a un server di report e restituisce un report a un'applicazione client.|  
|Set di righe|Restituisce un set di righe a un'applicazione client.|  
|.|Esegue un comando OLE DB.|  
|URL|Visualizza una pagina Web dinamica in un browser Internet|  
  
Le azioni consentono agli utenti di avviare un'applicazione o di eseguire altre procedure nell'ambito di un elemento selezionato. Per altre informazioni, vedere [Azioni &#40;Analysis Services - Dati multidimensionali&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md), [Azioni nei modelli multidimensionali](../multidimensional-models/actions-in-multidimensional-models.md)  
  
> [!NOTE]  
> Per ulteriori esempi di azioni, vedere quelli disponibili nella scheda Modelli nel riquadro Strumenti di calcolo oppure nel data warehouse di esempio [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] DW. Per altre informazioni sull'installazione di questo database, vedere [Installare dati di esempio e progetti per l'esercitazione di modellazione multidimensionale di Analysis Services](install-sample-data-and-projects.md).  
  
Questa lezione include gli argomenti seguenti:  
  
[Definizione e utilizzo di un'azione drill-through](lesson-8-1-defining-and-using-a-drillthrough-action.md)  
In questa procedura viene definita, utilizzata e utilizzerà e quindi modificata un'azione drill-through tramite la relazione di tipo Fatti citata precedentemente in questa esercitazione.  
  
## <a name="next-lesson"></a>Lezione successiva  
[Lezione 9: Definizione di prospettive e traduzioni](lesson-9-defining-perspectives-and-translations.md)  
  
## <a name="see-also"></a>Vedere anche  
[Scenario di Analysis Services Tutorial](analysis-services-tutorial-scenario.md)  
[Modellazione multidimensionale &#40;esercitazione di AdventureWorks&#41;](multidimensional-modeling-adventure-works-tutorial.md)  
[Azioni &#40;Analysis Services - Dati multidimensionali&#41;](../multidimensional-models/actions-analysis-services-multidimensional-data.md)  
[Azioni nei modelli multidimensionali](../multidimensional-models/actions-in-multidimensional-models.md)  
  
  
  
