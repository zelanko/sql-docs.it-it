---
title: SearchDirectionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- SearchDirectionEnum
helpviewer_keywords:
- SearchDirectionEnum enumeration [ADO]
ms.assetid: 81272ae3-2165-4f4e-adfe-9ede0368cb17
author: rothja
ms.author: jroth
ms.openlocfilehash: 7e2928f1817b994c3101182677b5b2fcad9a4b1d
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755778"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Specifica la direzione di una ricerca di record in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Esegue la ricerca all'indietro, arrestandosi all'inizio del **Recordset**. Se non viene trovata alcuna corrispondenza, il puntatore del record viene posizionato in [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Cerca in futuro, arrestandosi alla fine del **Recordset**. Se non viene trovata alcuna corrispondenza, il puntatore del record viene posizionato in corrispondenza del valore [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. SearchDirection. Backward|  
|AdoEnums. SearchDirection. INOLTR|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Find (ADO)](../../../ado/reference/ado-api/find-method-ado.md)
