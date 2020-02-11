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
ms.openlocfilehash: 48e9d8c40d2ab76b902d285526fcd9e9abf7be07
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67967335"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Specifica se i record con valori null sono indicizzati.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|L'indice consente le voci in cui le colonne chiave sono null. Se viene immesso un valore null in una colonna chiave, la voce viene inserita nell'indice.|  
|**adIndexNullsDisallow**|1|Default. L'indice non consente le voci in cui le colonne chiave sono null. Se viene immesso un valore null in una colonna chiave, si verificherà un errore.|  
|**adIndexNullsIgnore**|2|L'indice non inserisce voci contenenti chiavi null. Se viene immesso un valore null in una colonna chiave, la voce viene ignorata e non si verifica alcun errore.|  
|**adIndexNullsIgnoreAny**|4|L'indice non inserisce voci in cui alcune colonne chiave hanno un valore null. Per un indice con una chiave a più colonne, se viene immesso un valore null in una colonna, la voce viene ignorata e non si verifica alcun errore.|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà IndexNulls (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
