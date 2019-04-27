---
title: Definizione e identificazione di oggetti (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 48223f9718ae4eb87b0880c2f266c886ec7abbb0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62634594"
---
# <a name="defining-and-identifying-objects-xmla"></a>Definizione e identificazione di oggetti (XMLA)
  Nei comandi XMLA (XML for Analysis) gli oggetti vengono identificati tramite identificatori e riferimenti all'oggetto e vengono definiti tramite comandi XMLA relativi a elementi ASSL (Analysis Services Scripting Language).  
  
## <a name="object-identifiers"></a>Identificatori di oggetto  
 Un oggetto viene identificato tramite l'identificatore univoco dell'oggetto come definito in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Gli identificatori di oggetto possono essere specificati in modo esplicito o determinati dall'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando l'oggetto viene creato in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. È possibile usare la [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) metodo per recuperare gli identificatori di oggetto per successivi **Discover** oppure [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) chiamate al metodo.  
  
## <a name="object-references"></a>Riferimenti agli oggetti  
 Numerosi comandi XMLA, ad esempio [eliminare](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) oppure [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla), usare un riferimento all'oggetto per fare riferimento a un oggetto in modo non ambiguo. Un riferimento all'oggetto contiene l'identificatore dell'oggetto su cui viene eseguito un comando e gli identificatori di oggetto dei predecessori dell'oggetto specifico. Il riferimento all'oggetto per una partizione ad esempio contiene l'identificatore di oggetto della partizione nonché gli identificatori di oggetto del gruppo di misure padre della partizione specifica, del cubo e del database.  
  
## <a name="object-definitions"></a>Definizioni di oggetti  
 Il [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) e [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) comandi in XMLA creano o modificano, rispettivamente, gli oggetti in un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza. Le definizioni per tali oggetti sono rappresentate da un [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) elemento che contiene elementi ASSL. Gli identificatori di oggetto possono essere specificati in modo esplicito per tutti i principali e molti oggetti secondari tramite il [ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) elemento. Se il **ID** elemento non viene usato, il [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza costituisce un identificatore univoco, con una convenzione di denominazione che dipende dall'oggetto che deve essere identificato. Per altre informazioni su come usare il **Create** e **Alter** comandi per definire gli oggetti, vedere [creazione e modifica di oggetti &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/creating-and-altering-objects-xmla.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento dell'oggetto &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento ParentObject &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento Source &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Elemento target &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
