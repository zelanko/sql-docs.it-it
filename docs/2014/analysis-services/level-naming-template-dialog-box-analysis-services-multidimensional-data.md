---
title: Finestra di dialogo modello (Analysis Services - dati multidimensionali) di denominazione dei livelli | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.levelnamingtemplatedialog.f1
helpviewer_keywords:
- Level Naming Template dialog box
ms.assetid: 96cad715-213e-4eac-9003-130a2f5fc985
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: febaae6051e8428d3fed2bb6533ce2c4d972950f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078054"
---
# <a name="level-naming-template-dialog-box-analysis-services---multidimensional-data"></a>Finestra di dialogo Modello denominazione livelli (Analysis Services - Dati multidimensionali)
  Usare la finestra di dialogo **Modello denominazione livelli** in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per creare il modello di denominazione dei livelli per un attributo padre in una dimensione. Per altre informazioni sui modelli di denominazione dei livelli, vedere [Elemento NamingTemplate &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/namingtemplate-element-assl). È possibile visualizzare il **modello denominazione livelli** finestra di dialogo facendo clic sul pulsante con puntini di sospensione ( **...** ) sul `NamingTemplate` valore di una traduzione per un attributo nel **dettagli di traduzione** riquadro il **traduzioni** scheda della finestra di **progettazione dimensioni**.  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Definire il modello di livello**|Consente di visualizzare una griglia in cui è possibile progettare la gerarchia di livelli nell'attributo padre. La griglia include le colonne seguenti:<br /><br /> **Livello**: Consente di visualizzare la posizione ordinale del livello per il quale viene usato il nome specificato in **Nome** . Per aggiungere un nuovo modello di denominazione per un livello, selezionare **Nome** nella riga contenente un asterisco (\*) in **Livello**.<br /><br /> **Nome**: Contiene il modello di denominazione usato per il livello indicato in **Livello**. Per aggiungere un segnaposto per la posizione ordinale del livello nel modello di denominazione, aggiungere un asterisco (*). Per aggiungere un asterisco come parte del nome creato dal modello di denominazione, aggiungere due asterischi (\*\*).|  
|**Cancella tutto**|Selezionare questa opzione per rimuovere tutte le righe in **Definire il modello di livello**.|  
|**Result**|Consente di visualizzare il modello di denominazione dei livelli creato nella finestra di dialogo.|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Le traduzioni &#40;progettazione dimensioni&#41; &#40;Analysis Services - dati multidimensionali&#41;](translations-dimension-designer-analysis-services-multidimensional-data.md)  
  
  
