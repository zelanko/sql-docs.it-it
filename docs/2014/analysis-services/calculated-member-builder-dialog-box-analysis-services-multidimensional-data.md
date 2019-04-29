---
title: Finestra di dialogo Generatore membri (Analysis Services - dati multidimensionali) calcolato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.calculatedmemberbuilderdialog.f1
ms.assetid: 73b89a9f-f403-4ab8-99f7-e3ceb870c260
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa1dd7ba570a02eae75d93aa540090983717f130
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62664297"
---
# <a name="calculated-member-builder-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Generatore membri calcolati (Analysis Services - Dati multidimensionali)
  Utilizzare la finestra di dialogo **Generatore membri calcolati** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per compilare un membro calcolato.  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Name**|Consente di digitare il nome del membro calcolato.|  
|**Gerarchia padre**|Consente di selezionare la gerarchia in cui creare il membro calcolato.|  
|**Membro padre**|Questa opzione è abilitata se si seleziona una gerarchia padre, diversa dalla dimensione `Measures`, che include più di un livello. Fare clic sui puntini di sospensione (**...** ) per selezionare un membro padre. Il membro padre determina la posizione del membro calcolato nella struttura della dimensione.|  
|**Espressione**|Consente di digitare l'espressione MDX da utilizzare.|  
|**Controlla**|Fare clic su **Controlla** per verificare l'espressione MDX definita in **Espressione**.|  
|**Metadati**|Visualizza i metadati relativi all'oggetto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] corrente che è possibile includere nell'espressione MDX definita in **Espressione**.<br /><br /> È possibile copiare la sintassi MDX per l'elemento selezionato facendo clic con il pulsante destro del mouse sull'elemento e scegliendo **Copia**oppure trascinando l'elemento selezionato in **Espressione**.|  
|**Funzioni**|Consente di visualizzare le funzioni MDX disponibili per l'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] corrente. Gli elementi elencati sono recuperati dal set di righe dello schema MDSCHEMA_FUNCTIONS.<br /><br /> È possibile copiare la sintassi MDX per l'elemento selezionato facendo clic con il pulsante destro del mouse sull'elemento e scegliendo **Copia**oppure trascinando l'elemento selezionato in **Espressione**.|  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a MDX &#40;Multidimensional Expressions&#41;](/sql/mdx/multidimensional-expressions-mdx-reference)  
  
  
