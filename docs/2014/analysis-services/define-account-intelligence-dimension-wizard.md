---
title: Definizione funzionalità di Business Intelligence per la contabilità (creazione guidata dimensione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.dimensionwizard.accountintelligencetypemapping.f1
ms.assetid: cbcff072-3a7e-4e98-858f-1b4265461561
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7bbc2b890c61e2864aa727f42276f01c87e94a7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66082155"
---
# <a name="define-account-intelligence-dimension-wizard"></a>Definizione funzionalità di Business Intelligence per la contabilità (Creazione guidata dimensione)
  La pagina **Funzionalità di Business Intelligence per la contabilità** consente di eseguire il mapping tra i tipi di conto definiti nell'istanza [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e i tipi di conto definiti nell'attributo della dimensione associato al tipo di attributo **Tipo conto** nella dimensione.  
  
> [!NOTE]  
>  Questa pagina viene visualizzata solo se è stata selezionata l'opzione **dimensione standard** nella pagina **Selezione tipo di dimensione** e se è stato eseguito il mapping di un attributo della dimensione al tipo di attributo **tipo conto** nella pagina **impostazione tipo di dimensione** .  
  
## <a name="options"></a>Opzioni  
 **Tipi di conto tabella di origine**  
 Visualizza i valori contenuti nell'attributo della dimensione assegnato al tipo di attributo **Tipo conto** nella pagina **Impostazione chiave e tipo della dimensione** .  
  
 **Tipi di conto predefiniti**  
 Consente di selezionare il tipo di conto definito nell'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] di cui eseguire il mapping ai tipi di conto nella tabella di origine.  
  
 Nella tabella seguente vengono elencati i tipi di conto definiti in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Asset**|Valore degli elementi posseduti in un determinato momento.|  
|**Balance**|Conteggio di alcuni elementi in un determinato momento.|  
|**Spese**|Valore di elementi spesi.|  
|**Flusso**|Conteggio incrementale degli elementi.|  
|**Reddito**|Valore di elementi ricevuti.|  
|**Responsabilità**|Valore degli elementi dovuti in un determinato momento.|  
|**Statistica**|Rapporto calcolato di alcuni elementi oppure conteggio di elementi non aggregabili.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida sensibile al contesto della creazione guidata dimensione](dimension-wizard-f1-help.md)   
 [Dimensioni &#40;Analysis Services Dati multidimensionali&#41;](multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)   
 [Dimensioni nei modelli multidimensionali](multidimensional-models/dimensions-in-multidimensional-models.md)  
  
  
