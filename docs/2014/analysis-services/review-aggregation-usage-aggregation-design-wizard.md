---
title: Controlla utilizzo aggregazioni (Progettazione guidata aggregazioni) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.aggregationdesignwizard.reviewusage.f1
ms.assetid: 107ee872-3df2-4931-b56c-af11e38f6745
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 10968a24c858f2523ff8b816bf153b9dc5dc2a8a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62748283"
---
# <a name="review-aggregation-usage-aggregation-design-wizard"></a>Controlla utilizzo aggregazioni (Progettazione guidata aggregazioni)
  Utilizzare la pagina **Controlla utilizzo aggregazioni** per configurare le impostazioni di utilizzo delle aggregazioni.  
  
## <a name="options"></a>Opzioni  
 **Default**  
 Selezionare per impostare l'impostazione di utilizzo delle aggregazioni per l'attributo su Predefinito. Con questa impostazione, la progettazione applica una regola predefinita in base al tipo di attributo e di dimensione.  
  
 `Full`  
 Selezionare per impostare l'impostazione di utilizzo delle aggregazioni per l'attributo in `Full`. Con questa impostazione, ogni aggregazione per il cubo deve includere questo attributo o un attributo correlato che è a un livello inferiore nella catena dell'attributo. Evitare l'impostazione di utilizzo aggregazioni `Full` quando un attributo contiene molti membri. Se specificata per più attributi o attributi che hanno molti membri, questa impostazione potrebbe impedire la progettazione delle aggregazioni a causa delle dimensioni eccessive.  
  
 **None**  
 Selezionare per impostare l'impostazione di utilizzo delle aggregazioni per l'attributo in Nessuna. Con questa impostazione nessuna aggregazione del cubo deve includere questo attributo.  
  
 `Unrestricted`  
 Selezionare per impostare l'impostazione di utilizzo delle aggregazioni per l'attributo in `Unrestricted`. Con questa impostazione non sono inserite restrizioni nella progettazione delle aggregazioni. Tuttavia, l'attributo ancora deve essere valutato per stabilire se è idoneo.  
  
 **Impostare come predefinito per tutti**  
 Selezionare per impostare le impostazioni  di utilizzo delle aggregazioni per tutti gli attributi su Predefinito.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida F1 guidata di progettazione delle aggregazioni](aggregation-design-wizard-f1-help.md)   
 [Procedure guidate di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
