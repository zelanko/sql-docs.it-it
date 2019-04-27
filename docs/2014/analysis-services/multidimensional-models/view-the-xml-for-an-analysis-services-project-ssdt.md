---
title: Visualizzare il codice XML per un Analysis Services Project (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], viewing XML
ms.assetid: dd1a4bc6-57b5-47df-8619-09f921aa6351
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ff8c70b2a4cd98fe665ca40bb95af8fa986bb6fc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62740811"
---
# <a name="view-the-xml-for-an-analysis-services-project-ssdt"></a>Visualizzare il codice XML per un progetto di Analysis Services (SSDT)
  Quando si utilizza un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in modalità progetto, in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] viene creata una definizione XML per ogni oggetto all'interno della cartella di progetto. È possibile visualizzare il contenuto del file XML per ogni oggetto in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. È inoltre possibile modificare direttamente il file XML. Nella maggior parte delle circostanze, tuttavia, ciò non è consigliabile poiché le modifiche apportate potrebbero rendere il codice XML illeggibile per [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
> [!NOTE]  
>  Non è possibile visualizzare il codice XML per un intero progetto. Viene invece visualizzato il codice per ogni oggetto, per il quale esiste un file separato. L'unico modo per visualizzare il codice per un intero progetto consiste nel compilare il progetto e visualizzare la definizione ASSL Scrivi codice nel \<nome progetto > file con estensione asdatabase.  
  
### <a name="to-view-the-xml-code-for-an-object"></a>Per visualizzare il codice XML per un oggetto  
  
1.  Aprire il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sull'oggetto in Esplora soluzioni e quindi scegliere **Visualizza codice**.  
  
     In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]verrà visualizzato il codice XML per l'oggetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilare progetti di Analysis Services &#40;SSDT&#41;](build-analysis-services-projects-ssdt.md)  
  
  
