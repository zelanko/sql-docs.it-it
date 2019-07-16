---
title: Sviluppo con Analysis Services Scripting Language (ASSL) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c113e07099ed96abdb0eb5f62c8517ee422d3cc7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208478"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>Sviluppo con Analysis Services Scripting Language (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  ASSL (Analysis Services Scripting Language) è un'estensione di XMLA che aggiunge un linguaggio di definizione dell'oggetto e un linguaggio di comando per la creazione e la gestione di strutture di Analysis Services direttamente sul server. È possibile utilizzare ASSL in un'applicazione personalizzata per comunicare con Analysis Services mediante il protocollo XMLA. Il linguaggio ASSL è costituito da due componenti:  
  
-   Linguaggio DDL (Data Definition Language), o linguaggio di definizione dell'oggetto, che specifica e descrive un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] nonché i database e gli oggetti di database che l'istanza contiene.  
  
-   Un linguaggio di comando che invia i comandi di azione, ad esempio **Create**, **Alter**, o **processo**, a un'istanza di Analysis Services. Questo linguaggio di comando viene discusso nel [XML for Analysis &#40;XMLA&#41; riferimento](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference).  
  
 Per visualizzare l'ASSL che descrive una soluzione multidimensionale in [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], è possibile utilizzare il comando Visualizza codice al livello del progetto. È inoltre possibile creare o modificare script ASSL in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] utilizzando l'editor di query XMLA. Gli script compilati possono essere utilizzati per gestire oggetti o eseguire comandi nel server.  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti ASSL e relative caratteristiche](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-objects-and-object-characteristics.md)   
 [Convenzioni XML di ASSL](../../../analysis-services/multidimensional-models/scripting-language-assl/assl-xml-conventions.md)   
 [Origini dati e associazioni &#40;SSAS multidimensionale&#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
