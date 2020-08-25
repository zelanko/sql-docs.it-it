---
description: Comandi ibridi
title: Comandi ibridi | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- hybrid commands [ADO]
- data shaping [ADO], hybrid commands
ms.assetid: e8ca40e8-459c-40e2-8dd3-3ec6d5ee7b51
author: rothja
ms.author: jroth
ms.openlocfilehash: fe4661618a56f208f0aeea7e66d5f57d4f95c44d
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805985"
---
# <a name="hybrid-commands"></a>Comandi ibridi
I comandi ibridi sono comandi con parametri parziali. Ad esempio:  
  
```  
SHAPE {select * from plants}   
   APPEND( {select * from customers where country = ?}   
           RELATE PlantCountry TO PARAMETER 0,   
             PlantRegion TO CustomerRegion )   
```  
  
 Il comportamento di memorizzazione nella cache per un comando ibrido è identico a quello dei normali comandi con parametri.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di data shaping](./data-shaping-example.md)   
 [Grammatica forma formale](./formal-shape-grammar.md)   
 [Comandi Shape in generale](./shape-commands-in-general.md)