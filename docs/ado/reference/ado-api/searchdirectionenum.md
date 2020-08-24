---
description: SearchDirectionEnum
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
ms.openlocfilehash: 13f8e73bc382493084c8d3712d4b7bda2ed35c13
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777530"
---
# <a name="searchdirectionenum"></a>SearchDirectionEnum
Specifica la direzione di una ricerca di record in un [Recordset](./recordset-object-ado.md).  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adSearchBackward**|-1|Esegue la ricerca all'indietro, arrestandosi all'inizio del **Recordset**. Se non viene trovata alcuna corrispondenza, il puntatore del record viene posizionato in [BOF](./bof-eof-properties-ado.md).|  
|**adSearchForward**|1|Cerca in futuro, arrestandosi alla fine del **Recordset**. Se non viene trovata alcuna corrispondenza, il puntatore del record viene posizionato in corrispondenza del valore [EOF](./bof-eof-properties-ado.md).|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. SearchDirection. Backward|  
|AdoEnums. SearchDirection. INOLTR|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo Find (ADO)](./find-method-ado.md)