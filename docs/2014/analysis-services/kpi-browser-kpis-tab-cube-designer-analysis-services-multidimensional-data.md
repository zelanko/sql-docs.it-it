---
title: Visualizzatore KPI (scheda KPI, Progettazione cubi) (Analysis Services-Dati multidimensionali) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.kpibrowserpane.f1
ms.assetid: 2f61bde6-e6ec-4511-8645-c272374014ad
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 41000c78c4ff3a68e1d3acd107ce57c221a16e28
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66079495"
---
# <a name="kpi-browser-kpis-tab-cube-designer-analysis-services---multidimensional-data"></a>Visualizzatore KPI (scheda KPI, Progettazione cubi) (Analysis Services - Dati multidimensionali)
  Usare il riquadro **Visualizzatore KPI** della scheda **KPI** in Progettazione cubi per visualizzare e testare i risultati degli indicatori di prestazioni chiave (KPI). Prima di eseguire l'esplorazione, gli [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] indicatori KPI devono essere prima distribuiti in un'istanza di.  
  
> [!NOTE]  
>  Questo riquadro viene visualizzato solo nella visualizzazione Esplorazione.  
  
## <a name="options"></a>Opzioni  
 **Griglia del sottocubo**  
 Usare questa opzione per definire un sottocubo e limitare i risultati degli indicatori KPI da visualizzare nel riquadro **Risultati** . La griglia include le colonne seguenti:  
  
 **Dimension**  
 Consente di selezionare la dimensione alla quale viene applicato il filtro.  
  
 **Gerarchia**  
 Consente di selezionare la gerarchia alla quale viene applicato il filtro.  
  
 **Operatore**  
 Consente di selezionare l'operatore che definisce il modo in cui l'espressione contenuta in **Espressione filtro** viene applicata alla gerarchia selezionata. Nella tabella seguente vengono descritti gli operatori disponibili.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Uguale**|I risultati sono limitati al set definito in **Espressione filtro**.|  
|**Diverso da**|I risultati sono limitati ai membri esclusi dal set definito in **Espressione filtro**.|  
|**In**|I risultati sono limitati al set denominato scelto in **Espressione filtro**.|  
|**Non incluso**|I risultati sono limitati ai membri esclusi dal set denominato scelto in **Espressione filtro**.|  
|**Contiene**|I risultati sono limitati ai membri i cui nomi contengono la stringa inclusa in **Espressione filtro**.|  
|**Inizia con**|I risultati sono limitati ai membri i cui nomi iniziano con la stringa inclusa in **Espressione filtro**.|  
|**Intervallo (inclusivo)**|I risultati sono limitati all'intervallo scelto in **Espressione filtro**.|  
|**Intervallo (esclusivo)**|I risultati sono limitati ai membri esclusi dall'intervallo scelto in **Espressione filtro**.|  
|**MDX**|I risultati sono limitati al set di espressioni MDX incluso in **Espressione filtro**.|  
  
 **Espressione filtro**  
 Consente di digitare l'espressione che dovrà essere valutata da **Operatore**, che limita i risultati KPI da esplorare.  
  
> [!NOTE]  
>  Questo campo rappresenta un elemento dinamico per l'immissione di dati, che cambia aspetto per riflettere i tipi di dati necessari per l'operatore selezionato.  
  
 **Griglia risultati**  
 Consente di visualizzare il valore valutato, l'obiettivo, lo stato e la tendenza per gli indicatori KPI, in base al filtro definito nella **Griglia filtri**. La griglia include le colonne seguenti:  
  
 **Visualizza struttura**  
 Consente di visualizzare gli indicatori KPI contenuti nel cubo, organizzati gerarchicamente in base ai valori di **Cartella di visualizzazione** o di **KPI padre** per ogni indicatore KPI.  
  
 **Valore**  
 Consente di visualizzare il valore dell'indicatore KPI.  
  
 **Obiettivo**  
 Consente di visualizzare il valore dell'obiettivo dell'indicatore KPI.  
  
 **Status**  
 Consente di visualizzare l'icona di stato dell'indicatore KPI.  
  
 **Tendenza**  
 Consente di visualizzare l'icona di tendenza dell'indicatore KPI.  
  
 **Peso**  
 Consente di visualizzare il fattore di ponderazione dell'indicatore KPI.  
  
 **Descrizione**  
 Consente di visualizzare un'icona Informazioni se è disponibile una descrizione per un indicatore KPI.  
  
 Fare passare il mouse sull'icona Informazioni per visualizzare una descrizione comando per l'indicatore KPI.  
  
> [!NOTE]  
>  Se viene generato un errore durante il calcolo di un indicatore KPI nell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , questa opzione visualizza le informazioni associate all'errore.  
  
## <a name="see-also"></a>Vedere anche  
 [Indicatori KPI &#40;Progettazione cubi&#41; &#40;Analysis Services Dati multidimensionali&#41;](kpis-cube-designer-analysis-services-multidimensional-data.md)  
  
  
