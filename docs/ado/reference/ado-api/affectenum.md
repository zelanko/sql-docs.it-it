---
description: AffectEnum
title: AffectEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- AffectEnum
helpviewer_keywords:
- AffectEnum enumeration [ADO]
ms.assetid: 1ab921a0-6c57-43b4-9291-701b2599f3e8
author: rothja
ms.author: jroth
ms.openlocfilehash: d67a4916328d5d6d435da1b8080be42e52b35f67
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776650"
---
# <a name="affectenum"></a>AffectEnum
Specifica quali record sono interessati da un'operazione.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|Se al **Recordset**non è applicato alcun [filtro](./filter-property.md) , influiscono su tutti i record.<br /><br /> Se la proprietà **Filter** è impostata su un criterio di stringa, ad esempio "Author =' Smith '", l'operazione influiscono sui record visibili nel capitolo corrente.<br /><br /> Se la proprietà **Filter** è impostata su un membro di [FilterGroupEnum](./filtergroupenum.md) o di una matrice di segnalibri, l'operazione avrà effetto su tutte le righe del **Recordset**. **Nota: adAffectAll** è nascosto nell'Visualizzatore oggetti Visual Basic.|  
|**adAffectAllChapters**|4|Influiscono su tutti i record di tutti i capitoli di pari livello del **Recordset**, inclusi quelli non visibili tramite un **filtro** attualmente applicato.|  
|**adAffectCurrent**|1|Influiscono solo sul record corrente.|  
|**adAffectGroup**|2|Interessa solo i record che soddisfano l'impostazione della proprietà [filtro](./filter-property.md) corrente. Per usare questa opzione, è necessario impostare la proprietà **Filter** su un valore **FilterGroupEnum** o una matrice di **segnalibri** .|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. influisce su ALL|  
|AdoEnums. influisce. ALLCHAPTERS|  
|AdoEnums. influisce. CURRENT|  
|AdoEnums. influisce. GROUP|  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Metodo CancelBatch (ADO)](./cancelbatch-method-ado.md)  
        [Metodo Delete (Recordset - ADO)](./delete-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [Metodo Resync](./resync-method.md)  
        [Metodo UpdateBatch](./updatebatch-method.md)  
    :::column-end:::
:::row-end:::