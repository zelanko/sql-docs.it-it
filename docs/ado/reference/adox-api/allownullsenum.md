---
description: AllowNullsEnum
title: AllowNullsEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: c2d21b4a7e4de67e45210f11598a7cf3a2a99b9e
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985542"
---
# <a name="allownullsenum"></a>AllowNullsEnum
Specifica se i record con valori null sono indicizzati.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adIndexNullsAllow**|0|L'indice consente le voci in cui le colonne chiave sono null. Se viene immesso un valore null in una colonna chiave, la voce viene inserita nell'indice.|  
|**adIndexNullsDisallow**|1|Valore predefinito. L'indice non consente le voci in cui le colonne chiave sono null. Se viene immesso un valore null in una colonna chiave, si verificherà un errore.|  
|**adIndexNullsIgnore**|2|L'indice non inserisce voci contenenti chiavi null. Se viene immesso un valore null in una colonna chiave, la voce viene ignorata e non si verifica alcun errore.|  
|**adIndexNullsIgnoreAny**|4|L'indice non inserisce voci in cui alcune colonne chiave hanno un valore null. Per un indice con una chiave a più colonne, se viene immesso un valore null in una colonna, la voce viene ignorata e non si verifica alcun errore.|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà IndexNulls (ADOX)](./indexnulls-property-adox.md)