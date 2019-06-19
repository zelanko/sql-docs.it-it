---
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AllowNullsEnum
helpviewer_keywords:
- AllowNullsEnum enumeration [ADOX]
ms.assetid: 6acf3689-1a7f-4379-9d7f-df452ccbac27
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 53fadcddd49ebf68949da0a7dca3cb37da0b5d93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66708610"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Specifica se i record con valori null vengono indicizzati.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|L'indice consente le voci in cui le colonne chiave sono null. Se viene immesso un valore null in una colonna chiave, la voce viene inserita nell'indice.|  
|**adIndexNullsDisallow**|1|Valore predefinito. L'indice non consente le voci in cui le colonne chiave sono null. Se viene immesso un valore null in una colonna chiave, si verificherà un errore.|  
|**adIndexNullsIgnore**|2|L'indice non inserisce le voci che contengono le chiavi null. Se viene immesso un valore null in una colonna chiave, la voce viene ignorata e verrà generato alcun errore.|  
|**adIndexNullsIgnoreAny**|4|L'indice non inserisce le voci in cui alcune colonne chiave ha un valore null. Per un indice con una a più colonne chiave, se si immette un valore null in una colonna, la voce viene ignorata e verrà generato alcun errore.|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà IndexNulls (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
