---
title: Finestra di dialogo analisi di incidenza (dati multidimensionali Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.impactanalysisdialog.f1
ms.assetid: 208268eb-4e14-44db-9c64-6f74b776adb6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0c08690cd2f5b77471392cab3aad1587b4cb0f9a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080745"
---
# <a name="impact-analysis-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Analisi di impatto (Analysis Services - Dati multidimensionali)
  Utilizzare la finestra di dialogo **Analisi di impatto** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] e in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per identificare ed eventualmente elaborare gli oggetti dipendenti sui quali influisce l'elaborazione degli oggetti elencati nella finestra di dialogo **Elabora** . Per visualizzare la finestra di dialogo **Analisi di impatto** , è possibile fare clic su **Analisi di impatto** nella finestra di dialogo **Elabora** .  
  
> [!NOTE]  
>  Vengono visualizzate più occorrenze di uno stesso oggetto qualora quest'ultimo sia interessato da più eventi.  
  
## <a name="options"></a>Opzioni  
 **Elenco oggetti**  
 Visualizza l'elenco degli oggetti dipendenti in una griglia. La griglia include le colonne seguenti:  
  
 **nome oggetto**  
 Visualizza il nome dell'oggetto dipendente che può essere necessario elaborare. L'icona a sinistra del nome indica il tipo di oggetto.  
  
 **Type**  
 Indica il tipo di oggetto dipendente che può essere necessario elaborare.  
  
 **Tipo impatto**  
 Indica l'effetto che l'elaborazione degli oggetti elencati nella finestra di dialogo **Elabora** avrà sull'oggetto dipendente. Nella tabella seguente vengono elencati i possibili effetti dell'elaborazione, ognuno dei quali viene individuato come la causa di un avviso o di un errore.  
  
|Impatto|Message|  
|------------|-------------|  
|L'oggetto verrà cancellato (non elaborato)|Avviso|  
|L'oggetto risulterà non valido|Errore|  
|L'aggregazione verrà rimossa|Avviso|  
|L'aggregazione flessibile verrà rimossa|Avviso|  
|Gli indici verranno rimossi|Avviso|  
|Gli oggetti che non sono figli verranno elaborati|Avviso|  
  
 **Elabora oggetto**  
 Consente di selezionare gli oggetti dipendenti che si desidera includere nell'operazione di elaborazione. Sarà necessario elaborare gli oggetti dipendenti non selezionati al termine dell'operazione di elaborazione. In caso contrario, non sarà possibile utilizzarli.  
  
## <a name="see-also"></a>Vedi anche  
 [Finestre di progettazione e finestre di dialogo Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Finestra di dialogo elabora &#40;Analysis Services-Dati multidimensionali&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
