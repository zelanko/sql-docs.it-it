---
title: Definizione e identificazione di oggetti (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- objects [XML for Analysis]
- identifying objects [XML for Analysis]
- XML for Analysis, objects
- object references [XML for Analysis]
- object identifiers [XML for Analysis]
- object definitions [XML for Analysis]
- XMLA, objects
ms.assetid: 43b65f6d-0123-4556-81f0-c7a0b84361e5
author: minewiskan
ms.author: owend
ms.openlocfilehash: d2fd3263a2f8050c36747a81ab3473f5b405ef21
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545028"
---
# <a name="defining-and-identifying-objects-xmla"></a>Definizione e identificazione di oggetti (XMLA)
  Nei comandi XMLA (XML for Analysis) gli oggetti vengono identificati tramite identificatori e riferimenti all'oggetto e vengono definiti tramite comandi XMLA relativi a elementi ASSL (Analysis Services Scripting Language).  
  
## <a name="object-identifiers"></a>Identificatori di oggetto  
 Un oggetto viene identificato utilizzando l'identificatore univoco dell'oggetto come definito in un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Gli identificatori di oggetto possono essere specificati in modo esplicito o determinati dall'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quando l'oggetto viene creato in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. È possibile usare il metodo [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) per recuperare gli identificatori di oggetto per le `Discover` chiamate al metodo successive o [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) .  
  
## <a name="object-references"></a>Riferimenti a oggetti  
 Diversi comandi XMLA, ad esempio [Delete](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/delete-element-xmla) o [Process](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla), utilizzano un riferimento a un oggetto per fare riferimento a un oggetto in modo non ambiguo. Un riferimento all'oggetto contiene l'identificatore dell'oggetto su cui viene eseguito un comando e gli identificatori di oggetto dei predecessori dell'oggetto specifico. Il riferimento all'oggetto per una partizione ad esempio contiene l'identificatore di oggetto della partizione nonché gli identificatori di oggetto del gruppo di misure padre della partizione specifica, del cubo e del database.  
  
## <a name="object-definitions"></a>Definizioni di oggetti  
 I comandi [create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) e [ALTER](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) in XMLA creano o modificano rispettivamente oggetti in un' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza di. Le definizioni per tali oggetti sono rappresentate da un elemento [ObjectDefinition](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/objectdefinition-element-xmla) che contiene elementi di ASSL. Gli identificatori di oggetto possono essere specificati in modo esplicito per tutti i principali e molti oggetti secondari utilizzando l'elemento [ID](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/id-element-xmla) . Se l'elemento `ID` non viene utilizzato, l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] specifica un identificatore univoco, con una convenzione di denominazione che dipende dall'oggetto da identificare. Per ulteriori informazioni su come utilizzare i `Create` comandi e `Alter` per definire gli oggetti, vedere [creazione e modifica di oggetti &#40;&#41;XMLA ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects).  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento oggetto &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento ParentObject &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla)   
 [Elemento Source &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla)   
 [Elemento target &#40;&#41;XMLA](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/target-element-xmla)   
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
