---
title: Proprietà livello | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- user hierarchies [Analysis Services]
- hierarchies [Analysis Services], user
ms.assetid: dabb7335-887b-442a-b67c-4901ba1242b7
author: minewiskan
ms.author: owend
ms.openlocfilehash: 553503b9d35142bcc998b4ec12ad2e29d4c66318
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545073"
---
# <a name="level-properties"></a>Proprietà di livello 
  Nella tabella seguente vengono elencate e descritte le proprietà di un livello in una gerarchia definita dall'utente.  
  
|Proprietà|Descrizione|  
|--------------|-----------------|  
|Descrizione|Contiene la descrizione del livello.|  
|HideMemberIf|Indica se e quando un membro di un livello deve essere nascosto per le applicazioni client. I possibili valori della proprietà sono i seguenti:<br /><br /> Mai<br /> I membri non vengono mai nascosti. Si tratta del valore predefinito.<br /><br /> OnlyChildWithNoName<br /> Un membro viene nascosto quando il membro è l'unico figlio del relativo padre e il nome del membro è vuoto.<br /><br /> OnlyChildWithParentName<br /> Un membro viene nascosto quando il membro è l'unico figlio del relativo padre e il nome del membro è uguale a quello del relativo padre.<br /><br /> NoName<br /> Un membro viene nascosto quando il nome del membro è vuoto.<br /><br /> ParentName<br /> Un membro viene nascosto quando il nome del membro è uguale a quello del relativo padre.|  
|ID|Contiene l'identificatore univoco (ID) del livello.|  
|Nome|Contiene il nome descrittivo del livello. Per impostazione predefinita, il nome di un livello è uguale al nome dell'attributo di origine.|  
|SourceAttribute|Contiene il nome dell'attributo di origine sul quale si basa il livello.|  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà delle gerarchie definite dall'utente](user-hierarchies-properties.md)  
  
  
