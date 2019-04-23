---
title: Sviluppo con Analysis Services Scripting Language (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- Analysis Services Scripting Language
- ASSL
ms.assetid: ce9aca4d-b7ad-451e-bb7f-20c2b0c03f29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dfdce0d0db35d651d12670ffd3cb1c9437961cd1
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "60154277"
---
# <a name="developing-with-analysis-services-scripting-language-assl"></a>Sviluppo con Analysis Services Scripting Language (ASSL)
  ASSL (Analysis Services Scripting Language) è un'estensione di XMLA che aggiunge un linguaggio di definizione dell'oggetto e un linguaggio di comando per la creazione e la gestione di strutture di Analysis Services direttamente sul server. È possibile utilizzare ASSL in un'applicazione personalizzata per comunicare con Analysis Services mediante il protocollo XMLA. Il linguaggio ASSL è costituito da due componenti:  
  
-   Linguaggio DDL (Data Definition Language), o linguaggio di definizione dell'oggetto, che specifica e descrive un'istanza di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] nonché i database e gli oggetti di database che l'istanza contiene.  
  
-   Linguaggio di comando che invia comandi di azione, ad esempio `Create`, `Alter` o `Process`, a un'istanza di Analysis Services. Questo linguaggio di comando viene discusso nel [XML for Analysis &#40;XMLA&#41; riferimento](https://docs.microsoft.com/bi-reference/xmla/xml-for-analysis-xmla-reference).  
  
 Per visualizzare l'ASSL che descrive una soluzione multidimensionale in [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)], è possibile utilizzare il comando Visualizza codice al livello del progetto. È inoltre possibile creare o modificare script ASSL in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] utilizzando l'editor di query XMLA. Gli script compilati possono essere utilizzati per gestire oggetti o eseguire comandi nel server.  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetti ASSL e relative caratteristiche](assl-objects-and-object-characteristics.md)   
 [Convenzioni XML di ASSL](assl-xml-conventions.md)   
 [Origini dati e associazioni &#40;SSAS multidimensionale&#41;](../data-sources-and-bindings-ssas-multidimensional.md)  
  
  
