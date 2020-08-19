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
ms.openlocfilehash: 551c2ec7b8351ed17841ed1a4073c1a411dc77d0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451293"
---
# <a name="affectenum"></a>AffectEnum
Specifica quali record sono interessati da un'operazione.  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adAffectAll**|3|Se al **Recordset**non è applicato alcun [filtro](../../../ado/reference/ado-api/filter-property.md) , influiscono su tutti i record.<br /><br /> Se la proprietà **Filter** è impostata su un criterio di stringa, ad esempio "Author =' Smith '", l'operazione influiscono sui record visibili nel capitolo corrente.<br /><br /> Se la proprietà **Filter** è impostata su un membro di [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) o di una matrice di segnalibri, l'operazione avrà effetto su tutte le righe del **Recordset**. **Nota: adAffectAll** è nascosto nell'Visualizzatore oggetti Visual Basic.|  
|**adAffectAllChapters**|4|Influiscono su tutti i record di tutti i capitoli di pari livello del **Recordset**, inclusi quelli non visibili tramite un **filtro** attualmente applicato.|  
|**adAffectCurrent**|1|Influiscono solo sul record corrente.|  
|**adAffectGroup**|2|Interessa solo i record che soddisfano l'impostazione della proprietà [filtro](../../../ado/reference/ado-api/filter-property.md) corrente. Per usare questa opzione, è necessario impostare la proprietà **Filter** su un valore **FilterGroupEnum** o una matrice di **segnalibri** .|  
  
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
        [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)  
        [Metodo Delete (Recordset - ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)  
    :::column-end:::
    :::column:::
        [Metodo Resync](../../../ado/reference/ado-api/resync-method.md)  
        [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)  
    :::column-end:::
:::row-end:::
