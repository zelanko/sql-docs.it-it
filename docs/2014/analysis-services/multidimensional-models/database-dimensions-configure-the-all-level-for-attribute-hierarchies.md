---
title: Configurare il livello (totale) per le gerarchie degli attributi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- All members
- IsAggregatable property
- topmost levels [Analysis Services]
- (All) levels
- AttributeAllMemberName property
- levels [Analysis Services]
- members [Analysis Services], All
- AllMemberName property
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96e7e0cd5377e180630f10bdae6c32e33fcd119b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726785"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>Configurare il livello (Totale) per le gerarchie di attributi
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] il livello (Totale) è un livello facoltativo generato dal sistema. Contiene un solo membro il cui valore è determinato dall'aggregazione dei valori di tutti i membri nel livello immediatamente subordinato. Questo membro è denominato membro Totale. Si tratta di un membro generato dal sistema non contenuto nella tabella della dimensione. Poiché il membro nel livello (Totale) si trova al primo livello della gerarchia, il relativo valore è determinato dall'aggregazione consolidata dei valori di tutti i membri della gerarchia. Il membro Totale spesso funge da membro predefinito di una gerarchia.  
  
 La presenza di un livello (Totale) nella gerarchia di un attributo dipende dall'impostazione della proprietà `IsAggregatable` dell'attributo, mentre la presenza di un livello (Totale) in una gerarchia definita dall'utente dipende dall'impostazione della proprietà `IsAggregatable` dell'attributo nel livello superiore della gerarchia definita dall'utente. Se la proprietà `IsAggregatable` è impostata su `True`, esisterà un livello (Totale). Se la proprietà `IsAggregatable` è impostata su `False`, il livello (Totale) non sarà presente.  
  
## <a name="establishing-the-topmost-level"></a>Determinazione del livello superiore  
 Se la proprietà `IsAggregatable` è impostata su `False` nell'attributo di origine di un livello di una gerarchia, la gerarchia non potrà contenere un livello aggregabile al di sopra di tale livello. È necessario che il livello non aggregabile sia il livello superiore di qualsiasi gerarchia oppure che la proprietà `IsAggregatable` degli attributi di origine in qualsiasi livello al di sopra di quello non aggregabile sia anch'essa impostata su `False`.  
  
## <a name="all-member-and-all-level"></a>Membro Totale e livello (Totale)  
 Il singolo membro del livello (Totale) è denominato membro Totale. Il `AttributeAllMemberName`proprietà su una dimensione specifica il nome del membro totale per gli attributi in una dimensione. La proprietà `AllMemberName` di una gerarchia specifica il nome del membro Totale per la gerarchia.  
  
## <a name="see-also"></a>Vedere anche  
 [Definire un membro predefinito](attribute-properties-define-a-default-member.md)  
  
  
