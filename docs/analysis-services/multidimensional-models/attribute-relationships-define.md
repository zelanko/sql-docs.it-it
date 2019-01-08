---
title: Definire relazioni tra attributi | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e49207e99887e13cdd5321821e7325b4a2dac7dc
ms.sourcegitcommit: 38076f423663bdbb42f325e3d0624264e05beda1
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/06/2018
ms.locfileid: "52983962"
---
# <a name="attribute-relationships---define"></a>Relazioni tra attributi - Definire
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], gli attributi rappresentano l'elemento costitutivo fondamentale di una dimensione. Una dimensione contiene un set di attributi organizzato in base alle relazioni tra attributi.  
  
 Per ogni tabella inclusa in una dimensione, vi è una relazione tra attributi che mette in relazione l'attributo chiave della tabella agli altri attributi di quella tabella. Si crea questa relazione quando si crea la dimensione.  
  
 Una relazione tra attributi fornisce i vantaggi seguenti:  
  
-   Riduce la quantità di memoria necessaria per l'elaborazione della dimensione. Ciò consente di rendere più rapida l’elaborazione di dimensioni, partizioni e query.  
  
-   Aumenta le prestazioni di esecuzione delle query in quanto l'accesso all'archiviazione è più veloce ed i piani di esecuzione sono ottimizzati.  
  
-   Determina la selezione di aggregati più efficaci da parte degli algoritmi di progettazione delle aggregazioni, purché siano presenti gerarchie definite dall'utente nei percorsi delle relazioni.  
  
  
## <a name="attribute-relationship-considerations"></a>Considerazioni sulle relazioni tra attributi  
 Quando i dati sottostanti lo supportano, si devono definire anche relazioni univoche tra attributi. Per definire relazioni tra attributi univoche, usare la scheda **Relazioni tra attributi** di Progettazione dimensioni.  
  
 Qualsiasi attributo che ha una relazione in uscita deve avere una chiave univoca relativa all'attributo correlato. In altre parole, un membro in un attributo di origine deve identificare un solo membro in un attributo correlato. Si consideri, ad esempio, la relazione, Città -> Stato. In questa relazione, l'attributo di origine è Città e l'attributo correlato è Stato. L'attributo di origine è il lato "molti" e il lato correlato è il lato "uno" della relazione molti-a-uno. La chiave per l'attributo di origine sarebbe Città + Stato. Per altre informazioni, vedere [Creare, modificare o eliminare una relazione tra attributi](../../analysis-services/multidimensional-models/attribute-relationships-create-modify-or-delete-relationship.md).  
  
 Per altre informazioni sulle proprietà di una relazione tra attributi, vedere [Configurare le proprietà della relazione tra attributi](../../analysis-services/multidimensional-models/attribute-relationships-configure-attribute-properties.md).  
  
> [!NOTE]  
>  Definire erroneamente relazioni tra attributi può produrre risultati della query non validi.  
  
## <a name="see-also"></a>Vedere anche  
 [Relazione tra attributi](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attribute-relationships.md)  
  
  
